---
title: Debugging binder and bindings
---

When compiled with the symbol AGL_DEVEL defined, the ***binder***
understands the 2 configuration variables:

 - AFB_DEBUG_BREAK: to emit interrupts
 - AFB_DEBUG_WAIT: to wait interrupts

To use these variables, assign it the list of break or wait points
to reach.

Example:

```bash
$ AFB_DEBUG_BREAK=main-entry AFB_DEBUG_WAIT=start-load,start-exec afb-daemon ....
```

This tells to ***afb-daemon*** to break at the point **main-entry** and to
wait at the points **start-load** and **start-exec**.

The items of the list can be separated using comma, space, tab or new-line.

The break/wait points are, in the order of their occurrence:

- main-entry: before decode arguments
- main-args: before daemon setup
- main-start: before starting jobs
- start-entry: before initialisation of sessions and hooks
- start-load: before load and pre-init of bindings
- start-start: before init of bindings
- start-http: before start of http server
- start-call: before execution of requests of the command line (option --call)
- start-exec: before execution of child preocees

Note also that a call to 'personality' is inserted just after
the point start-start.