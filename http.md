> From [this link](https://code.tutsplus.com/tutorials/http-the-protocol-every-web-developer-must-know-part-1--net-31177)

HTTP stands for Hypertext Transfer Protocol. It's a stateless, application-layer protocol for communicating between distributed systems, and is the foundation of the modern web.

## HTTP Basics

HTTP allows for communication between a variety of hosts and clients, and supports a mixture of network configurations.

The communication usually takes place over TCP/IP, but any reliable transport can be used. The default port for TCP/IP is 80, but other ports can also be used.

- Custom headers can also be created and sent by the client.

HTTP/1.1 adds a few extra features to the previous 1.0 version. These includes *persistent connections, chunked transfer-coding* and *fine-grained caching headers*.

### URLs

At the heart of web communications is the request message, which are sent via Uniform Resource Locators (URLs). URLs have a simple structure that consists of the following components:

![http_url](images/http-url.png)

The protocol is typically `http`, but it can also be https for secure communications. The default port is `80`, but one can be set explicitly, as illustrated in the above image. The resource path is the *local path* to the resource on the server.

### Verbs