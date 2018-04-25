- Non-blocking (Asynchronous) architecture: single thread is used to handle multiple requests. Single thread to handle all requests. Node applications are by default. Blocking (Synchronous): a new thread to serve another client. Another request have to wait or more hardware is needed.

- event queue

- Node is ideal for I/O-intensive apps.(apps need a lot of disks and network access) (should only be used in data intensive and real time applications) Do not use Node for CPU-intensive apps (video encoding, image manipulation service) (a lot of calculations should be done by CPU and a few operations that touch the file system or network)