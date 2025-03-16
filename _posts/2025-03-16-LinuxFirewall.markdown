How to Set Up a Firewall with UFW on Linux
Firewalls are essential for securing your system by controlling incoming and outgoing traffic. In this guide, I’ll show you how to set up and manage a firewall using UFW (Uncomplicated Firewall) on Linux.

Step 1: Install UFW
Most Linux distributions come with UFW pre-installed. If it’s not installed, you can add it with:

bash
sudo apt install ufw
Step 2: Enable UFW
To activate the firewall, run:

bash
sudo ufw enable
You can check its status with:

bash
sudo ufw status
Step 3: Allow or Deny Specific Ports
To allow traffic on a specific port (e.g., SSH on port 22):

bash
sudo ufw allow 22
To deny traffic on a port:

bash
sudo ufw deny 80
Step 4: Allow Applications
UFW can manage predefined application profiles. For example, to allow OpenSSH:

bash
sudo ufw allow OpenSSH
List available profiles with:

bash
sudo ufw app list
Step 5: Test Your Firewall
Ensure your rules are working by testing access to the allowed and denied ports. Use tools like nmap to verify.

Conclusion
With UFW, managing a firewall is straightforward and effective. Regularly review and update your rules to maintain security.