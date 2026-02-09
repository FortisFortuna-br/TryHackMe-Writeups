Bounty Hacker - TryHackMe Walkthrough
Machine IP=10.48.162.249

1. Enumeration & Discovery
Nmap Scan: Identified open ports 21 (FTP), 22 (SSH), and 80 (HTTP).

FTP Access: Logged in as anonymous and retrieved locks.txt and task.txt.

2. Initial Access
Brute Force: Used Hydra with the locks.txt wordlist to crack the SSH password for user lin.

Used the locks.txt file found on FTP to perform a brute force attack against the SSH service.
Hydra Command: hydra -l lin -P locks.txt ssh://<MACHINE_IP>

SSH Login: Successfully gained access to the system as a low-privileged user.

3. Privilege Escalation
System Check: Ran sudo -l to check for passwordless sudo commands.

Vulnerability: Discovered that /bin/tar could be run as root without a password.

Exploit Technique: Used GTFOBins tar exploitation with wildcard/checkpoint parameters to spawn a root shell.

Final Payload: sudo tar -cf /dev/null /dev/null --checkpoint=1 --checkpoint-action=exec=/bin/sh  

5. Post-Exploitation
Root Access: Confirmed root privileges with whoami.

Flags: Successfully captured both user.txt and root.txt flags.
