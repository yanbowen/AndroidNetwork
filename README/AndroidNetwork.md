# 深入理解Android网络编程  

## 第一章 ：网络编程概要  

Uir.parse()//方法返回一个URL类型，Intent.ACTION\_VIEW调用系统浏览器打开指定网页  
  
        Uri uri = Uri.parse("http://translate.google.cn/");
        Intent intent = new Intent(Intent.ACTION_VIEW, uri);
        startActivity(intent);
<center>![](http://i.imgur.com/oc7Kw19.jpg)</center>  

        WebView webView = (WebView) findViewById(R.id.webView1);
        webView.loadUrl("http://www.baidu.com/");
        webView.setWebViewClient(new WebViewClient() {
            public boolean shouldOverrideUrlLoading(WebView view, String request) {
                view.loadUrl(request);
                return true;
            }
        });  
  

## 第二章 ：Android基本网络技术和编程实践  

<center>![](http://i.imgur.com/cAnFGTq.jpg)</center>  
OSI/RM模型相对过于复杂，显示中广泛应用的是TCP/IP模型。TCP/IP是一个协议集，是由ARPA于1977年推出的。 
 
* 应用层：多数与网络相关的程序为了通过网络与其他程序通信所使用的层。在应用层中，数据以应用内部使用的格式进行传送，然后被编码成标准协议的格式。重要的例子如万维网使用HTTP协议、文件传输使用的FTP协议、接收电子邮件使用的POP3和IMAP协议、发送邮件使用的SMTP协议，以及远程登录使用的SSH和Telnet等。
* 传输层：传输层响应来自应用层的服务请求，并向网络层发出服务请求。传输层提供两台主机之间透明的数据传输，通常用于端到端连接、流量控制或错误恢复。这一层最重要的两个协议是TCP和UDP。
* 网络层：网络层提供端到端的数据包交付，换言之，它负责数据包从源发送到目的地，任务包括网络路由、差错控制和IP编址等。这一层重要的协议有IP4/6、ICMP（控制报文协议）和IPSec（协议安全）
* 网络接口层：是TCP/IP参考模型的最底层，负责通过网络发送和接收IP数据报；
一个应用层应用一般都会使用到两个传输层协议之一：面向连接的TCP传输控制协议和面向无连接的UDP用户数据报协议。  

### 使用TCP通信步骤  

TCP建立连接后，通信双方可以同时进行数据传输。  

##### TCP服务器端主要步骤如下：  
  
* 1.调用ServerSocket(int port)创建一个ServerSocket,并绑定到指定端口上。  
* 2.调用accept(),监听连接请求，如果客户端请求连接，则接受连接，返回通信套接字。
* 3.调用Socket类的getOutputStream()和getInputStream()获取输出和输入流，开始网络数据的发送和接收。
* 4.关闭通信套接字   

##### TCP客户端工作的主要步骤：  
 
* 1.调用Socket()创建一个流套接字，并连接到服务器端。  
* 2.调用Socket类的getOutputStream()和getInputStream()方法获取输出和输入流，开始网络数据的发送和接收。  
* 3.关闭通信套接字。  

### 使用TCP通信步骤  

UDP有不提供数据报分组、组装和不能对数据包排序的缺点，也就是说，当报文发送之后，是无法得知其是否安全完整到达的。   

##### UDP服务端工作的主要步骤：   
* 1.调用DatagramSocket(int port)创建一个数据报套接字，并绑定到指定端口上。  
* 2.调用DatagramPacket(byte[]buf,int length),建立一个字节数组以接收UDP包。  
* 3.调用DatagramSocket类的receive()，接收UDP包  
* 4.关闭数据报套接字

##### UDP客户端主要步骤：  

* 1.调用DatagramSocket()创建一个数据包套接字。  
* 2.调用DatagramPacket(byte[]buf,int offset,int length,InetAddress address,int port),建立要发送的UDP包。  
* 3.调用DatagramSocket类的send()发送UDP包。  
* 4.关闭数据报套接字。  

## 第三章 ：Android基本Web技术  

