이벤트 워커 그룹은 크게 두 종류로 나뉩니다. 

## Boss_group
첫번째는 보스 그룹으로, 이 그룹은 server type 워커로 이루어집니다. 
보스 그룹은 accept()를 위한 소켓을 바인드하고, 이로부터 클라이언트로부터 요청을 받아 후술할 차일드 그룹에 할당해줍니다.

보스 그룹에 워커가 추가되면 새로운 워커는 차일드 그룹의 소켓 정보는 모두 공유하지만, 각 보스가 bind()한 소켓의 정보는 알 필요가 없습니다. (실제로 모름)

## Child_group
두번째는 차일드 그룹입니다. 이 그룹은 stream type 워커로 이루어집니다. 
차일드 그룹은 보스에게 받아온 소켓 정보를 이용하여 read()와 write()를 실행합니다. 보스는 차일드를 적절한 루프에 등록시키며, 루프 속에서 필요에 따라 read(), write()를 실행합니다. 이는 kqueue나 epoll을 통해 구현되어 있으므로 효율적입니다.

There are two main types of event worker groups. 

## Boss_group
The first is the boss group, which consists of server type workers. 
The boss group binds a socket for accept(), which receives requests from clients and assigns them to the child groups described later.

When a worker is added to the boss group, the new worker shares all the socket information of the child group, but does not need to know which sockets each boss has bind() to. (It doesn't really know.)

## Child_group
The second is the child group, which is made up of stream type workers. 
The child group performs read() and write() using the socket information it receives from the boss. The boss puts the children in the appropriate loop, and they perform read() and write() as needed within the loop. This is implemented via kqueue or epoll, so it's efficient.
