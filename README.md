cedb
====

Console Erlang Debugger.

Run debug directly from console.

Run debug
---------

Go inside the example app and run the shell:

```sh
cd examples/test
rebar3 shell
```

```erlang
1> application:ensure_all_started(cedb).
2> % Set a breakpoint in `test.erl` module in line `16`
2> cedb:break(test, 16).
3> % Set a breakpoint in `test.erl` module `function2` with arity `1`
3> cedb:break(test, function2, 1).
4> % run the application to debug
4> test:start().

=> {<0.258.0>,{attached,test,16,false}}

File /projects/cedb/examples/test/_build/default/lib/test/src/test.erl

   11:       function1(),
   12:       io:format("Finish~n").
   13:
   14:     function1() ->
  *15:       A = "Hello",
   16:       B = #{A => <<"c">>},
   17:       function2(B),
   18:       io:format("I'm in function 1~n").
   19:
   20:     function2(C) ->
   21:       io:format("I'm in function 2, the value is ~p~n", [C]),

cedb> next.
ok 
=> {<0.258.0>,running}

File /projects/cedb/examples/test/_build/default/lib/test/src/test.erl

   11:       function1(),
   12:       io:format("Finish~n").
   13:
   14:     function1() ->
   15:       A = "Hello",
  *16:       B = #{A => <<"c">>},
   17:       function2(B),
   18:       io:format("I'm in function 1~n").
   19:
   20:     function2(C) ->
   21:       io:format("I'm in function 2, the value is ~p~n", [C]),

cedb> A.
"Hello"
cedb> n.
ok 
=> {<0.258.0>,running}
cedb>
```

Commands
--------

You can run the current commands when the debugger is running:

Command      | Description
-------------|-------------------------------------------
backtrace    | Show backtrace.
bindings     | Show binded variables.
continue     | Continue the execution of the process.
finish       | Finish the debug session.
messages     | Show process messages.
next         | Execute next instruction.
skip         | Skip.
step         | Step inside next instruction.
stop         | Stop debugging.
timeout      | Timeout.
Var          | Variable names are evaluated in the current context.

Abbreviations of the above commands are also accepted, like `n` for `next`, `ba` for `backtrace` etc.
