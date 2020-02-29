This week I am going to go over the steps needed to create your own Certificate Authority and self sign certificates using openssl.

The first step that you need to do is install an Ubuntu Server edition(or any distro that you like).

Once the install is compplete run:
	apt-get update
	apt-get upgrade -y

Once your server is completly updated and upgraded you will need to install a few packages.
	apt-get openvpn
	apt-get openssl  (Only if you do not have it)
		
Open the openssl configuration file that is located at
	 /usr/lib/ssl/openssl.cnf

Under the section [ CA_default ] the first line should be dir = ./demoCA. 
Change this line to /root/ca(or where ever you would like your CA to live).

Take note of the file structure in this section, it will make the next section make sense.
There are a lot of options that are in this configuration file.  Save and close the file.

Now make the directory that you just named for dir in the config file.

	mkdir /root/ca && cd /root/ca
	mkdir certs crl newcerts private request
	touch index.txt && echo '01' > serial

These there commands will setup the file structure that is needed for your CA.
The next command will generate your CA private key make sure you remember the options that you select,
you will need them for your other certificates.

	openssl genrsa -aes256 -out private/cakey.pem 4096

Make sure you select a strong password for this private key.

	openssl req -new -x509 -key /root/ca/private/cakey.pem -out cacert.pem -days 3650

This will sign your CA with the key we just created and it will be valid for 10 years.
It is a good idea to run:
	chmod 600 -R /root/ca
for security reasons.

You now have a fully working self-signing certificate, now lets generate a certificate for a VPN server.

	cd request
	openssl genrsa -out server.pem 2048
	openssl req -new -key server.pem -out server.csr
	openssl ca -in server.csr -out server.crt

We are going to move the server.pem, private key and the server.crt public key to /etc/openvpn/server.
These can be used later to create a OpenVPN Server.

Instead of having to type all of those commands lets create a bash script to do the leg work for us.

	nano gencerts.sh
#!/bin/sh
useradd $1
openssl genrsa -out $1.pem 2048
openssl req -new -key $1.pem -out $1.csr \
-subj "/C=US/ST=California/L=Northridge/O=California State University Northridge/OU=Advancing Tech Lab/CN=$1"
openssl ca -in $1.csr -out $1.crt



This will add a user that is provided when the script is called and generate all the certs needed.

	




