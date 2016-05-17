---
layout: post
title: Install VPN on Raspberry Pi
description: 
headline: 
categories: personal
tags: 
  - raspberry pi
  - vpn
imagefeature: "raspberry-pi.jpg"
comments: true
mathjax: true
featured: false
published: true
---

I bought a Raspberry Pi B+ model with starter kit. It includes a case, which nicely fits the raspberry pi. It also contains a 8GB microsd card with NOOBS preinstalled. So I can skip installing NOOBS on microsd card. My purpose is to setup a vpn network at my home so that I can use it when I am outside. It is more secure than using public wifi network. 

<figure>
        <a href="{{ site.url }}/images/gallery1/b-plus.jpg"><img src="{{ site.url }}/images/gallery1/b-plus.jpg"></a>
</figure>



<section id="table-of-contents" class="toc">
  <header>
    <h1>Install Guildance</h1>
  </header>
<div id="drawer" markdown="1">
*  Auto generated table of contents
{:toc}
</div>
</section><!-- /#table-of-contents -->


## Install Raspbian and related softwares##
The first step is to install the operating system on raspberry pi. Plug in keyboard, mouse and microsd card, connect hdmi cable with monitor. After plug in the power, it will automatically start with several options. I choose to install the Raspbian operating system at the start up page. It will take about 20 mins to finish installing the operating system. The default login is the command line enviroment. To start the GUI, just type "startx" in the terminal.
Now we can access RPI(Raspberry Pi) remotely using ssh. In order to use remote desktop service from PC, we need to install xrdp in RPI, it will install the dependency tigervncserver as well.
{% highlight bash %}
sudo apt-get install xrdp (for remote desktop access) 
sudo update-rc.d xrdp enable (enable it at boot)
{% endhighlight %}
Since most of the home network use dynamic ip, we need to update our ip with the free dns domain name we get from some online provider. I choose the noip, I download linux version noip software (for dynamic dns service), use make and sudo make install to install the software. The last software to install is the openvpn.
  
## Network configuration ##
The ip address of RPI can be found using ifconfig command. If I am using my laptop remotely, I can use nmap to scan the available ip and find it (in my case, it is 192.168.0.8). 
{% highlight bash %}
nmap -sP 192.168.0.0/24
{% endhighlight %}
To make this internal ip static, first step is to configure the home router to make a dhcp reservation for my RPI ip address(i.e. reserve a internal ip for RPI). Then, change the interface file located in /etc/network/interfaces. Use ifconfig(ip address, netmask, broadcast address) and netstat -nr(network,gateway) to find all the information and put it there.
{% highlight bash %}
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
    address 192.168.0.8
    netmask 255.255.255.0
    network 192.168.0.0
    broadcast 192.168.0.255
    gateway 192.168.0.1
{% endhighlight %}
Now we have a fixed internal ip address to connect. However, if we want to connect to RPI outside home, we need has a static ip address. Unfortunately, my home ip is dynamic ip. After some search online, I found noip is a good choice to host the dynamic dns. It provided me a dynamic hostname. First, I registered a free dns hostname on noip website. Then I installed its linux version software Dynamic Update Client (noip2) on my RPI. With some simple configuration, it will update my dynamic ip to the dns server every 30s(you can change the value). Thus, when I ssh to my RPI remotely, I can use the registered dns hostname instead of the dynamic ip address. 


By default, Raspbian does not forward internet traffic. To enable it:
{% highlight bash %}
$ vi /etc/sysctl.conf
net.ipv4.ip_forward=1 (uncomment this line)
$ sysctl -p (configure kernel parameters at runtime, -p means reload)
{% endhighlight %}
RPI has a build-in firewall that will block incoming connections. We need open an hole for OpenVPN in the firewall. 
{% highlight bash %}
$ vi /etc/firewall-openvpn-rules.sh
#! /bin/sh
iptables -t nat -A POSTROUTING -s 10.20.30.0/24 -o eth0 -j SNAT --to-source 192.168.0.8
{% endhighlight %}
The first ip is the start ip that I chose for VPN subnet, the second is the internal ip of RPI. Next, we put it into the interfaces setup code so it runs on boot.
{% highlight bash %}
$ chmod 700 /etc/firewall-openvpn-rules.sh
$ vi /etc/network/interfaces
auto eth0
iface eth0 inet static
    pre-up /etc/firewall-openvpn-rules.sh(add this line)
{% endhighlight %}



## Configure OpenVPN server and client ##
There are two major steps. The first is to create the master certificate, server certificate, client certificate, and the private keys. Please follow the following two tutorials [rpi-vpn-tutorial](http://readwrite.com/2014/04/10/raspberry-pi-vpn-tutorial-server-secure-web-browsing/) and [openvpn-documentation](https://openvpn.net/index.php/open-source/documentation/howto.html). To create diffie-hellman key with size 2048, RPI will take about 3~4 hours to find a large prime number with 2048 bits. The easier way is to find such a key on your desktop or laptop and copy it onto RPI, this approach will be much faster. The dh pem file can be created by the following command
{% highlight bash %}
openssl dhparam -out dh2048.pem 2048
{% endhighlight %}
Actually, even 2048 bit is not secure enough nowadays. However, I just use it for myself. The most secure method is not to leak the domain name to other people. 
The second step is to write configuraion files for server and client. The tutorials mentioned above have the template available.


