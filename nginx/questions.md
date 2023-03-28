# Questions

<details>

<summary>Maximum number of connections a server can hold</summary>

There is no upper limit on the number of connections a server can hold. It depends on the CPU and memory.&#x20;

</details>

<details>

<summary>Maximum number of connections a client can make to the server</summary>

You can make around 64000ish connections from one IP with source port to server. This is a limit because, in the transport layer(L4), the source port address is 16 bits, so `2^16` it is **65,536.** Excluding reserved ports, a client can make a maximum of 64000ish connections to the server. There is only one listener per port.

Again, the client can make 64000ish connections to the server when it has to connect to a different port of the server

[https://stackoverflow.com/questions/21253474/source-port-vs-destination-port](https://stackoverflow.com/questions/21253474/source-port-vs-destination-port)

![](<../.gitbook/assets/Screenshot 2023-03-28 at 8.42.29 PM.png>)

</details>

<details>

<summary>Layer 4 proxying causes a bottleneck to hold connections</summary>



</details>

<details>

<summary>Layer 4 and Layer 7 proxy usages</summary>



</details>

<details>

<summary>Pros and Cons of using HTTP network between the load balancer and app servers</summary>



</details>

<details>

<summary>How do ports help in scaling?</summary>



</details>

<details>

<summary>How does NGINX help with connection management?</summary>



</details>

<details>

<summary>What is the difference between an App server and a Web server?</summary>



</details>

<details>

<summary>Pros and Cons of Layer 4 proxying</summary>



</details>

<details>

<summary>Pros and Cons of Layer 7 proxying</summary>



</details>

<details>

<summary>How can I share the key with the client to maintain end-to-end encryption?</summary>



</details>

<details>

<summary>How does Nginx leverage event-driven model</summary>



</details>

<details>

<summary>TLS termination vs TLS passthrough</summary>



</details>

<details>

<summary>Why should I use HTTPS even on my backend when deployed in the cloud</summary>



</details>

<details>

<summary>Different ways to connect from Nginx to Backend servers with TLS</summary>



</details>

### Threading and connections

* Listener
* Acceptor
* Reader
* TCP Stream vs Requests
