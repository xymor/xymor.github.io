---
published: true
title: Comp Sci Basics - Http Request Life Cycle
layout: post
tags: [comsci, basic, http, web]
---
Between typing www.wikipedia.org in the browser and reading about the Unexpected Spanish Iquisition there's a lot of magic going on.

## DNS lookup
 First the computer has to make sense of the url, that is, translate it into a meaningful IP address where it connect and interact. The OS queries the nameserver for correct record and caches it locally so future queries won't need to hit the remote server.

## Estabilishing a connection
 With the IP at hand, the OS can estabilish a socket connection between the client machine and the remote server. The stream socket is the base for HTTP communication which is the application level procotol used by websites and is identified by the remote server IP, the service port(in this case the default 80), the local port opened and local network interface IP. These ports are binded and data written to one is relayed to the other.

## HTTP kicks in

###Request
 With the two way connection in place, the browser writes a message to the server:

{% highlight %}
GET / HTTP/1.1
Host: www.freebsd.org
User-Agent: Mozilla/5.0 (Windows; U; Windows NT 5.1; en-US; rv:1.7.7) Gecko/20050414 Firefox/1.0.3
Accept: text/html
Accept-Language: en-us,en;q=0.5
{% endhighlight %}

The first line tells the server the client is using http 1.1 for communication and using the GET verb on the root directory. The client also send several information using HTTP Headers, meta information exchanges by the two peers about the information. For instance, the Accept header tells the server the client knows how to understand HTML and the Accept-Language one says the content should be in english preferably.

### Response
The server will then reply with the index.html document sitting the root of the server by writting an HTTP response to the socket. Like the client, the server will respond with several metadata about the content it is streamming. One important point is the status code 200, http have several status codes about server availablity, erros, auth and even if the content replied is up to date or a stale copy.

{% highlight %}
HTTP/1.1 200 OK
Date: Fri, 13 May 2005 05:51:12 GMT
Server: Apache/1.3.x LaHonda (Unix)
Last-Modified: Fri, 13 May 2005 05:25:02 GMT
Content-Length: 33414
Keep-Alive: timeout=15, max=100
Connection: Keep-Alive
Content-Type: text/html
<!DOCTYPE html>
<html>
<img src="/spanish-inquisition.jpg"/>
</html>
{% endhighlight %}

Rendering
The browser reads the html payload and displays it using its rendering engine.

![](https://raw.githubusercontent.com/xymor/xymor.github.io/master/public/images/no_one_expects_the_spanish_inquisition_by_simzer-d5bxjqp.png)

