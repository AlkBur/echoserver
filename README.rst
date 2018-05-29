Echo servers in some languages
=================================

Echo server in different languages + framework.

Some code is writing the original code that was in the sample program,
epoll, thread version is created by methane (github.com/methane/echoserver).

test environment
-----------------

client and server are connected by Gigabit Ethernet.

server and client - one virtual computer
^^^^^^^^^^^^^^^
Lubuntu 18.04 (amd64)
Intel(R) Core(TM) i-3 4000M 2 CPU 2.40 GHz

test command
-------------

bench.sh does kick client 3 times with following option.

::

   ./client -c50 -o2 -h10000 127.0.0.1

C++ epoll
---------

server::

   ./server_epoll

result::

   Throughput: 32759.39 [#/sec]
   Throughput: 31857.36 [#/sec]
   Throughput: 30606.24 [#/sec]

with forking server::

   ./server_epoll -f2

result::

   Throughput: 38289.52 [#/sec]
   Throughput: 32920.54 [#/sec]
   Throughput: 2130.14 [#/sec]

C++ thread
-----------

server::

   ./server_thread -c120

result::

   Throughput: 37030.09 [#/sec]
   Throughput: 36148.11 [#/sec]
   Throughput: 38303.02 [#/sec]

C++ libev
-------------

server::

   ./server_libev

result::

   $ sh bench.sh 
   Throughput: 36378.17 [#/sec]
   Throughput: 34321.19 [#/sec]
   Throughput: 36602.43 [#/sec]
   $ sh bench.sh 
   Throughput: 38684.08 [#/sec]
   Throughput: 35297.25 [#/sec]
   Throughput: 34895.54 [#/sec]

libev have dynamic event queue size. So, first benchmark is slower than
after.
   
Rust (1.24.1)
----------

server::

   ./server_rust

result::

   Throughput: 37619.34 [#/sec]
   Throughput: 20236.68 [#/sec]
   Throughput: 15944.72 [#/sec]

Go (1.10)
-------

server::

   $ ./server_go

result::

   Throughput: 31057.19 [#/sec]
   Throughput: 32425.42 [#/sec]
   Throughput: 31929.84 [#/sec]

server::

   $ GOMAXPROCS=2 ./server_go

result::

   Throughput: 34154.67 [#/sec]
   Throughput: 34288.68 [#/sec]
   Throughput: 34541.08 [#/sec]
   
Haskell
----------

GHC 7.0.3

server::

   ./server_haskell

result::

   Throughput: 0 [#/sec]
   Throughput: 0 [#/sec]
   Throughput: 0 [#/sec]
   
Erlang
-------------

server::

   $ erl
   Erlang R14A (erts-5.8) [source] [64-bit] [smp:2:2] [rq:2] [async-threads:0] [hipe] [kernel-poll:false]
   Eshell V5.8  (abort with ^G)
   1> c(server_erlang, [native, {hipe, ['O3']}]).
   {ok,server_erlang}
   2> server_erlang:listen(5000).

result::

   Throughput: 0 [#/sec]
   Throughput: 0 [#/sec]
   Throughput: 0 [#/sec]

pypy 1.6 + Tornado 2.0
-----------------------

server::

   ~/pypy-1.6/bin/pypy server_tornado.py 

result::

   Throughput: 0 [#/sec]
   Throughput: 0 [#/sec]
   Throughput: 0 [#/sec]


pypy 1.8 + Tornado 2.2
-----------------------

server::

   ~/pypy-1.8/bin/pypy server_tornado.py 

result::

   Throughput: 0 [#/sec]
   Throughput: 0 [#/sec]
   Throughput: 0 [#/sec]


pypy 1.6 + twisted
-------------------

server::

   ~/pypy-1.6/bin/pypy server_twisted.py 

result::

   Throughput: 0 [#/sec]
   Throughput: 0 [#/sec]
   Throughput: 0 [#/sec]


node.js  0.5.4
---------------

server::

   ~/local/node-0.5.4/bin/node server_node.js


result::

   Throughput: 0 [#/sec]
   Throughput: 0 [#/sec]
   Throughput: 0 [#/sec]



Ruby 1.9.1 + EventMachine 0.12.10
-----------------------------------

server::

   $ ruby1.9.1 server_em.rb

result::

   Throughput: 0 [#/sec]
   Throughput: 0 [#/sec]
   Throughput: 0 [#/sec]



Ruby 1.9.1 + rev 0.3.2
-------------------------

server::

   $ ruby1.9.1 server_rev.rb

result::

   Throughput: 0 [#/sec]
   Throughput: 0 [#/sec]
   Throughput: 0 [#/sec]



Python 2.7.2 + Tornado
-------------------------

server::

   ~/python2.7/bin/python server_tornado.py

result::

   Throughput: 0 [#/sec]
   Throughput: 0 [#/sec]
   Throughput: 0 [#/sec]


Python 2.7.2 + gevent
-------------------------------

server::

   ~/python2.7/bin/python server_gevent.py

result for gevent 0.13.6::

   Throughput: 0 [#/sec]
   Throughput: 0 [#/sec]
   Throughput: 0 [#/sec]

result for gevent 1.0a2::

   Throughput: 0 [#/sec]
   Throughput: 0 [#/sec]
   Throughput: 0 [#/sec]


gevent-1.0a2 without greenlet. Event driven fashion::

   ~/python2.7/bin/python server_gevent_loop.py

result::

   Throughput: 0 [#/sec]
   Throughput: 0 [#/sec]
   Throughput: 0 [#/sec]



Python 2.7.2 + Twisted
----------------------

server::

   ~/python2.7/bin/python server_twidted.py

result::

   Throughput: 0 [#/sec]
   Throughput: 0 [#/sec]
   Throughput: 0 [#/sec]


..
   vim: paste sw=3 expandtab
