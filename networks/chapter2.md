# Application Layer

* when developing a web application there are two popular architecture:
    * client-server architecture
    * peer 2 peer architecture
* the process the initiates the communication is called the client
* the process that waits to be contacted to begin the session is the server
* A process sends messages into, and receives messages from the network through a software interface 
  called a **socket**
* in order for a message to get to a process two pieces of information is required:
    * the address of the host -> **IP address**
    * something to identify the process on that host -> **port number**
* many networks including the internet provide more than one transport layer protocol
* when you develop an application you must choose one of the available transport layer protocol
* the services that a transport layer protocol can offer to the application invoking it have four dimensions:
    1. reliable data transfer
    2. throughput
    3. timing
    4. security
* if the transport protocol that you are using don't provide reliable data transfer this means that some data 
  that you send could never reach the receiving process
  
* throughput is the rate at which the sending process can send bits to the receiving process
* a transport layer protocol can guarantee the throughput given to a process. So a process can ask 
  for a specific throughput (r bits/sec)
* applications that have specific throughput requirements are said to be **bandwidth-sensitive application**
* **elastic application** is the opposite of bandwidth-sensitive application

* an example of timing service provided by transport layer might be that every bit that the sender pumps 
  into the socket arrives at the receiver's socket no more than 100 msec later
  
* in security service the transport layer could encrypt the sending messages and decrypt the receiving messages

* the internet provides two protocols:
    * TCP
    * UDP

* TCP Services: includes a connection-oriented service and a reliable data transfer service
* neither TCP or UDP provide security service
* an enhancement for TCP SSL was developed to provide security
* the SSL is not a separate protocol
* if an application wants to use SSL it has to include the code in the server and the client side
* typically you send a message through SSL which then gets encrypted and goes through TCP socket 
  
* UDP is connection-less and provides unreliable data transfer service


* **Application-layer protocol** defines how an application's processes, running on different end systems, 
  pass messages to each other
* Application layer protocol defines:
    * the types of messages exchanged(request message, response messages)
    * the syntax of various message types
    * the semantics of the fields (the meaning of it)
    * rules of when and how a process sends messages and responds to messages

# HTTP 

* HTTP is an Application protocol
* in HTTP the client is usually the browser and the host-server is the web server such as tomcat or apache
* web pages consists of objects: HTML file, JPEG image, java applet, video clip ...
* objects are addressable by a single URL
* two types of connections: persistant and non-persistant connection

* non-persistent HTTP uses a new TCP connection for every request it makes
* persisten HTTP keeps the connection open for multiple requests

* HTTP Message Format: 
    GET /somedir/page.html HTTP/1.1
    Host: www.adek.com
    Connection: close
    User-agent: Mozilla/5.0
    Accept-language: ar
  
* HTTP Request Properties:
    1. it is written in ASCII text
    2. every line is followd by a carriage return and a line feed
    3. the first line is called **request line** and the rest are called **header lines**
    4. after the header lines there is an extra line containing a carriage return an a line feed
    5. then after that there is an **entity body** which is empty with the GET request

* connection: close → tells the server to close the connection after the request

* HTTP Response Format:
    HTTP/1.1 200 OK
    Connection: close
    Date: Tue, 18 Aug 2015 15:44:04 GMT
    Server: Apache/2.2.3 (CentOS)
    Last-Modified: Tue, 18 Aug 2015 15:11:03 GMT
    Content-Length: 6821
    Content-Type: text/html
    
    (data data ...)
    
* the first line is called the **status line** then followed by **six headers lines** and then the entity body

## Cookies
* HTTP servers are stateless which means every request you make is a new request for the server
* cookies allow servers to keep track of users
* cookie technology has four components:
    1. cookie header line in the http response message
    2. cookie header line in the http request message
    3. cookie file kept on the user end-system and managed by the user's browser
    4. back end database at the web site 
       
* cookie usage example:
    * the user contacts the website for the first time
    * the server creates an identification number and creates an entry in the back-end database 
      that is indexed by the identification number
    * then the server include in the http response message the Set-cookie: header line which contains the id
      for example Set-cookie: 15035
    * when the browser sees this header line it appends a line to the special cookie file that it manages. 
      this line includes the hostname of the server and the identification number
    * now every time the user sends a request to that host again the browser will look up the cookie file and 
      put the identification number in the header line Cookie
      for example Cookie: 15035

## Web Caching

* A web-cache also called a proxy-server is a network entity that satisfies the HTTP request 
  on the behalf of the original web server
  
* the web-cache has its own disk storage and keeps copies of recently requested objects in this storage
* user's browser can be configured so that all of the user's HTTP requests are are first directed to the web-cache

* when a user request a somthing from the server
    1. the borwser establish a TCP connection to the web cache and request for the object
    2. if the web cache has the object it sends the response to the user
    3. if the web cache doesn't have the object it opens a TCP connection with the original server 
       and sends an HTTP request then the original server sends the object back in a response
    4. when the web cache recieves the request it stores a copy and sends a copy in a response to the web browser
* typically the web cache is purchased and installed by ISP
* since the copy at the cache might get outdated when a browser sends a request to the cache the 
  cache sends a conditional GET to the original server to check if the main copy has been modified
  
  


