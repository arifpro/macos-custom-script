# ☁️ EC2 Quick Connect Script: `arif-ec2`

This is a convenient Bash script that allows you to quickly and securely connect to your EC2 instance without typing out the full SSH command each time.

---

## 🧰 What It Does

- ✅ Uses a pre-defined `.pem` file for authentication
- ✅ Connects to a specific EC2 instance using a custom command: `arif-ec2`
- ✅ Verifies that the `.pem` file exists before attempting connection
- ✅ Prevents common mistakes by checking variables and permissions

---

## 📂 Script Location

Place the script in your `~/bin` folder so it’s globally accessible as a terminal command:

```bash
mkdir -p ~/bin
```

Then create the file:

```bash
nano ~/bin/arif-ec2
```

Paste the following:

```bash
#!/bin/bash
PEM_FILE="$HOME/Documents/ec2/devarif/devarif-instance-1.pem"
INSTANCE_USER="ubuntu"
INSTANCE_IP="ec2-15-206-67-164.ap-south-1.compute.amazonaws.com"

# Check if the PEM file exists
if [ ! -f "$PEM_FILE" ]; then
    echo "❌ Error: PEM file not found at $PEM_FILE"
    exit 1
fi

# Check if the instance user and IP are set
if [ -z "$INSTANCE_USER" ] || [ -z "$INSTANCE_IP" ]; then
    echo "❌ Error: Instance user or IP not set"
    exit 1
fi

# Connect to the EC2 instance
echo "🔌 Connecting to EC2 instance at $INSTANCE_IP..."
ssh -i "$PEM_FILE" "$INSTANCE_USER@$INSTANCE_IP" || { echo "❌ Connection failed"; exit 1; }
```

---

## ✅ Make It Executable (every time you update)

After creating or updating the script, make it executable:

```bash
chmod +x ~/bin/arif-ec2
```

---

## 🛠 Add to PATH (if not already)

Ensure `~/bin` is in your shell’s PATH:

```bash
echo 'export PATH="$HOME/bin:$PATH"' >> ~/.zshrc
source ~/.zshrc
```

> Use `.bashrc` instead if you're using Bash.

---

## 🔐 Fix Permissions (Important)

Ensure the `.pem` file has correct permissions:

```bash
chmod 400 ~/Documents/ec2/devarif/devarif-instance-1.pem
```

---

## 🚀 Usage

Now you can connect to your EC2 instance with a simple command:

```bash
arif-ec2
```

---

## 📋 Output Example

```bash
🔌 Connecting to EC2 instance at ec2-15-206-67-164.ap-south-1.compute.amazonaws.com...
Welcome to Ubuntu 22.04 LTS
Last login: ...
```

---

## 📧 Contact

- 🌐 [devarif.me](https://devarif.me)
- 💼 [LinkedIn](https://www.linkedin.com/in/devarif)
- 💻 [GitHub](https://github.com/arifpro)
