---
layout: post
title: SSH Tunneling
---

SSH(Secure Shell) is a network protocol that creates a secure encrypted connection between client(local) and server(remote). SSH tunneling is like port forwarding over SSH, allowing secure connection for service ports from client(local) to server(remote) or vice versa.

It is mostly used to bind port on the client-side(local) to some port on the server-side(remote).

## Types of port forwarding

### Local port forwarding

In this case, a specified port on the ssh client side is bound to the specified port on the ssh server side. On the client-side, the ssh client is listening to the client configured port, and forward any traffic from this port to the ssh server configured port.


```
ssh -L 4000:127.0.0.1:3306 remote.server.com
```


In the above example, an ssh connection is made to remote.server.com, and port 4000 on the client-side(local machine) is bound to port 3306 and host 127.0.0.1 on server-side(remote). If on the remote side MySQL is running on port 3306 on host 127.0.0.1, then can be accessed from port 4000 on client-side. Since we have not specified the host on the client-side, anyone who has access to the client can access to the server port 3306 host 127.0.0.1. We can restrict this by adding a host on the client-side.

```
ssh -L localhost:4000:127.0.0.1:3306 remote.server.com
```

Now, all the traffic from client localhost port 4000 is forwarded to 127.0.0.1 port 3306.

```
ssh -L [local bind address]:[local bind port]:[remote bind address]:[remote bind port] [remote address]
```

Remote port forwarding
In this case, a specified port on the ssh server-side(remote) is bound to ssh client-side(local). On the server-side(remote), the ssh server is listening to the configured port, and forward any traffic from this port to ssh client configured port.

```
ssh -R example.com:8080:localhost:80 remote.server.com
```

In the above example, an ssh connection is made to remote.server.com, and port 8080 with host example.com on server-side(remote) is bound to port 80 with host localhost on client-side(local).

```
ssh -R :[remote bind address]:[remote bind port]:[local bind address]:[local bind port] [remote address]
```