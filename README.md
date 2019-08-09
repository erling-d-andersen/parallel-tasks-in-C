# parallel-tasks-in-C
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






I found the talk: Plain Threads are the GOTO of todays computing by Hartmut Kaiser very interesting 
because I have been working on improving the multithreaded code in MOSEK recently. And is also thinking how MOSEK should deal with all the cores in the CPUs in the future. I agree with Hartmut something else than plain threads is needed.



Here are some potential replacements:

Berkeley Unified Parallel C
CheckedThreads  Source with a liberal license. Cilk like. Both C and C++.
Cilk Plus Supported by Intel C, gcc and Clang.
HPX C++ only.
Occa. A unified approach to multithreaded languages. See also.
OpenMP Supported by many compilers.
Pfunc Cilk like features. Liberal license. Can be called from C but is C++.
Starpu
Threaded building blocks. C++ only.
Wool  A pure C implementation that provides something very close to Cilk. 
XKAAPI
Previously I have used OpenMP but I really dislike that. In my opinion it is somewhat ugly and you feel the Fortran origins. Recently I have played with Cilk which is very simple.



Checkedthreads seems like a good option if a simple C only tool can do the job. I have plan to try that at MOSEK.



Pfunc seems very powerful and there is ph.d. thesis about its design. The project might be semi-dead though.



Wool also seems very interesting. It is plain C and the author claims the spawn overhead is very low. There is also an older comparison with other task libraries.



Btw I biased towards tools that has no C++ bindings because currently MOSEK is plain C code. Adding a dependency on a C++ runtime library adds headaches.



Some common terminology when working on parallism is

Fork-join parallel model
Pthreads programming and tutorial
