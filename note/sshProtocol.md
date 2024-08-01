#### SSH Protocol & VPS

### How SSH Authentication Works:
SSH (Secure Shell) is a protocol that provides a secure channel over an unsecured network. SSH uses a public-key cryptography system for authentication, which involves two keys: a public key and a private key. The public key is shared with the server, while the private key remains with the client. When a client attempts to connect to an SSH server, the server sends a challenge that can only be answered using the private key, verifying the client's identity without transmitting sensitive information.

### Key Generation:
Keys are typically generated using tools like `ssh-keygen`. A user can create a new key pair with the following command:

```bash
ssh-keygen -t rsa -b 2048 -f ~/.ssh/my_ssh_key
```

Here:
- `-t rsa` specifies the type of key to create (RSA).
- `-b 2048` sets the key size to 2048 bits, which is secure for most applications.
- `-f ~/.ssh/my_ssh_key` specifies the name and the file path where the keys will be saved, creating `my_ssh_key` (private key) and `my_ssh_key.pub` (public key).

### Inserting Public Key During VPS Creation:
When creating a Virtual Private Server (VPS), the provider usually has an option to add the public key in the settings. This key should be the public key of the root user, named `key_name.pub` in this example. Once added, this allows the server to recognize the root user's private key for future SSH authentication.

**Accessing a VPS:**
To access the VPS, you can use the SSH command with your private key. For example:

```bash
ssh -i ~/.ssh/key user_name@your_vps_ip
```

In this command:
- `-i ~/.ssh/key` specifies the private key file to use.
- `user_name@your_vps_ip` indicates the user of the VPS and its IP address.

### Accessing as Root:
To acces as Root user:

```bash
ssh -i ~/.ssh/my_ssh_key root@your_vps_ip
```

### Adding New Users and Assigning SSH Keys:
To add a new user and grant them `sudo` privileges, you first create the user with the following command:

```bash
adduser newuser
```

Next, you can add the user to the `sudo` group:

```bash
usermod -aG sudo newuser #skip this part if you dont want add the sudo privileges
```

Now, to assign the user an SSH key, you must first generate a key pair on the user's local machine. Using the same command as before, the user would create their private and public keys:

```bash
ssh-keygen -t rsa -b 2048 -f ~/.ssh/newuser_ssh_key
```

Then, the public key `newuser_ssh_key.pub` needs to be copied to the new user's `~/.ssh/authorized_keys` file on the VPS. This can be done by:

```bash
mkdir -p /home/newuser/.ssh
cat newuser_ssh_key.pub >> /home/newuser/.ssh/authorized_keys
```

Lastly, you must set the correct permissions:

```bash
chown newuser:newuser /home/newuser/.ssh/authorized_keys
chmod 600 /home/newuser/.ssh/authorized_keys
```

This ensures that the new user can now access the VPS securely using their SSH key with the following command:

```bash
ssh -i ~/.ssh/newuser_ssh_key newuser@your_vps_ip
```

Using these commands, users can securely access the VPS and manage permissions and capabilities as required.
