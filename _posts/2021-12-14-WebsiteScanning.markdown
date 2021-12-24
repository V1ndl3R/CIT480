Website Scanning

check the robots.txt file
http://<SITE>/robots.txt
This may give you clues to what you can scan or not scan. It should return something like this:
	User-agent: *
	Allow: /
	Disallow: /staff-portal
Next you can check the favicon it may be left over from the framework that may have been used to create the website.
Check the source code to view were the favicon.ico is located. You can then curl this icon and create the md5 Hash.
Then you can check the file hash vs the OWASP database located here:
	https://wiki.owasp.org/index.php/OWASP_favicon_database
You can also check the sitemap located at:
	http://<SITE>/sitemap.xml
This will list subpages that the developer wanted you to find, but there may be other clues located in this file.
You should also check the HTTP headers this may give you clues to the webserver software.
	curl http://<SITE> -v
Check for the comments at the bottom or in the source code that may let you know what if any framework created this page.
Once you find the framework you might be able to find a default login page and try the default login credentials 
or bruteforce it.

Below are some tools that may also help find the framework or system that is running the website.
	Google Dorking: https://en.wikipedia.org/wiki/Google_hacking
	Wappalyzer: https://www.wappalyzer.com/
	Wayback Machine: https://archive.org/web/
	
You can check to see if the website is hosted on a S3 bucket. If the address ends with http://s3.amazonaws.com/
there might be a misconfiguration that will allow you to access the website.

Below are tools that will allow you to Fuzz a website and find additional directories:
	ffuf: https://www.kali.org/tools/ffuf/
	dirb: https://www.kali.org/tools/dirb/
	wap: https://www.kali.org/tools/zaproxy/
	gobuster: https://www.kali.org/tools/gobuster/

This site will let you see when a site was registered and who created the website:
	crt.sh
This tool will brute force dns records dnsrecon the command is:
	dnsrecon -t brt -d <SITE>
This tool will enumerate subdomains by searching in different search engines:
	https://github.com/aboul3la/Sublist3r
The command is:
	./sublist3r.py -d <SITE>
