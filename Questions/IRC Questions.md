#### #Q  Why some of typedef is ended with `_t`, and som other is with `_type`? 

#conjecture
 *`_t`* for simple typedef(trivial types)
 *`_type`* for complex typedef.

----
#### #Q  What is `__base` in size_type of byte_buffer?
in particular, on our project irc, it is just a vector type.



----
#### #Q Why redefine after #cpp14 here?

``` c++
#if _LIBCPP_STD_VER > 14
template <bool __b>
using bool_constant = integral_constant<bool, __b>;
#define _LIBCPP_BOOL_CONSTANT(__b) bool_constant<(__b)>
#else
#define _LIBCPP_BOOL_CONSTANT(__b) integral_constant<bool,(__b)>
#endif
```
#conjecture 
template argument with non-typename is after #cpp11 option?

#in_real
using with template is since #cpp11

---
#### #Q Why event channel goes to server and stream, not client and stream?

What I think:
event channel is what we get event from. stream means that event is stream, so It continuesly streamed from socket?
but what is server mean?
and what if it is client mean?
how different from client and stream then?

#conjecture 
server makes stream child inside. 
server accept sockets but stream dosen't.
So, stream doesn't do task stand alone, but server makes accepts, and make child stream and then use stream in it.?

#SUB #Q is stream always child of server? or it can be independant?


---
#### #Q Why set O_NONBLOCK even if doesn't affect to select, (e)poll, and similar?
It does effect on kqueue?

---
#### #Q why use `size_type()` instead of 0
in byte_buffer.hpp:140;

---
#### #Q server_bootstrap takes make_server_t, what is this?

---
#### #Q what is boss mean in bootstrap


