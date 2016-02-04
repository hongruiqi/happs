Q. If I have 2GB of state, will small changes be written directly to the disk, or will the entire 2GB be written?

A:
  * The full 2GB will be written on each checkpoint.
  * The transaction log is effectively an incremental diff between the current state and the and the latest checkpoint.