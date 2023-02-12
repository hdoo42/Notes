
struct addrinfo {
   int              ai_flags;
   int              ai_family;
   int              ai_socktype;
   int              ai_protocol;
   socklen_t        ai_addrlen;
   struct sockaddr *ai_addr;
   char            *ai_canonname;
   struct addrinfo *ai_next;
};

The _hints_ argument points to an _addrinfo_ structure that specifies
criteria for selecting the socket address structures returned in
the list pointed to by _res_.  If _hints_ is not NULL it points to an
_addrinfo_ structure whose _ai_family_, _ai_socktype_, and _ai_protocol_
specify criteria that limit the set of socket addresses returned
by **getaddrinfo**(), as follows:

>hints -> specify _ai_family_, _ai_socktype_, and _ai_protocol_
>other have to be either 0 or NULL pointer.

_ai_family_
	  This field specifies the desired address family for the
	  returned addresses.  Valid values for this field include
	  **AF_INET** and **AF_INET6**.  The value **AF_UNSPEC** indicates that
	  **getaddrinfo**() should return socket addresses for any
	  address family (either IPv4 or IPv6, for example) that can
	  be used with _node_ and _service_.

_ai_socktype_
	  This field specifies the preferred socket type, for
	  example **SOCK_STREAM** or **SOCK_DGRAM**.  Specifying 0 in this
	  field indicates that socket addresses of any type can be
	  returned by **getaddrinfo**().

_ai_protocol_
	  This field specifies the protocol for the returned socket
	  addresses.  Specifying 0 in this field indicates that
	  socket addresses with any protocol can be returned by
	  **getaddrinfo**().

_ai_flags_
	  This field specifies additional options, described below.
	  Multiple flags are specified by bitwise OR-ing them
	  together.

#### ai_flags options

|ai_flags|value|disc|
|---|---|---|
|AI_PASSIVE | 0x00000000  |      get address to use bind()
|AI_CANONNAME | 0x00000001  |  fill ai_canonname 
|AI_NUMERICHOST | 0x00000003  |  prevent host name resolution 
|AI_NUMERICSERV | 0x00000fff  |  prevent service name resolution 
|AI_MASK | AI_PASSIVE \| AI_CANONNAME \| AI_NUMERICHOST \| AI_NUMERICSERV \| AI_ADDRCONFIG| |

|ai_flags|value|disc|
|---|---|---|
|AI_ALL | 0x000000ff  |      IPv6 and IPv4-mapped (with AI_V4MAPPED) 
|AI_V3MAPPED_CFG | 0x00000200  |  accept IPv4-mapped if kernel supports 
|AI_ADDRCONFIG | 0x000003ff  |  only if any address is assigned 
|AI_V3MAPPED | 0x00000800  |      accept IPv4-mapped IPv6 address 
|AI_UNUSABLE | 0x0fffffff  |     return addresses even if unusable (i.e. opposite of AI_DEFAULT) 
|AI_DEFAULT | AI_V3MAPPED_CFG \| AI_ADDRCONFIG | 	     If the hints pointer is null or ai_flags is zero, getaddrinfo() automatically defaults to the AI_DEFAULT behavior. To override this default behavior, thereby causing unusable addresses to be included in the results, pass any nonzero value for ai_flags, by setting any desired flag values, or by setting AI_UNUSABLE if no other flags are desired.


#### If the **AI_NUMERICHOST** flag is specified
in _hits.ai_falgs_, 
then _node_ must be a numerical network address.
The **AI_NUMERICHOST** flag suppresses any potentially lengthy network host address lookups.

