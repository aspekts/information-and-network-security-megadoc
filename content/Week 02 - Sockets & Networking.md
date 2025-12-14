| Term                                     | Definition                                                                                                                                                                                                                         | Exam Context/Example                                                                                                                                                                                        |
| :--------------------------------------- | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Secure Sockets Layer (SSL)**           | A communication protocol (or set of rules) used to create a secure connection between two devices or applications on a network. It is an older technology that contains known security flaws. Stands for **Secure Sockets Layer**. | Although all versions are deprecated, the term _SSL_ or _SSL/TLS_ is still commonly used to refer to the **TLS protocol** and TLS certificates.                                                             |
| **Transport Layer Security (TLS)**       | The upgraded version of SSL that resolves existing SSL vulnerabilities. It authenticates more efficiently and continues to support encrypted communication channels. Stands for **Transport Layer Security**.                      | TLS 1.2 and 1.3 are actively used. AWS clients must support TLS 1.2 or later by June 2023, as earlier TLS versions (1.0 and 1.1) were formally deprecated in 2021.                                          |
| **Communication Protocol**               | A set of rules that defines how two devices or applications exchange data securely. Both SSL and TLS are examples of these protocols.                                                                                              | SSL and TLS protocols authenticate two parties connected over a network so they can exchange data securely.                                                                                                 |
| **Sockets (Developer Viewpoint)**        | An API provided by the operating system to send and receive data over the network between software running on different devices, or sometimes on the same machine. They are an abstraction of network facilities.                  | For developers, handling secure sockets can be challenging due to network-dependent issues like transmission delays requiring buffers and complicated debugging.                                            |
| **Sockets (Network Viewpoint/Endpoint)** | The end points of a data transmission between software running on computers, identified by an address (usually IP) and a port number. To the network, they correspond to packets being transmitted.                                | Whether a socket is secured with TLS/SSL has no impact on the network, outside of the network devices being unable to inspect the data transmitted.                                                         |
| **Sockets (Operating System Viewpoint)** | The end points corresponding to low-level system calls related to network card(s), managed internally by the kernel similarly to file descriptors.                                                                                 | When data is received by the network card driver, the OS makes the data available in the corresponding socket based on the port number.                                                                     |
| **HTTP**                                 | A protocol or set of communication rules for client-server communication over any network.                                                                                                                                         | **HTTPS** is the secure version, established by layering SSL/TLS over HTTP.                                                                                                                                 |
| **HTTPS**                                | The practice of establishing a secure SSL/TLS protocol on an insecure HTTP connection. The additional 's' stands for 'secure'.                                                                                                     | To verify a secure connection, a browser checks for `https://` in the address bar, indicating a connection secured by a TLS or SSL certificate.                                                             |
| **Handshake (SSL/TLS)**                  | A process in which a browser authenticates a server’s SSL or TLS certificate. This process authenticates both parties and exchanges cryptographic keys.                                                                            | An **SSL handshake** was explicit and complex, while a **TLS handshake** is implicit, has fewer steps, and results in a faster connection.                                                                  |
| **Alert messages**                       | Mechanisms used by SSL and TLS protocols to communicate errors and warnings.                                                                                                                                                       | **SSL** alerts are unencrypted and only include `warning` and `fatal` types. **TLS** alerts are encrypted and include an additional `close notify` alert to signal the end of the session.                  |
| **Message authentication codes (MACs)**  | A cryptographic technique used by both SSL and TLS for verifying the authenticity and integrity of messages. A fixed-length code generated using a secret key and attached to the original message.                                | The SSL protocol used the now-outdated MD5 algorithm for MAC generation, whereas TLS uses **HMAC** (Hash-Based Message Authentication Code) for enhanced security.                                          |
| **Cipher suite**                         | A collection of algorithms that create keys to encrypt information between a browser and a server.                                                                                                                                 | A cipher suite typically encompasses a key exchange algorithm, a validation algorithm, a bulk encryption algorithm, and a MAC algorithm. TLS upgraded several algorithms from SSL due to security concerns. |
| **TLS/SSL Certificates**                 | Digital certificates used to facilitate the handshake process and establish encrypted communications between a browser and a web server. They indicate that a server adheres to current security standards.                        | When setting up a secure server, the developer must load the certificate and keys into the SSL/TLS context. Although often called SSL certificates, they are the industry standard **TLS certificates**.    |
| **AWS Certificate Manager (ACM)**        | An AWS service offered to help users meet SSL/TLS requirements. It provisions, manages, and deploys public and private SSL/TLS certificates.                                                                                       | ACM can be used to protect internal resources and maintain SSL/TLS certificates through automated management, including certificate renewals.                                                               |
## Difference between SSL and TLS

**Transport Layer Security (TLS)** is the direct successor and upgraded version of **Secure Sockets Layer (SSL)**, developed specifically to resolve the security vulnerabilities found in SSL,. All versions of the older SSL protocol are now deprecated, while TLS versions 1.2 and 1.3 are actively used,.

The key operational and security differences between the two protocols include:

### Handshake Process

- The **SSL handshake** was described as an **explicit connection** and was complex and slow because it involved more steps,.
- The **TLS handshake** is an **implicit connection**, speeding up the process by having fewer steps and reducing the total number of cipher suites involved,.

### Alert Messages

- **SSL** alert messages are **unencrypted** and limited to only two types: `warning` and `fatal`,.
- **TLS** alert messages are **encrypted** for additional security and include an extra alert type called `close notify`, which signals the end of the session,.

### Message Authentication and Encryption

- Both protocols use Message Authentication Codes (MACs) for verifying message authenticity and integrity. However, **SSL** uses the **outdated MD5 algorithm** for MAC generation.
- **TLS** uses **HMAC** (Hash-Based Message Authentication Code) for more complex cryptography and enhanced security,.
- Regarding **cipher suites** (collections of algorithms used to create encryption keys), **SSL** supports older algorithms that have known security vulnerabilities, while **TLS** uses advanced encryption algorithms,.

### Version History and Certificates

- SSL moved through versions 1.0, 2.0, and 3.0 before being replaced. TLS has progressed through versions 1.0, 1.1, 1.2, and 1.3.
- Though all SSL certificates are no longer in use and **TLS certificates** are the current industry standard, the term _SSL_ or _SSL/TLS_ is still commonly used to refer to the TLS protocol and its certificates,.

## Steps to use Secure Sockets
The sources outline the sequence of steps for using **secure sockets** (SSL/TLS), which behave similarly to standard TCP sockets but include additional security steps.

The sequence of function calls (steps) for the client and server processes are outlined below:

### Client Connection Sequence

The client follows these six steps to establish and terminate a secure connection:

1. **Create a socket object/structure**.
2. **Create a SSL/TLS context**.
3. **Wrap the socket in the SSL/TLS context**.
4. **Connect the wrapped socket to IP:port**.
5. **Loop sending/receiving data with the server**.
6. **Close the connection**.

### Server Connection Sequence

The server sequence involves setup steps for the main server socket, followed by iterative steps for handling individual clients, and finally, a cleanup step for the server socket:

**Server Setup and Listening Phase:**

1. **Create a socket object/structure**.
2. **Bind the socket to an IP:port**.
3. **Listen for new connection**.
4. **Create a SSL/TLS context**.
5. **Load certificate and keys in the SSL/TLS context**.
6. **Loop accepting new client connections**.

**Handling Individual Client Connections (Inside the Loop):**

1. **Get the client socket**.
2. **Wrap the client socket in the SSL/TLS context**.
3. **Loop sending/receiving data with that client**.
4. **Close this client connection**.

**Server Cleanup:**

7. **Close the server socket**.