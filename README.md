High Level Approach:
For this project, we implemented the Raft protocal for the key-value store database. The general idea of Raft is to have a consensus understanding information changing way between servers and clients, followers and leaders. A Normal Raft include two parts: Voting and Log updating.

The program starts by the hello messages between the server and clients. The clients will then send put and get request to servers in our system. If the current leader is still unknown "FFFF". Each server will then add the commands to their own queue and will redirect them to their leader whenever they receive the append_entries from the leader; this means that the new leader is now elected.

A normal election will start if the server doesn't receive a heartbeat from the leader in its timeout time. They will send a request vote messages to all servers in this system. The servers that receive those messages will check the term and index of the sender and will decide if they want to vote for it. The server that receives the most votes becomes the leader and sends an append_entries to make all servers become followers. The new round starts from there.

In each append_rpc, the leader sends to the server, the leader would also include its previous log and previous term so that the server can check if the leader is stale, and if it wants the log entries that are farther before. Once the server receive the log it wants, it cuts off all the entries after that and append the log from the user to its own log. A log will only be committed if majority of the servers have that log. If the entry is committed, the command will then be excuted.

Challenges:
We faced many challenges during this assignment. The hardest challenge was to understand how election and log updating works. It took us some time to figure out how to make new elections and elect the right leader and making sure that all followers form a consensus on the new leader. We also had issues with resending failed messages and detecting those failed messages.

Testing:
We used the given tests provided in the configs files. We used print statments to keep track of the messages sent/received and revise the errors.
