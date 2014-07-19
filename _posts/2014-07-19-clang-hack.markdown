---
layout: post
title:  "Nios II clang port status"
date:   2014-07-19 23:06:38
categories: compiler
---

Nios II clang port is finally "working". It depends on the altera gcc chain tools to generate
object code.

* Clone llvm core and clang
{% highlight bash %}
$ git clone https://github.com/ivanllopard/nios2-llvm.git
$ export LLVM_SOURCE=`pwd`/nios2-llvm
$ cd nios2-llvm/tools
$ git clone https://github.com/ivanllopard/nios2-clang.git
{% endhighlight %}

* Build llvm and clang inside a new build directory.
{% highlight bash %}
$ mkdir build
$ cd build
$ $LLVM_SOURCE/configure --enable-optimized --target=nios2 --enable-targets=nios2
$ make -j2 && sudo make install
{% endhighlight %}

You will get the nios2-clang compiler installed at the default prefix path.
Currently, the front-end uses nios2-elf-as and nios2-elf-ld from the altera
toolchain.
You can either compile the entire toolchain from its [sources][nios2-elf-toolchain] or
download a compiled version which comes with the [Nios II Embedded Design Suite Legacy Tools][altera-nios2-eds]
Similar to nios2-elf-gcc, nios2-clang depends on nios2 system includes installed
at H-i686-pc-linux-gnu/nios2-elf/include.

The compiler is still at its "hack" state, I do not have a board to fully test
it. Please feel free to clone the repo and submit patches!

[altera-nios2-eds]: https://www.altera.com/download/software/nios-ii
[nios2-elf-toolchain]: ftp://ftp.altera.com/outgoing/download/support/ip/processors/nios2/gnu/nios2_gnu_gcc4_13.0.gz
