**Note, this page is out of date**

# Introduction #

This is an overview of the HAppS architecture.

# Event System Semantics #

The event system is based on the state monad. You have updates `(a -> (a, ()))` and queries `(a -> ret)`. HAppS takes care of durability itself.

Events can either be created by `expose` or by hand.
Creating events by hand is only necessary if you need exact control of the serialization process.

# Durability #

  * HAppS treats all events as atomic and puts them in a total order so you never need to worry about concurrency (isolation).
  * HAppS achieves durability by state checkpointing and write-ahead logging events. End-users can never be confused by a server reboot because HAppS won't execute responses or side effects until their driving events have been logged.
  * HAppS also tracks which side-effects have completed. If the server is rebooted before a side-effect completes, HAppS will retry on recovery.