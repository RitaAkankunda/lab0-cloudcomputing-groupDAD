📝 Lab 0 Documentation: Windows Implementation
1. Account & Project Setup
Action: Registered as csc26dad under the CraneCloud project.

Group Sync: Successfully verified the account via the group email (csc26-dad@cit.ac.ug).

Key Management: Uploaded multiple public keys (for all group members) to the shared account to ensure multi-user access.

2. Infrastructure Configuration
Default Shell: Changed the default shell to bash in the CloudLab "Manage Account" settings as recommended for script compatibility.

Experiment: Instantiated the csc2202-cloud-project profile as DAD-lab0 on the Utah cluster.

3. SSH Authentication Agent (The Windows Challenge)
The manual requested the use of ssh-agent. On our Windows machines, we implemented this using the Windows OpenSSH Authentication Agent service:

Service Initialization: Instead of the Linux ssh-agent command, we used PowerShell to set the service to Automatic and started it.

Identity Loading: Used ssh-add to load the private key (id_ed25519) into the local session.

Agent Forwarding: Successfully used the -A flag to connect to ms0823.utah.cloudlab.us. This confirms that our local keys can now be used by scripts running on the server to talk to other nodes.

💡 Reflection: What worked and what didn't
Worked Well: The ssh-add and ssh -A commands are universal! Once the Windows service was running, the experience was identical to the Linux instructions.

Challenges: The "Permission Denied" errors were initially confusing, but we discovered this was due to the Utah cluster sync delay (it takes ~5 minutes for the server to recognize a new key added to the website).

Windows-Specific Fixes: We had to manually point ssh-add to the $env:USERPROFILE path because Windows handles file shortcuts differently than Linux.
