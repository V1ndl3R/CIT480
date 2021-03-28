We will create a Wireguard VPN server on AWS lightsail, this only costs $3.50 a month.  One of the main benefits of this VPN is you do not have to open any ports on your home network.  The only port that has to be open is on the AWS instance.


You can select any linux distro that you like, I will be using Ubuntu 20.04 LTS, select OS only and select your distro.
Make sure you select the correct region, you can name it anything you like, all other settings can be default:

![VPN1](https://v1ndl3r.github.io/CIT480/assets/AWS-VPN1.png)


As the instance is spinning up, select the network tab and create a static IP.  Select your instance and attach the IP.


![VPN2](https://v1ndl3r.github.io/CIT480/assets/AWS-VPN2.png)

Go you for lightsail account page and download your SSH key.
Select your Instance and select Manage, go to the networking tab restrict your SSH in IPV4 delete the IPV6 rules.
Delete the Port 80 rules.  Then we are going to add a rule Custom UDP and pick a random high port for example 52368.
For added security you can restrict this to your IP and create rules for anyone connecting to you VPN.

Now connect using ssh and your downloaded key:
	ssh -i <PATHKEY> ubuntu@<PUBLICIP>

Replace <PATHEKEY> and <PUBLICIP> with your key and IP.  Run:
	sudo apt update
	sudo apt upgrade -y
	sudo apt install wireguard
 
Now we are going to generate our server keys:

	wg genkey | sudo tee /etc/wireguard/privatekey | wg pubkey | sudo tee /etc/wireguard/publickey

This will print out your Public Key you will need this for later. Now run this command to print your server private key:
	sudo cat /etc/wireguard/privatekey

Now we need to create the server config file:
	sudo nano /etc/wireguard/wg0.conf

	[Interface]
	Address = 10.0.0.1/24
	SaveConfig = true
	ListenPort = 51820
	PrivateKey = CAnaKiflpOHl8xlW6vQ2RUgNzVMcOMH68lLPonXMhAg
	PostUp = iptables -A FORWARD -i %i -j ACCEPT; iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE
	PostDown = iptables -D FORWARD -i %i -j ACCEPT; iptables -t nat -D POSTROUTING -o eth0 -j MASQUERADE
	
	[Peer]
	PublicKey = 
	AllowedIps = 10.0.0.2/32

You should add a Peer section for every computer you want to connect.
You can edit the address to any that you like, the ListenPort should be the same one we opened on AWS.  The PrivateKey is the one
we printed earlier. 

Now run:
	sudo ufw allow 51820
Replace the port with your port.

Enable IPV4 forwarding:
	sudo nano /etc/sysctl.conf
	sysctl -p

![VPN3](https://v1ndl3r.github.io/CIT480/assets/AWS-VPN3.png)

Run to start the wireguard and then enable it to run on startup:
	wg-quick up wg0
	sudo systemctl enable wg-quick@wg0

We can create client configurations:
	[Interface]
	PrivateKey = 
	Address = 
	DNS = 1.1.1.1
	
	[Peer]
	PublicKey = SERVER PUBLIC KEY
	AllowedIPs = 0.0.0.0/0
	Endpoint = SERVERIP:PORT
After you import this into a client machine you can connect to you new VPN and you are ready to go.
