# EC2-Lab-Create-EC2-Without-Key-Pair-Manually-Configure-SSH-Access

Create an EC2 instance without a key pair, generate SSH keys inside the instance, and securely connect from your local machine.

# What you will learn

- Launch EC2 without key pair
- Generate SSH keys inside EC2
- Configure authorized_keys
- Connect EC2 from local machine


# Step 1: Launch EC2 Instance (No Key Pair)
Go to AWS Console → EC2 → Launch Instance
- Configure:
- Name: No-Key-EC2
- AMI: Amazon Linux
- Instance type: t2.micro
- Key Pair: Proceed without key pair
- 
Network Settings:
- Allow SSH (Port 22) from your IP
- Click Launch Instance

# Step 2: Connect Using EC2 Instance Connect
Select your instance
Click Connect
Choose EC2 Instance Connect
Click Connect

# Step 3: Generate SSH Key Inside EC2
```bash
ssh-keygen -t rsa -b 2048

```

👉 Press Enter for all prompts

# Step 4: Verify Keys

```bash
cd ~/.ssh
```

```bash
ls
```

👉 Expected files:

- id_rsa
- id_rsa.pub

# Step 5: Add Public Key to authorized_keys

```bash
mv id_rsa.pub authorized_keys
```
# Step 6: Set Permissions

```bash
chmod 700 ~/.ssh
```

```bash
chmod 600 ~/.ssh/authorized_keys
```

# Step 7: Copy Private Key

```bash
cat id_rsa
```

👉 Copy the full output

# Step 8: Save Key on Local Machine
Open Notepad
Paste key

Save as:
- my-ec2-key.pem

# Step 9: Set Permission on Key

```bash
chmod 400 my-ec2-key.pem
```

# Step 10: Connect to EC2 from Local Machine

```bash
ssh -i my-ec2-key.pem ec2-user@<EC2-PUBLIC-IP>
```

👉 Example:

```bash
ssh -i my-ec2-key.pem ec2-user@3.110.xxx.xxx

```

# Important Concept

Public key → stored in EC2 (authorized_keys)

Private key → used from your system

SSH matches both keys for secure login

# Common Issues

Permission denied → check .pem permissions
Connection timeout → check Security Group (Port 22)
Invalid key → ensure correct key copied

# Final Result

EC2 launched without key pair

SSH key generated manually

Secure connection established from local machine
