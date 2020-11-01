[![Maven Central](https://maven-badges.herokuapp.com/maven-central/jitsi/jsocks/badge.svg)](https://search.maven.org/artifact/jitsi/jsocks)
[![Javadocs](http://javadoc.io/badge/jitsi/jsocks.svg)](http://javadoc.io/doc/jitsi/jsocks)


# JAVA SOCKS Server
It is a SOCKS server written entirely in Java, which supports both SOCKS4 and SOCKS5 protocols. This software is distributed under GNU Lesser General Public License, meaning that both binary and source code are freely available and can be modified an distributed.
I would not bother you with long list of things I'm not responsible for. Let me just say, that you are using this program on your own risk, and it is not me to blame if anything doesn't work as you expected. I tried my best, but it is up to you to check if it works as you wish it to, the source code is there, so you can correct whatever you don't like.

## Update Information
Please visit the JSocks Project Page for latest updates. The CVS update log should be most informative.
Latest packaged version is 1.01. Proxy have been rewised and there are some changes to the Socks Library. New features have been added to the proxy server itself, well at least one
Now it is possible to use this proxy from behind another proxy.
Also proxy chaining is introduced, it allows you to configure the proxy to connect through a series of proxies before reaching the desired host: proxy1-> proxy2->...proxyN->desired_host. It is a strange feature but might be useful in some situations.
Some bug fixes have been done, it is now possible to use ICQ with this proxy server.

## What this Server is good for?
Well, it is a not a commercial proxy server. It does not have plenty of features like address caching. Authentication scheme is rather simplistic, but can be extended, if you know how to program in Java. It is java application after all, which gives platform independence but at the cost of performance. But it is simple to install and use.
It is assumed that the socks library itself is more useful to most developers, rather than a simple server which uses the library. If you are a developer and want your applications to have support for SOCKSv5 protocol, you might find useful visiting Socks Library page.

## SocksEcho
SocksEcho is another application which uses socks package. It is GUI echo client, which is SOCKS aware, you can make and accept connections through the proxy using this client. You can also send datagrams through SOCKS5 proxy. I have used it a lot for testing. This application is also included.

## Requirements
Java 1.8
 
## Acknowledgments
I would like to thank people at SourceForge for the great services they provide to open source community.


SOCKS Library
-------------
This page contains information that might be interesting for developers, who wish to use SOCKS protocol in applications they are developing, both client and server side.

## Why to use it
There are plenty of reasons for which you might want to use SOCKS library in your java application. They are generally divided in two parts
1. You are developing a client application, which needs to access proxy.
2. You are developing a custom Proxy server.

## Client Application
Current version of java has a support for SOCKSv4 proxy, which is probably enough for most applications, which need to do some networking. Connections are being done through the proxy or directly depending on the user configurations, transparently to the java application. But SOCKSv4 has some limitations:

1. Lack of sufficient authentication.
The only authentication SOCKSv4 supports is the authentication based on Ident protocol. Basically client tells the server who he is, and server verifies it with the identd daemon running on the client machine. This technique works fine when proxy is used to let people on local network have access to the Internet. But it is not suitable when proxy is used to let people from the outside in.

2. Lack of UDP support.
SOCKSv4 protocol does not have any UDP support. And currently with almost all multimedia applications using UDP this might be a serious disadvantage.
Besides implementation of the SOCKSv4 in Java appears to be not complete (probably I'm wrong, check with sun). It appears to me that there is no way to accept a connection from the outside Firewall using Java1.2 ServerSocket.

So if you need your application to be able to
1. Send and receive datagrams through the firewall.
2. Accept connections from hosts behind the firewall.
3. Provide non-trivial authentication to the proxy server.
4. Ensure secure connection to the proxy server.

you might find that you need SOCKSv5 support, and hence this library may be useful to you. Even though I have forced the advantages of SOCKSv5 protocol, this library supports SOCKSv4 as well.

Hopefully one day Java will support SOCKSv5 as well, but it's not yet happened.

## Server Application
If you are developing proxy server which need to support either SOCKSv4 or SOCKSv5 or both, you'll find using this library very time saving. There are plenty of things to take care about when developing proxy server, protocol handling is just one part of the problem, which have been solved by this library, so that you can concentrate on authentication, authorization and initialization.
There are generally two major reasons for which proxy servers are used: to let people in, or to let them out, or both. Proxy server is like a door in the Firewall. Usually you do not care all that much who gets out, but you should be very careful in deciding who gets in.

SOCKSv5 protocol provides for extendable authentication schemes, which might be standard or private. And this socks library makes it easy to use your own implementations of authentication methods. Next step after authentication is authorization, for which methods are also provided.

## How to use
Now as you are convinced in the fact that you'll need to use socks library. Its time to know how to do so.
How to page will cover these issues.
I have just finished redesign and testing. There have been major changes to the library, mostly due to poor design decisions in the first stage. Few things that have been changed:

- It is now possible to connect through unlimited number of proxies, rather then just one. That is it is now possible to use proxyA to connect to proxyB to connect to ... proxyZ to connect to desired host.
- I have previously overlooked UDP handling. It was not possible to perform authentication specific transformations to UDP data. Now this problem have been removed.
- Few convenience features have been added.
- Some bugs have been fixed.
- Some restructuring have been done, to yield more convenient package structure.
- How to page is still yet to come. I haven't had time recently. As for now, read the documentation pages, they are now available online.
