Step 1: Install OpenSSH Client

Open PowerShell as Administrator and run:

Add-WindowsCapability -Online -Name OpenSSH.Client~~~~0.0.1.0
 Step 2: Fix PATH (if ssh-add opens apps instead)

If running ssh-add opens a “Choose an app” dialog, fix it:

 Remove incorrect ssh-add file
Remove-Item C:\Windows\System32\ssh-add

 Add OpenSSH to PATH
$env:PATH += ";C:\Windows\System32\OpenSSH"

Verify:

where.exe ssh-add

 Expected output:

C:\Windows\System32\OpenSSH\ssh-add.exe
 Step 3: Start the SSH Agent
Start-Service ssh-agent
Get-Service ssh-agent

 Status should be:

Running
 Step 4: Generate an SSH Key

If you don’t already have a key:

ssh-keygen -t ed25519 -C "your_email@example.com"

Press Enter to save in default location:

C:\Users\USERNAME\.ssh\id_ed25519
 Step 5: Add Key to SSH Agent
ssh-add C:\Users\NAIRAH\.ssh\id_ed25519

Output:

Identity added
 Step 6: Copy Your Public Key
Get-Content $env:USERPROFILE\.ssh\id_ed25519.pub



ssh-ed25519 AAAAC3Nz... nairah@NAIRAH
☁️ Step 7: Upload Key to CloudLab
Log in to: https://www.cloudlab.us/ssh-keys.php
Paste your public key into “Add Key”
Click Submit
Wait 1–2 minutes
🔗 Step 8: Connect to Your Node
ssh <username>@<node>.apt.emulab.net
Example:
ssh csc26dad@apt038.apt.emulab.net
