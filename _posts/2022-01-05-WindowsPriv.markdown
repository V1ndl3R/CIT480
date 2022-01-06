For this task we will use Burp Suite to grab the packet then we will use hydra to brute force the login.
Burp suite is capible of brute forcing it but it would take a very long time.

You can find burp suite at this address if you do not have it:
	
	https://portswigger.net/burp

We are given the IP address of the target box: 10.10.50.31
The Kali box we are using has an IP of :       10.10.211.188

We know there is a webServer running but if we did not we could run a NMAP scan we also know it is a Windows so we must use -Pn flag:

	nmap -Pn 10.10.50.31

![Nmap](https://v1ndl3r.github.io/CIT480/assets/hakParkNmap.png "Nmap")

We can see there is a website running on the standard port 80 and RDP running.  You may be able to brute force both of these logins.
We will start with the website, putting the IP address into a brower we are greeted with a webpage if we poke around we can find a 
login page. If we could not find a login page we could also scan for directories with gobuster or dirbuster. We can also check robots.txt

![Login](https://v1ndl3r.github.io/CIT480/assets/hakParkLogin.png "Login")

	gobuster scan
	gobuster dir -u http://10.10.50.31/ -w /usr/share/directory-list-2.3-medium.txt

![Gobuster](https://v1ndl3r.github.io/CIT480/assets/hakParkGob.png "Gobuster")

Robots.txt does not give us much information

![Robots](https://v1ndl3r.github.io/CIT480/assets/hakParkRobots.png "Robots")

Now that we know there is a webpage and a login screen we will use Burp to capture the packet and get the required information for hydra:

![Packet](https://v1ndl3r.github.io/CIT480/assets/hakParkCapture.png "Packet")

We know we need to brute force this login and we know we need to use hydra this is the information we can use so far:

![Hydra1](https://v1ndl3r.github.io/CIT480/assets/hakParkHydra1.png "Hydra1")

But there is not alot of information to get the rest to work correctly. The correct command you will need to add the webpage where the 
login is located and add it after the http-post-form:

![Hydra2](https://v1ndl3r.github.io/CIT480/assets/hakParkHydra2.png "Hydra2")

This is still not enough information for the hydra to run correctly we will need to add more from the burp capture:

![Hydra3](https://v1ndl3r.github.io/CIT480/assets/hakParkHydra3.png "Hydra3")

You will need to copy the response and add it after the path to the login form with a : in between then at the end add failed status.
You can get that from burp responses as well:

![Hydra4](https://v1ndl3r.github.io/CIT480/assets/hakParkHydra4.png "Hydra4")

You can see that when the login fails you get a "200" response and the message login failed. Now you have the correct query you just need to tell hydra where to insert the username and password.
Replace the username with ^USER^ and password with ^PASS^ and you get the final query:

	hydra -l admin -P /usr/share/wordlists/rockyou.txt 10.10.50.31 http-post-form "/Account/login.aspx?ReturnURL=/admin/:__VIEWSTATE=2KDF2UOGOa8hb0xmx%2BTvjEbBg3hCJenmHN7xXrz9l9xx5BQ0lxkU5lvEREVspANAzpA%2FOSNr7o6gLUv7P%2FojooyocRY%2F9Y0VpLrNPqg3Tgy3VxIMFEEtSHyO9E%2BG7b0MVAHAlj2m%2FYazvXUK1jLWSoQm5gxPREN8SPVnIQG%2B%2BjGPdABh&__EVENTVALIDATION=Ydss8pagi3vLu3k%2B30ihYk9%2BsptmyJGUF%2FRPVohWEVB8E8oWh%2BcukV6unTK0jbmx5GpnXULRlVkzwFEdfL6AxoybWMqqNAhf8dtxptcsbG5sP8sgNoNo8WkrjpKA3AEilBfQ4s3XSfIWW2lHCgkecEdrEBZLpPzSKIJgKAC43x%2B7DRXx&ctl00%24MainContent%24LoginUser%24UserName=^USER^&ctl00%24MainContent%24LoginUser%24Password=^PASS^&ctl00%24MainContent%24LoginUser%24LoginButton=Log+in:F=Login Failed"

![Hydra5](https://v1ndl3r.github.io/CIT480/assets/hakParkHydra5.png "Hydra5")

Searching around the application we can find the name and version blogengine.net 3.3.6.0. Use searchsploit or exploit database archive to find a CVE.
	
	http://www.exploit-db.com/

Once you find the correct exploit in this case 46353 run this command to cp it.

	searchsploit -m 46353 /path/tocopyto/name.py

Once you have copied the exploit you can edit it and add your IP and listening port, then start an netcat listener:

	nc -lvnp 443

Make sure this listener port and the port in the exploit match.

You should now have a basic user shell on the webserver.
