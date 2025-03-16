How to Install Metasploit on Kali Linux
This week, I’m diving into how to set up Metasploit, one of the most widely used penetration testing frameworks, on Kali Linux. If you’re using Kali, Metasploit is pre-installed, but I’ll also cover how to ensure it’s the latest version and troubleshoot installation issues. Let’s get started!

Step 1: Check for Pre-Installed Metasploit
Kali Linux often comes with Metasploit Framework pre-installed. To verify, open your terminal and type:

bash
msfconsole
If Metasploit starts successfully, you’re ready to go! If not, or if you’d like to ensure you have the latest version, proceed to the next step.

Step 2: Update Your System
Keeping your system up-to-date minimizes compatibility issues. Run the following commands:

bash
sudo apt update
sudo apt upgrade -y
These commands ensure your repositories and installed packages are current.

Step 3: Install or Reinstall Metasploit
If Metasploit isn’t installed or you need to reinstall it, use the following commands:

bash
sudo apt install metasploit-framework -y
This will fetch and install the latest version of Metasploit directly from the Kali repositories.

Step 4: Launch Metasploit
Once installation is complete, start Metasploit with:

bash
msfconsole
You should see the Metasploit banner, and the console will be ready for commands.

Step 5: Verify Installation
To confirm everything is working, test the version of Metasploit by typing:

bash
version
This will display the framework version number.

Conclusion
Now you’re set up and ready to explore the power of Metasploit. Whether you’re conducting vulnerability assessments or exploring modules for penetration testing, you’ve got one of the most powerful tools in your arsenal. Happy hacking (responsibly)!