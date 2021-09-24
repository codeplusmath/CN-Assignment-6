# CN-Assignment-6
### Implement an application level RDT protocol.

Your program will have a client and a server part, both using UDP sockets and then additional RDT layer on top of it.  The server is basically going to do an addition of specified numbers. This is how the communication will take place:

```
Client: 3 
Server: 3 + ACK 
Client: 4 5 9 + ACK 
Server: 18  + ACK
```

The first message from client is the number of numbers(3 here), the server echoes the same back in second message; then client sends the numbers (3 RANDOM nos: 4 5 9 in this case), and server sends their sum back. The client verifies that the sum is correct by locally computing it and verifying it.
Since both client and server are going to run on 127.0.0.1, there is no chance of packets getting dropped; hence we will 'simulate' the packets getting dropped.

Packets dropped simulation:
The program will have a function called udtsend() which will accept a packet and send it with a probability as command line argument. Not sending the packet will be equivalent to the packet getting dropped.

Both the programs will use a timer to detect a packet drop (actually packet that was never sent by other side) and then resend packets.

You need to take care of the following: duplicate packets, duplicate ACKS, sequence numbers. Design the application header properly.Each message from the client and server should carry an identifier also (same identifier for the 4 messages), to distinguish between different connections.

Your code should clearly modularise the functions 
```
udtsend()
rdtsend()
udtrecv()
rdtrecv().
```
Every packet drop, timeout and retransmit should be printed one each side.

Filenames: client.py server.py library.by (the library.py can include the common code used by client and server both)

For example: The programs will run like this: 

```
$ python3 ./client.py 0.4

Dropped Packet 2, ID: 123123

Retransmitted Packet 2, ID: 123123

$ python3 ./server.py 0.75

Timeout: Packet 2: ID 123123
```

Where the second argument is the probability of dropping packets.
