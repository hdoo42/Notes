#Q perpose of  **F_DUPFD_CLOEXEC** and  **O_CLOEXEC**

Note that the use of this flag is essential in some multithreaded programs, because using a separate [fcntl(2)](https://man7.org/linux/man-pages/man2/fcntl.2.html)

**F_SETFD** operation to set the **FD_CLOEXEC** flag does not suffice to avoid race conditions where one thread opens a file descriptor and attempts to set its close-on-exec flag using [fcntl(2)](https://man7.org/linux/man-pages/man2/fcntl.2.html) at the same time as another thread does a [fork(2)](https://man7.org/linux/man-pages/man2/fork.2.html) plus [execve(2)](https://man7.org/linux/man-pages/man2/execve.2.html).
Depending on the order of execution, the race may lead to the file descriptor returned by **open**() being unintentionally leaked to the program executed by the child process created by [fork(2)](https://man7.org/linux/man-pages/man2/fork.2.html).
(This kind of race is in principle possible for any system call that creates a file descriptor whose close-on-exec flag should be set, and various other Linux system calls provide an equivalent of the **O_CLOEXEC** flag to deal with this problem.)

---
#Q why doesn't effect nonblock on the operation of poll, select, epoll?

and why the hell we use them?

Note that the setting of this flag has no effect on the
operation of [poll(2)](https://man7.org/linux/man-pages/man2/poll.2.html), [select(2)](https://man7.org/linux/man-pages/man2/select.2.html), [epoll(7)](https://man7.org/linux/man-pages/man7/epoll.7.html), and similar,
since those interfaces merely inform the caller about
whether a file descriptor is "ready", meaning that an I/O
operation performed on the file descriptor with the
**O_NONBLOCK** flag _clear_ would not block.

Note that this flag has no effect for regular files and
block devices; that is, I/O operations will (briefly)
block when device activity is required, regardless of
whether **O_NONBLOCK** is set.  Since **O_NONBLOCK** semantics
might eventually be implemented, applications should not
depend upon blocking behavior when specifying this flag
for regular files and block devices.

#conjecture maybe because of this? (named pipe)
For the handling of FIFOs (named pipes), see also [fifo(7)](https://man7.org/linux/man-pages/man7/fifo.7.html).
For a discussion of the effect of **O_NONBLOCK** in
conjunction with mandatory file locks and with file
leases, see [fcntl(2)](https://man7.org/linux/man-pages/man2/fcntl.2.html).




