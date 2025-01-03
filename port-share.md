# port share

To create a custom shell command on your Mac for running the `ssh arifpro@srv.us -R` command with flexible port options, you can define a shell function or script. Here's how to do it:

---

### **Requirements**

- **SSH Access**: You need SSH access to the server `srv.us` with the username `arifpro`.
- **Shell Configuration**: You should have a `.zshrc` or `.bashrc` file in your home directory.
- `ssh-keygen -t ed25519` to generate a new SSH key pair and add it to the github account to use github username to share the port.

---

### **Option 1: Add a Shell Function in Your `.zshrc` (or `.bashrc`)**

1. **Open your shell configuration file**:

   ```bash
   nano ~/.zshrc
   ```

   (Replace `.zshrc` with `.bashrc` if you're using Bash.)

2. **Add the following function**:

   ```bash
   port() {
       local username="arifpro"
       local server="srv.us"
       local port_args=""

       # Process arguments
       for port in "$@"; do
           port_args="$port_args -R ${port}:localhost:${port}"
       done

       # Run the SSH command
       ssh "${username}@${server}" $port_args
   }
   ```

3. **Save and apply the changes**:

   ```bash
   source ~/.zshrc
   ```

4. **Usage**:
   - For a single port:

     ```bash
     port 5001
     ```

   - For multiple ports:

     ```bash
     port 5001 3000
     ```

---

### **Option 2: Create an Executable Script**

1. **Create the script file**:

   ```bash
   nano ~/bin/port

   # or we can create the file and open it in VS Code

   # **Open Terminal**:
   mkdir -p ~/bin

   # **Create the Script File**:
   touch ~/bin/port

   # **Open the Script in VS Code**:
   code ~/bin/port
   ```

   (If `~/bin` doesn't exist, create it: `mkdir ~/bin` and add it to your `PATH` by editing `~/.zshrc` or `~/.bashrc` to include `export PATH="$HOME/bin:$PATH"`.)

2. **Add the script content**:

   ```bash
   #!/bin/bash
   username="arifpro"
   server="srv.us"
   port_args=""

   # Process arguments
   for port in "$@"; do
       port_args="$port_args -R ${port}:localhost:${port}"
   done

   # Run the SSH command
   ssh "${username}@${server}" $port_args
   ```

3. **Make the script executable**:

   ```bash
   chmod +x ~/bin/port
   ```

4. **Usage**:
   - For a single port:

     ```bash
     port 5001
     ```

   - For multiple ports:

     ```bash
     port 5001 3000
     ```

---

### **Explanation**

- **Dynamic Ports**: The script/function loops through all provided arguments and creates `-R` mappings dynamically.
- **Custom Command**: You use a simple command (`port`) instead of the full `ssh` syntax.
- **Reusable**: Add as many ports as needed in one command.
