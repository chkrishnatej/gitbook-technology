# Questions

<details>

<summary>Maximum number of connections a server can hold</summary>

There is no upper limit on the number of connections a server can hold. It depends on the CPU and memory.

</details>

<details>

<summary>Maximum number of connections a client can make to the server</summary>

You can make around 64000ish connections from one IP with source port to server. This is a limit because, in the transport layer(L4), the source port address is 16 bits, so `2^16` is **65,536.** Excluding reserved ports, a client can make a maximum of 64000ish connections to the server.

[https://stackoverflow.com/questions/21253474/source-port-vs-destination-port](https://stackoverflow.com/questions/21253474/source-port-vs-destination-port)

![](<../.gitbook/assets/Screenshot 2023-03-28 at 8.42.29 PM.png>)

</details>

* What is a connection?
* How does NGINX help with connection management?
* What is the difference between an App server and a Web server?
* How do ports help in scaling?
* Pros and Cons of using HTTP network between the load balancer and app servers
* Layer 4 and Layer 7 proxy usages
* Risks of Layer 4 proxying
* How can I share the key with the client to maintain end-to-end encryption?
* Why should I use HTTPS even on my backend when deployed in the cloud
* Different ways to connect from Nginx to Backend servers with TLS
* TLS termination vs TLS passthrough
* How does Nginx leverage event-driven model

### Threading and connections

* Listener
* Acceptor
* Reader
* TCP Stream vs Requests
