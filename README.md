## 🔐 Restricting SSH Access with Security Groups

### 📘 What This Demonstrates

This short guide explains how I tested AWS Security Groups by **blocking SSH access (port 22)** to an EC2 instance. The test shows how security groups protect your instance by only allowing traffic you explicitly permit.

---

### 🛠️ Step-by-Step Instructions

### 1. Launch an EC2 Instance

1. Go to [AWS EC2 Console](https://console.aws.amazon.com/ec2/)

2. Click **Launch Instance**

3. Use the following settings:
   - **AMI**: Ubuntu Server (any LTS version)

   - **Instance Type**: t2.micro (Free Tier)

   - **Key Pair**: Create new or use existing (`lawuruassign1.pem` file)

   - **Network Settings**:
     - **Create a new Security Group**

     - **DO NOT** add any inbound rules (leave it empty)

---

### 2. Prepare to SSH

In your terminal, navigate to where your `lawuruassign1.pem` key is located and set proper permissions:

```bash
chmod 400 lawuruassign1.pem
```

---

### 3. Try to SSH Into the Instance


Run this command (replace IP and key name) with yours:

```bash
ssh -i lawuruassign1.pem ec2-user@34.234.75.114
```

Observe the response;

```
ssh: connect to host 3.110.45.25 port 22: Connection timed out
```

This happens because the security group blocks all inbound traffic by default, including SSH.

---

### ✅ (Optional) Allow SSH to Test Again

To confirm it's the Security Group:

1. Go to **EC2 → Security Groups**

2. Edit the Security Group attached to your instance

3. Add the following **inbound rule**:

| Type | Protocol | Port Range | Source   |
|------|----------|------------|----------|
| SSH  | TCP      | 22         | Your IP  |


4. Save the rule

Now try the SSH command again — it should work ✅

---





