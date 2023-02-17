### socket utils
|function|discription| 
|--------|-----------|
|bind_socket||
|connect_socket||
|listen_socket|_listen()_ with backlog (default to **FT..BACKLOG**)|
|accept_socket||
|name||
|send||
|close||
|set_socket_linger||
|set_tcp_nodelay||
|set_nonblocking||
|nosigpipe_connect||
|reuse_address_bind| _setsockopt()_ with **SOL_SOCKET**, **SO_REUSEADDR** and _bind()_|
|forward_loockup|_getaddrinfo()_ with hints, do _socket()_, apply one of above two(nosig..., reuse...). |
|reverse_lookup|Do _getnameinfo()_ so that get name from address.|

### byte_buffer
|function|discription| 
|--------|-----------|
|raw_buffer|| 
|raw_length|| 
|raw_shrink|| 
|get|| 
|size|| 
|empty|| 
|put|| 
|append_from||
|remove|| 
|discard|| 
|clear|| 
 
|variable|discription| 
|--------|-----------|
|buffer||
|position||

### server_bootstrap
|function|discription| 
|--------|-----------|
|start_server||

### task_base
|function|argument|discription| 
|--------|--------|-----------|
|FT_SERV_DEFINE_TASK|name, T`N`, a`N`, expr| make class with name has only member function run()

|function|discription| 
|--------|-----------|
|run|this will do `expr` with each of type TN of argument aN|

# bootstrap flow

start_server(...)
->bind_socket(...)
->forward_lookup(...AI_PASSIVE, &reuse_address_bind);

  