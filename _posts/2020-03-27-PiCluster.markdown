This week I created I PI cluster so that I could test docker swarm and kubernetes.  The hardware I used for this project was 4 
raspberry pi zero W.  I installed the lastest raspian lite as you do not need desktop on zeros.  I used balenaEtcher to install all 
the OS software on the SD cards.  This is a very straight forward process just select the .iso image and the SD that you wish to 
write it to.  Once you have completed writing the image to the SD cards you will need to add a few files to the SD care before you
load for the first time.  You need to add ssh file to the boot drive, this can be completed with:
	touch D:/ssh
	
To be able to connect to the PI zeros, you need to add a file wpa_supplicant.conf add this:
	country = US
	ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
	update_config=1

	network={
	    ssid="NETWORK NAME"
            psk="Password"
	}
This will allow you to ssh into the PI's once they are online.  Once you are able to login to the raspberry pi zeros, I edited the 
host files to add the correct hostname and add the other nodes to the file:

![Hosts](https://v1ndl3r.github.io.CIT480/assets/cluster-hosts.png "Hosts File")

Once this is compeleted you need to assign static IP addresses for all of you nodes.  You will need to edit the 
/etc/network/interfaces to add the device as a static IP address

![Interface](https://v1ndl3r.github.io.CIT480/assets/cluster-static-1.png "Static-IP")

I was also able to configure my router to accept the static IP addresses.

![Router](https://v1ndl3r.github.io.CIT480/assests/cluster-router.png "router")

Once I was able to complete statically assigning IP addesses I went ahead and generated SSH files and shared them with all the 
machies so they would not need a password to log into.


![Router](https://v1ndl3r.github.io.CIT480/assets/cluster-rsa.png "rsa")


Once you are able to assign staic IP to all you nodes I was able to install docker swarm and attack all the nodes to the swarwm.

![Router](https://v1ndl3r.github.io.CIT480/assets/cluster-nodes.png "nodes")


Then you are able to see all of the nodes that are connected to the swarm
