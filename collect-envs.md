# 🛠️ Collect .env Files Script for macOS

This script searches your entire macOS filesystem for `.env*` files (e.g., `.env`, `.env.local`, `.env.production`, etc.), then copies them to your Desktop in a folder named `envs`, renaming each file to reflect its full path using dot notation.

You can run this from anywhere using the command: `collect-envs`

---

## 📌 Features

- ✅ Scans entire macOS (`/`) for `.env*` files
- ✅ Renames files using full folder path (e.g., `Users.arif.Projects.my-app.env.local`)
- ✅ Copies to `~/Desktop/envs`
- ✅ Automatically creates the target folder if it doesn't exist
- ✅ Replaces files if a matching name already exists

---

## 🚀 Setup Instructions

### 1. Create the Script File

```bash
mkdir -p ~/bin
nano ~/bin/collect-envs
```

### 2. Paste the Following Script

```bash
#!/bin/bash

# Define the target directory
TARGET_DIR="$HOME/Desktop/envs"

# Create the target directory if it doesn't exist
mkdir -p "$TARGET_DIR"

echo "🔍 Scanning filesystem for .env* files. This may take a while..."

# Find and process .env* files
sudo find / -type f -name ".env*" 2>/dev/null | while read file; do
  # Remove leading slash
  relative_path="${file#/}"

  # Get folder path and env file name
  folder_path="$(dirname "$relative_path")"
  env_name="$(basename "$file")"

  # Replace slashes with dots and remove leading dot from filename
  new_name="${folder_path//\//.}.${env_name#.}"

  # Full destination path
  dest="$TARGET_DIR/$new_name"

  # Copy the file (overwrite if exists)
  cp -f "$file" "$dest"
done

echo "✅ All .env* files copied to: $TARGET_DIR"
```

---

### 3. Make the Script Executable

```bash
chmod +x ~/bin/collect-envs
```

---

### 4. Add `~/bin` to Your PATH (If Needed)

If it's not already in your `PATH`, add it to your shell config file:

```bash
echo 'export PATH="$HOME/bin:$PATH"' >> ~/.zshrc
source ~/.zshrc
```

(Use `.bashrc` instead if you use Bash.)

---

## 🧪 Usage

Once installed, simply run:

```bash
collect-envs
```

> 🛑 You may be prompted for your password due to `sudo` access required for full system scanning.

---

## 📂 Example Output

If the original file is:

```txt
/Users/arif/Projects/my-app/.env.local
```

It will be copied and renamed as:

```txt
~/Desktop/envs/Users.arif.Projects.my-app.env.local
```

---

## 🧹 Optional Improvements

- Exclude folders like `/System` or `/Volumes` to reduce scan time
- Log output to a `.txt` file
- Automatically zip the final `envs` folder

---

## ✅ License

Feel free to copy, modify, and share!

---

## 📧 Contact

If you find this script useful or have suggestions for improvements, feel free to reach out!

- 🌐 [devarif.me](https://devarif.me)
- 💼 [LinkedIn](https://www.linkedin.com/in/devarif)
- 💻 [GitHub](https://github.com/arifpro)
