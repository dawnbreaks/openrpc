Added by lubinwang
========
On client side:
==========
*  All request(direct or async) will be push to rpc_async_queue.
*  Direct caller thread will be waiting on a fd for notifing server response comming.
*  Client_thread aim to handle all network io operation
*  Writer_thread will handle all the pending request in rpc_async_queue, and send all request through the cient thread's ev_loop.


On server side
==========
* Dispacher thread accept all connections, and then use round robin alg to choose a worker thread to pass the new connection to it.
(push fd to worker.rpc_queue and write msg to worker.fd to wakeup that worker)
* Worker thread handle the actual rpc request, each of worker thread has it own ev_loop.


All communication between threads both on client side and server side are achieved by ev_loop
(each thread watch on a fd for message passed by other thread)
