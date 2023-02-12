

### 그래프 읽는 법
```mermaid
graph TD


classA --상속 관계--> classB
classA -.그냥 다른 관계?.->classC


```

# event classes hierarchy
```mermaid

graph TD
  
A[event_worker_group]
B[event_worker]
C[event_channel]
D[event_layer]
E[event_handler]
F[byte_encoder]
G[object_encoder]
H[byte_decoder]
I[object_decoder]
J[logic_adapter]

A --> B
B --> C
C --> D
C -.-> server
C -.-> stream
D --> E

E --> F
E --> G
E --> H
E --> I
E --> J

class A,B,C,D,E,F,G,H,I,J,K,L,M,N,O,P,Q,R,S,T,U,V,W,X,Y,Z internal-link;



```



---
# other util classes

## socket utils
``` mermaid
classDiagram

	class socket {
		bind()
		connect()
		listen()
		accept()
		name()
		send()
		close()
		set_socket_linger()
		set_tcp_nodelay()
		set_nonblocking()
		nosigpipe_connect()
		reuse_address_bind()
		forward_loockup()
		reverse_lookup()
	}
```
- forward_lookup: 


### byte_buffer
```mermaid
classDiagram

class byte_buffer {
	container_type buffer
	size_type position
	raw_buffer()
	raw_length()
	raw_shrink()
	get()
	size()
	empty()
	put()
	append_from()
	remove()
	discard()
	clear()
}
```

### server_bootstrap
```mermaid
classDiagram

class server_bootstrap {
	start_server()
}
```

start_server:
bind,  set_nonblock,  listen,  name socket.

### task_base
```mermaid
classDiagram

class task_base {
	run()
}
```

FT_SERV_DEFINE_TASK(name, T`N`, a`N` expr)
make class with name, has only member function run()
run() will do `expr` with each of type TN of argument aN

Flow of utils
