# Frequently Asked Questions #

## Why use GEF over PEDA? ##

[PEDA](https://github.com/longld/peda) is a fantastic tool that provides similar
commands to make the exploitation development process smoother.

However, PEDA suffers from a major drawbacks, which the code is too
fundamentally linked to Intel architectures (x86-32 and x86-64). On the other
hand, not only GEF supports all the architecture supported by GDB
(currently x86, ARM, AARCH64, MIPS, PowerPC, SPARC) but is designed to integrate
new architectures very easily as well!

Also, PEDA development is quite idle for a few years now, and many new
interesting features a debugger can provide simply do not exist.


## I cannot get GEF to setup!! ##

GEF will work on any GDB 7.x compiled with Python support. You can view
that commands that failed to load using `gef missing`, but this will not affect
GEF generally.

If you have problems setting up on your host, please use the
IRC [`freenode##gef`](https://webchat.freenode.net/?channels=##gef) for that.
Note that the GitHub issue section is to be used to **report bugs** and
**GEF issues** (like unexpected crash, improper error handling, weird edge case,
etc.), not a place to ask for help.


## I get a SegFault when starting GDB with GEF ##

A long standing bug in the `readline` library can make `gef` crash GDB
when displaying certain characters (SOH/ETX). As a result, this would SIGSEGV
GDB as `gef` is loading, a bit like this:

```
root@debian-aarch64:~# gdb -q ./test-bin-aarch64
GEF ready, type `gef' to start, `gef config' to configure
53 commands loaded, using Python engine 3.4
[*] 5 commands could not be loaded, run `gef missing` to know why.
[+] Configuration from '/root/.gef.rc' restored
Reading symbols from ./bof-aarch64...(no debugging symbols found)...done.
Segmentation fault (core dumped)
```

If so, this can be fixed easily by setting the `gef.readline_compat` variable to
`True` in the `~/.gef.rc` file. Something like this:

```
root@debian-aarch64:~# nano ~/.gef.rc
[...]
[gef]
readline_compat = True
```

You can now use all features of `gef` even on versions of GDB compiled against
old `readline` library.


## Does GEF prevent the use of other GDB plugins? ##

Definitely not! You can use any other GDB plugin on top of it for an even better
debugging experience.

Some interesting plugins highly recommended too:

- [!exploitable](https://github.com/jfoote/exploitable/)
- [Voltron](https://github.com/snare/voltron)

![voltron](https://pbs.twimg.com/media/CsSkk0EUkAAJVPJ.jpg:large)
Src: [@rick2600: terminator + gdb + gef + voltron cc: @snare @_hugsy_](https://twitter.com/rick2600/status/775926070566490113)


## I want to contribute, where should I head first? ##

I would suggest reading thoroughly this documentation, just having a look to the
[CONTRIBUTE](https://github.com/hugsy/gef/blob/master/.github/CONTRIBUTING.md)
file of the project to give you pointers.

Also a good thing would be to join the `##gef` IRC channel
on [Freenode](https://webchat.freenode.net/?channels=##gef) to get in touch with
the people involved/using it.
