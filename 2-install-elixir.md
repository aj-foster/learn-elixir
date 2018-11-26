# Install Elixir and Erlang

Now that we understand the relationship between Erlang and Elixir, hopefully it is clear why we need to install both languages. Today we'll do just that.


## Installing asdf

If you've worked with multiple versions of Ruby or Node.js, you may be familiar with rvm/rbenv or nvm. These allow us to have multiple versions of a language or library installed at the same time, and easily switch between them for different projects. asdf is a similar project that works with multiple different languages and libraries.

The readme for asdf can be found [here](https://github.com/asdf-vm/asdf).

If you use **Bash on macOS**, you can do the following:

```bash
# Install common prerequisites and asdf.
brew install coreutils automake autoconf openssl libyaml readline libxslt libtool unixodbc
git clone https://github.com/asdf-vm/asdf.git ~/.asdf --branch v0.6.1

# Make the asdf command available in our terminal.
echo -e '\n. $HOME/.asdf/asdf.sh' >> ~/.bash_profile
echo -e '\n. $HOME/.asdf/completions/asdf.bash' >> ~/.bash_profile
source ~/.bash_profile

# Test that the asdf command is available by attempting to update.
asdf update

# Respect .nvmrc and other similar files if present.
echo "legacy_version_file = yes" >> ~/.asdfrc
```

asdf uses *plugins* for each language or framework it installs. We'll install the plugins for Erlang and Elixir now. You may be interested in using the Node.js plugin as well.


## Installing Erlang

The readme for asdf's Erlang plugin can be found [here](https://github.com/asdf-vm/asdf-erlang).

If you use macOS, you can do the following:

```bash
brew install wxmac
asdf plugin-add erlang
asdf install erlang 21.1.3
asdf global erlang 21.1.3
```

The build will take some time. You may see an error related to missing `fop`, but you should **not** see errors related to missing `wxtools` or `openssl`.


## Installing Elixir

The readme for asdf's Elixir plugin can be found [here](https://github.com/asdf-vm/asdf-elixir).

If you use macOS, you can do the following:

```bash
asdf plugin-add elixir
asdf install elixir 1.7.4-otp-21
asdf global elixir 1.7.4-otp-21
```

This installs Elixir 1.7.4 in a way that ensures it will work with the version of Erlang/OTP we installed earlier (21).


## A Quick Test

From anywhere, run `iex`. It should print something similar to the following:

```
Erlang/OTP 21 [erts-10.1.3] [source] [64-bit] [smp:4:4] [ds:4:4:10] [async-threads:1] [hipe]

Interactive Elixir (1.7.4) - press Ctrl+C to exit (type h() ENTER for help)
```

Check `Erlang/OTP 21` and `Interactive Elixir (1.7.4)`. Then, run `:observer.start()`. You should see a window open with diagnostic information about the running Erlang VM. (It may not look good on macOS with dark mode enabled). Type `:observer.stop()` to end it, and `Ctrl+C` twice to exit IEx.