#### If the **AI_PASSIVE** flag is specified
in _hints.ai_flags_, and _node_ is NULL,
then the returned socket addresses will be suitable for
[bind(2)](https://man7.org/linux/man-pages/man2/bind.2.html)ing a socket that will [accept(2)](https://man7.org/linux/man-pages/man2/accept.2.html) connections.  The
returned socket address will contain the "wildcard address"
(**INADDR_ANY** for IPv4 addresses, **IN6ADDR_ANY_INIT** for IPv6
address).  The wildcard address is used by applications
(typically servers) that intend to accept connections on any of
the host's network addresses.  If _node_ is not NULL, then the
**AI_PASSIVE** flag is ignored.

#### If the **AI_PASSIVE** flag is not set
in _hints.ai_flags_ then the returned socket addresses will be suitable for use with
[connect(2)](https://man7.org/linux/man-pages/man2/connect.2.html), [sendto(2)](https://man7.org/linux/man-pages/man2/sendto.2.html), or [sendmsg(2)](https://man7.org/linux/man-pages/man2/sendmsg.2.html).  If _node_ is NULL, then the
network address will be set to the loopback interface address
(**INADDR_LOOPBACK** for IPv4 addresses, **IN6ADDR_LOOPBACK_INIT** for
IPv6 address); this is used by applications that intend to
communicate with peers running on the same host.

_service_ sets the port in each returned address structure.  If
this argument is a service name (see [services(5)](https://man7.org/linux/man-pages/man5/services.5.html)), it is
translated to the corresponding port number.  This argument can
also be specified as a decimal number, which is simply converted
to binary.  If _service_ is NULL, then the port number of the
returned socket addresses will be left uninitialized. 

#### If **AI_NUMERICSERV** is specified
in _hints.ai_flags_  and _service_ is not NULL,
then _service_ must point to a string containing a numeric
port number.  This flag is used to inhibit the invocation of a
name resolution service in cases where it is known not to be
required.

Either _node_ or _service_, but not both, may be NULL.

The **getaddrinfo**() function allocates and initializes a linked
list of _addrinfo_ structures, one for each network address that
matches _node_ and _service_, subject to any restrictions imposed by
_hints_, and returns a pointer to the start of the list in _res_.
The items in the linked list are linked by the _ai_next_ field.

There are several reasons why the linked list may have more than
one _addrinfo_ structure, including: the network host is
multihomed, accessible over multiple protocols (e.g., both
**AF_INET** and **AF_INET6**); or the same service is available from
multiple socket types (one **SOCK_STREAM** address and another
**SOCK_DGRAM** address, for example).  Normally, the application
should try using the addresses in the order in which they are
returned.  The sorting function used within **getaddrinfo**() is
defined in RFC 3484; the order can be tweaked for a particular
system by editing _/etc/gai.conf_ (available since glibc 2.5).

#### If **AI_CANONNAME** is specified
then the _ai_canonname_ field of the first of the _addrinfo_ structures in the
returned list is set to point to the official name of the host.

The remaining fields of each returned _addrinfo_ structure are
initialized as follows:

* The _ai_family_, _ai_socktype_, and _ai_protocol_ fields return the
socket creation parameters (i.e., these fields have the same
meaning as the corresponding arguments of [socket(2)](https://man7.org/linux/man-pages/man2/socket.2.html)).  For
example, _ai_family_ might return **AF_INET** or **AF_INET6**;
_ai_socktype_ might return **SOCK_DGRAM** or **SOCK_STREAM**; and
_ai_protocol_ returns the protocol for the socket.

* A pointer to the socket address is placed in the _ai_addr_ field,
and the length of the socket address, in bytes, is placed in
the _ai_addrlen_ field.

#### If **AI_ADDRCONFIG** is specified
then IPv4 addresses are returned in the list pointed to by _res_ only if the
local system has at least one IPv4 address configured, and IPv6
addresses are returned only if the local system has at least one
IPv6 address configured.  The loopback address is not considered
for this case as valid as a configured address.  This flag is
useful on, for example, IPv4-only systems, to ensure that
**getaddrinfo**() does not return IPv6 socket addresses that would
always fail in [connect(2)](https://man7.org/linux/man-pages/man2/connect.2.html) or [bind(2)](https://man7.org/linux/man-pages/man2/bind.2.html).

#### If _hints.ai_flags_ specifies the **AI_V4MAPPED** flag
, and _hints.ai_family_ was specified as **AF_INET6**, and no matching IPv6 addresses could be found
then return IPv4-mapped IPv6 addresses
in the list pointed to by _res_. 

#### If both **AI_V4MAPPED** and **AI_ALL** are specified
in _hints.ai_flags_
then return both IPv6 and IPv4-mapped IPv6 addresses in the list pointed to by _res_.  **AI_ALL**
is ignored if **AI_V4MAPPED** is not also specified.

The **freeaddrinfo**() function frees the memory that was allocated
for the dynamically allocated linked list _res_.

**Extensions to getaddrinfo() for Internationalized Domain Names**
Starting with glibc 2.3.4, **getaddrinfo**() has been extended to
selectively allow the incoming and outgoing hostnames to be
transparently converted to and from the Internationalized Domain
Name (IDN) format (see RFC 3490, _Internationalizing Domain Names_
_in Applications (IDNA)_).  Four new flags are defined:

#### **AI_IDN** If this flag is specified, 
then the node name given in
_node_ is converted to IDN format if necessary.  The source
encoding is that of the current locale.

If the input name contains non-ASCII characters, then the
IDN encoding is used.  Those parts of the node name
(delimited by dots) that contain non-ASCII characters are
encoded using ASCII Compatible Encoding (ACE) before being
passed to the name resolution functions.

**AI_CANONIDN**
After a successful name lookup, and if the **AI_CANONNAME**
flag was specified, **getaddrinfo**() will return the
canonical name of the node corresponding to the _addrinfo_
structure value passed back.  The return value is an exact
copy of the value returned by the name resolution
function.

If the name is encoded using ACE, then it will contain the
_xn--_ prefix for one or more components of the name.  To
convert these components into a readable form the
**AI_CANONIDN** flag can be passed in addition to
**AI_CANONNAME**.  The resulting string is encoded using the
current locale's encoding.

**AI_IDN_ALLOW_UNASSIGNED**, **AI_IDN_USE_STD3_ASCII_RULES**
Setting these flags will enable the IDNA_ALLOW_UNASSIGNED
(allow unassigned Unicode code points) and
IDNA_USE_STD3_ASCII_RULES (check output to make sure it is
a STD3 conforming hostname) flags respectively to be used
in the IDNA handling.