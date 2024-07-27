## SSH Protocol Lesson

### Introduction to SSH
SSH, which stands for Secure Shell, is a network protocol that enables a secure and encrypted connection between a client and a server. It is widely used for accessing remote systems and executing commands or transferring files securely.

### Generating SSH Keys
To use SSH securely, it is recommended to use key-based authentication rather than password credentials. Let's go through the process of generating SSH keys.

### Step 1: Generating an SSH Key
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

### Step 2: Copying the Public Key to the Server
After generating the key, you need to copy the public key to the server you want to access. You can do this using the `ssh-copy-id` command:

```bash
ssh-copy-id -i ~/.ssh/my_ssh_key.pub user@remote_server
```

or add the key manually from the site.

**Explanation of the Command:**
- `-i ~/.ssh/my_ssh_key.pub`: specifies the file of the public key to be copied.
- `user@remote_server`: replace `user` with your username on the server and `remote_server` with the IP address or hostname of the server.

### Step 3: First Access to the Server
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
