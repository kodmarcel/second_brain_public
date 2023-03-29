---  
share: true  
tag: public  
---  
# SSH tunneling  
  
ssh -L 8080:server-hostname:80 remote-host  
  
Now if you point your web browser at http://localhost:8080/, you should see the contents of http://server-hostname/ as it would appear from the remote host.  
  
In OpenSSH, local port forwarding is configured using the -L option:  
  
ssh -L 80:intra.example.com:80 gw.example.com  
  
This example opens a connection to the gw.example.com jump server, and forwards any connection to port 80 on the local machine to port 80 on intra.example.com.  
  
By default, anyone (even on different machines) can connect to the specified port on the SSH client machine. However, this can be restricted to programs on the same host by supplying a bind address:  
  
ssh -L 127.0.0.1:80:intra.example.com:80 gw.example.com  
  
The LocalForward option in the OpenSSH client configuration file can be used to configure forwarding without having to specify it on command line. Remote Forwarding  
  
In OpenSSH, remote SSH port forwardings are specified using the -R option. For example:  
  
ssh -R 8080:localhost:80 public.example.com  
  
This allows anyone on the remote server to connect to TCP port 8080 on the remote server. The connection will then be tunneled back to the client host, and the client then makes a TCP connection to port 80 on localhost. Any other host name or IP address could be used instead of localhost to specify the host to connect to.  
  
This particular example would be useful for giving someone on the outside access to an internal web server. Or exposing an internal web application to the public Internet. This could be done by an employee working from home, or by an attacker.  
  
By default, OpenSSH only allows connecting to remote forwarded ports from the server host. However, the GatewayPorts option in the server configuration file sshd_config can be used to control this. The following alternatives are possible:  
  
GatewayPorts no  
  
This prevents connecting to forwarded ports from outside the server computer.  
  
GatewayPorts yes  
  
This allows anyone to connect to the forwarded ports. If the server is on the public Internet, anyone on the Internet can connect to the port.  
  
GatewayPorts clientspecified  
  
This means that the client can specify an IP address from which connections to the port are allowed. The syntax for this is:  
  
ssh -R 52.194.1.73:8080:localhost:80 host147.aws.example.com  
  
In this example, only connections from the IP address 52.194.1.73 to port 8080 are allowed.