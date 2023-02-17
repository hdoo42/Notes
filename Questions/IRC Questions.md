#### #Q Why do some typedefs end with `_t` and others with `_type`? 

#conjecture
 *`_t`* for simple typedef(trivial types)
 *`_type`* for complex typedef.

----
#### #Q What is `__base` in size_type of byte_buffer?
Especially in our irc project, it is just a vector type.

----
#### #Q Why redefine after #cpp14?

``` c++
#if _LIBCPP_STD_VER > 14
template <bool __b>
with bool_constant = integral_constant<bool, __b>;
#Define _LIBCPP_BOOL_CONSTANT(__b) bool_constant<(__b)>.
#else
define _LIBCPP_BOOL_CONSTANT(__b) integral_constant<bool,(__b)> #endif
#endif
```
#conjecture 
template argument with non-typename is after #cpp11 option?

#in_real
use "using" with template is since #cpp11

---
#### #Q Why does event channel go to server and stream, not client and stream?

What I think:
event_channel is what we get event from. stream means that event is stream, so it is streamed from socket continuously?
But what is server mean?
and if is a client, what does it mean?
how different from client and stream then?

#conjecture 
Server makes stream child inside. 
Server accepts sockets, but stream doesn't.
So stream doesn't do task stand alone, but server makes accepts, and make child stream and then use stream in it?

#SUB #Q Is stream always child of server? or can it be independent?

---
#### #Q Why set O_NONBLOCK even if it doesn't affect select, (e)poll, and similar?

Does it affect kqueue?

#in_real it will be used in non-block read.


#### #Q Why use `size_type()` instead of 0 in byte_buffer.hpp?
in byte_buffer.hpp:140;

for compatability.


#### #Q start_server takes make_server_t, what is that?

