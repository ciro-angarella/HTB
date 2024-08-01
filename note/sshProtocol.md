## SSH Protocol Lesson

### Introduction to SSH
SSH, which stands for Secure Shell, is a network protocol that enables a secure and encrypted connection between a client and a server. It is widely used for accessing remote systems and executing commands or transferring files securely.

### Generating SSH Keys
To use SSH securely, it is recommended to use key-based authentication rather than password credentials. Let's go through the process of generating SSH keys.

### Generating an SSH Key
You can generate a pair of SSH keys using the following command in the terminal:

```bash
ssh-keygen -t rsa -b 4096 -f ~/.ssh/my_ssh_key
```

**Explanation of Parameters:**
- `-t rsa`: specifies the type of key. RSA is one of the most common key types.
- `-b 4096`: defines the key length. The longer the length, the higher the security.
- `-f ~/.ssh/my_ssh_key`: specifies the file where the key will be saved. You can replace `my_ssh_key` with the name you prefer.

After running this command, two keys will be created:
- `my_ssh_key`: the private key, which should remain secret.
- `my_ssh_key.pub`: the public key, which can be shared.


### Creating a New User ( with Sudo Privileges )

 **Log in as root to your VPS:**
   ```sh
   ssh root@your_vps_ip
   ```
   This command connects you to your VPS using the root user. Replace `your_vps_ip` with the actual IP address of your VPS.

 **Create a new user:**
   ```sh
   adduser cry0l1t3
   ```
   This command creates a new user named `cry0l1t3`. You will be prompted to set a password and provide optional information for the new user.

 **Add the user to the `sudo` group (on some distributions, the group might be `wheel`):**
   ```sh
   usermod -aG sudo cry0l1t3
   ```
   This command adds the user `cry0l1t3` to the `sudo` group, giving the user administrative privileges.

 **Switch to the new user to verify that the user was created correctly:**
   ```sh
   su - cry0l1t3
   ```
   This command switches to the new user `cry0l1t3`. You will need to enter the password for this user when prompted.

### 2. Configuring the SSH Key for the New User

**Log in as the new user (if not already switched):**
   ```sh
   su - cry0l1t3
   ```
   This command ensures you are operating as the new user `cry0l1t3`.

**Create an `.ssh` directory in the user's home directory and set the correct permissions:**
   ```sh
   mkdir ~/.ssh
   ```
   This command creates the `.ssh` directory in the home directory of `cry0l1t3`.

**Add the SSH public key to the `authorized_keys` file:**
   ```sh
   echo '<vps-ssh.pub>' > ~/.ssh/authorized_keys
   ```
   Replace `'<vps-ssh.pub>'` with the actual SSH public key you want to use for accessing the VPS. This command saves the SSH public key to the `authorized_keys` file.

**Set the correct permissions on the `authorized_keys` file:**
   ```sh
   chmod 600 ~/.ssh/authorized_keys
   ```
   This command sets the permissions of the `authorized_keys` file to ensure it is secure. Only the user should have read and write access to this file.

or add the key manually from the site.

**Explanation of the Command:**
- `-i ~/.ssh/my_ssh_key.pub`: specifies the file of the public key to be copied.
- `user@remote_server`: replace `user` with your username on the server and `remote_server` with the IP address or hostname of the server.

### First Access to the Server
Once the public key is copied to the server, you can perform the first login using the following command:

```bash
ssh -i ~/.ssh/my_ssh_key user@remote_server
```

### `known_hosts` File
When you access an SSH server for the first time, the server sends a public key that is stored in the `known_hosts` file in your `.ssh` directory. This file contains a list of public keys of the servers you connect to.

- The access will register a new public key in `~/.ssh/known_hosts`.
   
You can view the contents of this file with:

```bash
cat ~/.ssh/known_hosts
```

### Subsequent Access
To access the server again in the future, you can simply use:

```bash
ssh -i ~/.ssh/my_ssh_key user@remote_server
```

SSH will attempt to authenticate using the private key you specified.

### Verifying Successful Access
After logging in, there are several ways to verify that the access was successful:

1. **Check Terminal Output:** If you did not receive error messages and you have access to the server's shell, the access was successful.
   
2. **Check Remote Environment:** You can execute simple commands to verify that you are indeed on the desired server. For example:

   ```bash
   hostname
   ```

   This command will display the name of the current server.

3. **Exit the Server:** To disconnect from the server, you can simply type:

   ```bash
   exit
   ```
