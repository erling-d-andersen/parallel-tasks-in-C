# Parallelizing C code: What are the options

This repository contains no code but rather describe my finding about writing parallel problems in C

Among other stuff I do then I am developer at Mosek. One of my tasks is to parallelize C code e.g. a sparse Cholesky computation.
Now parallelizing C using native threads such as pthread is major pain and therefore it is better to use an API or framework that makes it easy.

My current favourite is [Cilk](https://www.cilkplus.org/) which provides a very simplex extension to C language. The example
<pre>
cilk_spawn f();
cilk_spawn g();
cilk sync;
</pre>
will make the functions f and g run in parallel. Very simple and very powerful. I have relied on Cilk as implemented in Intel C to run my code. Unforfortuantely Intel has [deprecated](https://software.intel.com/en-us/forums/intel-cilk-plus/topic/745556) support Cilk code.

So Cilk seems dead but it seems a Cilk inspired parallel feature has just been introduced in Julia. For details see the [Julia blog](https://julialang.org/blog/2019/07/multithreading). Also the original inventors of Cilk is still working on it. See [Cilk at MIT](http://cilk.mit.edu).

Due to the deprecation of Cilk then I am looking for an alternative that can used in C. Below 

* [CheckedThreads](https://github.com/yosefk/checkedthreads)  Source with a liberal license. Cilk like. Both C and C++.
* [C thread pool](https://github.com/Pithikos/C-Thread-Pool)  Source with a liberal license.
* [OpenMP](openmp.org) Supported by many compilers.
* [PARTR](https://github.com/kpamnany/partr) Runtime engine written in C. It is employed in Julia for their Cilk inspired parallelization. 
* [Pfunc](https://projects.coin-or.org/PFunc). Cilk like features. Liberal license. Can be called from C but is C++. Seems very powerful and there is ph.d. thesis about its design. The project might be semi-dead though.
* Threaded building blocks. C++ only.
* [Cpp task flow](https://github.com/cpp-taskflow/cpp-taskflow). C++ only.

# Terminology

Some common terminology when working on parallism is

* [Fork-join](http://en.wikipedia.org/wiki/Fork%E2%80%93join_model) parallel model.
* [Pthreads](http://dreamrunner.org/wiki/public_html/Books%20Review/Pthreads%20Programming/Pthreads%20Programming.html) programming and tutorial
