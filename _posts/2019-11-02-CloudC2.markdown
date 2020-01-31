This week I setup a C2 Server on a home server that I could connect my Hak5 
devices to.  C2 was designed for deploying and managing Hak5 gear in the wild. It has a simple and straight forward web interface, an encrypted connection to devices with shell access and more from a single executable. It is self-hosted, which means you can host it almost anywhere. For example, many choose to host them on AWS or Azure, while others use their corporate networks. However, I wanted to host mine from home, on a linux server.

The first step in the setup process is to get an OS running to host your server.I plan to use a linux server running on an old laptop or possibly use an aws 
instance or even a Raspberry Pi.  Since this is still a work in progress I do not have much to report.

I was able to set this up on my localhost to play around with it a little bit 
but I want to install and run it on my own host.  This is used to connect and 
view all your Hak5 devices.  I have a few of these but have yet to play around 
with them all on the C2 instance.  

I am able to connect to them via ssh and download the files but hak5 released 
and cloud instance that allows you to view and manage all your files.  You can 
run this Cloud C2 on almost any type of server.
