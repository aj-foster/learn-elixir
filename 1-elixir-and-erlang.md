# Elixir's Relationship to Erlang

Elixir is both quite new and quite old. Understanding how Elixir works as a programming language requires an understanding of its relationship with Erlang, a language developed by Ericsson in 1986.


## Erlang's Background

Erlang was developed by employees of Ericsson for use in the telecom industry. In this context, systems must be able to:

- Handle a lot of traffic
- Handle failures in one area without affecting others
- Work cohesively with other "nodes"
- Never crash

These sound like good ideas in general, but Erlang was built especially towards these goals. This means that certain other areas were *not* priorities:

- Raw speed of calculations
- Interoperability with other languages
- etc.

Erlang continues to run telecom-related software (as well as other things) today. Your phone may be communicating with an LTE tower running Erlang right now.


## Erlang's Component Parts

Let's talk through the parts of a running Erlang system, which will lead us into a comparison with Elixir.

In any computing environment, you have the hardware at the lowest level. On top of that, you have an operating system, whose job it is to translate computation requests into physical actions the hardware can take. If we're running a OS-level virtual machine, that's at this level too (not important for us).

    |-----------------------|
    | Operating System (OS) |
    |-----------------------|
    |       Hardware        |
    |-----------------------|

If we were writing C code, it would be compiled by the C compiler into something the OS understands directly. Our *application* would thus be another layer on top of the OS. However, we aren't writing C code, so there are a few more layers to consider.


### ERTS and BEAM

ERTS stands for Erlang Run-Time System, and BEAM stands for Björn's Erlang Abstract Machine. Neither of those are particularly important to us, because we're going to lump them both together into something we'll call "the Erlang VM".

ERTS/BEAM/the VM form another layer on top of the OS. Whereas C code compiles into something the OS understands, our code *doesn't*. You cannot take a compiled Erlang program to a computer and run it without Erlang installed. The Erlang VM is what translates our compiled code into something the OS understands.

    |-----------------------|
    |    Erlang VM (etc)    |
    |-----------------------|
    | Operating System (OS) |
    |-----------------------|
    |       Hardware        |
    |-----------------------|

This is not a novel concept. Java runs on the Java Virtual Machine (JVM) which has the goal of translating Java code that was compiled *anywhere* and making it run *everywhere*. It's up to the language's virtual machine to make sure things still work in different environments.


### OTP

Our next layer is Erlang's standard library, known as OTP. In the past, OTP stood for *Open Telecom Platform*, but nowadays it's just OTP.

> Sidenote: There's a common trope in the Elixir/Erlang community that comes up when you encounter a problem. It says "Ericsson probably encountered this problem 20 years ago and solved it." OTP is the collection of solutions for all of the problems.

Using OTP libraries is the same as using standard libraries in other languages: they're just there, and you can use them whenever you want.


### Application

In Erlang, the final layer is your application. It has access to OTP libraries, it runs on the Erlang VM, which translates it for the OS, which translates it for the hardware.

    |-----------------------|
    |    Your Application   |
    |-----------------------|
    |  OTP / Standard Lib.  |
    |-----------------------|
    |    Erlang VM (etc)    |
    |-----------------------|
    | Operating System (OS) |
    |-----------------------|
    |       Hardware        |
    |-----------------------|


## Elixir

It may seem like we're talking a bunch about an unrelated topic, but here's the good part: Elixir is another layer in the stack between our application and the OTP libraries.

    |-----------------------|
    |    Your Application   |     |--------|
    |-----------------------| <-- | Elixir |
    |  OTP / Standard Lib.  |     |--------|
    |-----------------------|
    |    Erlang VM (etc)    |
    |-----------------------|
    | Operating System (OS) |
    |-----------------------|
    |       Hardware        |
    |-----------------------|

That's it. *Once the application is compiled*, Elixir is just another set of standard libraries available to our code before it works with the same exact stack as Erlang. What does this mean? It means:

- Every time Ericsson solved a problem and put it in OTP, they solved it for us too.
- The fault-tolerance and high uptime of Erlang is ours.
- The distributed computing aspect of Erlang is ours too.

Now, note it says "once the application is compiled" above. Compiled Elixir bytecode looks exactly like Erlang bytecode, but the uncompiled versions don't look the same. We use a different compiler (the Elixir compiler) to get from code to bytecode.

    |-------------|    |-----------------|
    | Elixir Code | -> | Elixir Compiler |
    |-------------|    |-----------------| \  |----------|     |-----------|
                                            > | Bytecode | --> | Erlang VM |
    |-------------|    |-----------------| /  |----------|     |-----------|
    | Erlang Code | -> | Erlang Compiler |
    |-------------|    |-----------------|

Elixir has libraries and language features of its own, but at the end of the day, it's running on the Erlang VM.


## Summary and Takeaways

Erlang is old. Elixir is new. Because Elixir sits on top of Erlang, it gets to use all of the old, battle-tested features of Erlang while also giving us a pleasant syntax to work with. That's pretty cool.

When we install Elixir, therefore, we have to install Erlang (generally, first). Any machine that runs our Elixir code will also need the Erlang VM installed in one way or another (we'll talk more about that later). We'll get everything installed next.
