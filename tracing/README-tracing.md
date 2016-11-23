Sandfly
-------

You're currently hard at work building microservices, and there's a
bug. In a monolith, you've got a bevy of tools at your disposal to fix
the bug: log data, profilers, stack traces. But all of this falls
apart when your code is scattered across multiple microservices.

Moreover, your debugging *must* happen in production. (You never see
these bugs in staging, do you?)

Introducing Sandfly.

Sandfly is a microservices debugger. Sandfly gives you:

- distributed stack traces. If a particular exception is thrown,
  Sandfly will tell you all the services that led to that exception
  being thrown.
- threaded log views. View the aggregated application log data for a
  given request -- in the order in which the application is executed.
  performance.


Sandfly is always-on, lightweight, and is designed to run on your
production systems.