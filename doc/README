openrpc is an open rpc framework,support sync and async call.

the event loop based on libev.

openrpc can use for commerical.

3q for libev/memcached/glib and my team amigo.

please report bug to me,3q.

author:yanghu
mail:believe3301@gmail.com


On client side:
1. All request(direct or async) will be push to rpc_async_queue.
2 direct caller thread will be waiting on a fd for notifing server response comming.
3. client thread aim to handle all network io operation
4. client writer thread will handle all the pending request in rpc_async_queue, and send all request through the cient thread's ev_loop.


On server side
1. Dispacher thread accept all connections, and then use round robin alg to choose a worker thread to pass the new connection to it.
(push fd to rpc_queue and write msg to worker.fd to notify worker)
2. Worker thread handle the actual rpc request, each of worker thread has it own ev_loop.


All communication between threads both on client side and server side are achieved by ev_loop
(each thread watch on a fd for message passed by other thread)


