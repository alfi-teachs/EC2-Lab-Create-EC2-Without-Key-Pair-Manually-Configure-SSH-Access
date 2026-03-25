# EC2-Lab-Create-EC2-Without-Key-Pair-Manually-Configure-SSH-Access
Create an EC2 instance without a key pair, generate SSH keys inside the instance, and securely connect from your local machine.

Step 1: Launch EC2 Instance (No Key Pair)

Go to AWS Console → EC2 → Launch Instance

Configure:

Name: No-Key-EC2
AMI: Amazon Linux 2
Instance Type: t2.micro
Key Pair: Select → Proceed without key pair

Network Settings:

Allow SSH (Port 22) from your IP

Click Launch Instance

Step 2: Connect Using Browser (EC2 Instance Connect)
Select your instance
Click Connect
Choose EC2 Instance Connect
Click Connect
Step 3: Generate SSH Key Inside EC2

'''bash
ssh-keygen -t rsa -b 2048
'''

Press Enter for all prompts.

Step 4: Verify Keys

'''bash
cd ~/.ssh
'''

'''bash
ls
'''

Expected output:

id_rsa
id_rsa.pub

Step 5: Add Public Key to authorized_keys

Check existing files:

'''bash
ls
'''

If authorized_keys exists:

'''bash
cat id_rsa.pub >> authorized_keys
'''

If not:

'''bash
cp id_rsa.pub authorized_keys
'''

Set permissions:

'''bash
chmod 700 ~/.ssh
'''

'''bash
chmod 600 ~/.ssh/authorized_keys
'''

Step 6: Copy Private Key

'''bash
cat id_rsa
'''

👉 Copy the full output

On Local Machine (Windows)
Open Notepad
Paste key
Save as:
my-ec2-key.pem

Step 7: Set Permission on Key

'''bash
chmod 400 my-ec2-key.pem
'''

Step 8: Connect from Local Machine

'''bash
ssh -i my-ec2-key.pem ec2-user@<EC2-PUBLIC-IP>
'''

Example:

'''bash
ssh -i my-ec2-key.pem ec2-user@3.110.xxx.xxx

'''

✅ Expected Output
[ec2-user@ip-xxx-xxx-xxx-xxx ~]$

⚠️ Important Notes
Instance must have Public IP
Security Group must allow:
Port: 22
Source: Your IP

Keep .pem file secure
Do not share private key
🧠 Concept
Public key → stored in EC2 (authorized_keys)
Private key → used from your local system
SSH matches both keys for secure login
