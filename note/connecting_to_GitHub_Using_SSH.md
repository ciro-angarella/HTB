### Connecting to GitHub Using SSH

#### Introduction
Connecting your GitHub account to your computer via SSH allows you to interact with your repositories securely without repeatedly entering your password. We assume you have already generated an SSH key pair. If not, refer to the instructions for generating SSH keys in the previous lesson.

### Connect GitHub Using SSH

#### Step 1: Add Your Public Key to GitHub

1. **Retrieve Your Public Key:**
   Ensure you have your public key in your `~/.ssh/id_rsa.pub` file (or another file if you used a different name). To view the contents of your public key, use:

   ```bash
   cat ~/.ssh/id_rsa.pub
   ```

2. **Add the Public Key to Your GitHub Account:**
   - Log in to your GitHub account.
   - Navigate to **Settings** by clicking on your user icon in the upper right corner and selecting **Settings**.
   - In the left sidebar, select **SSH and GPG keys**.
   - Click on **New SSH key**.
   - Enter a descriptive **Title** for the key (e.g., "Home Laptop").
   - Paste the public key into the **Key** field.
   - Click **Add SSH key** to complete the process.

#### Step 2: Verify the SSH Connection to GitHub

1. **Test the Connection:**
   You can verify if your SSH key is correctly configured for GitHub using the `ssh` command:

   ```bash
   ssh -T git@github.com
   ```

   If everything is set up correctly, you should receive a welcome message like:

   ```
   Hi username! You've successfully authenticated, but GitHub does not provide shell access.
   ```

   If you receive an error, check that your public key has been correctly added to GitHub and that your private key is in the correct location (`~/.ssh/id_rsa`).

#### Step 3: Configure Git to Use SSH for Repositories

1. **Clone a New Repository Using SSH:**
   If you are cloning an existing GitHub repository, make sure to use the SSH URL instead of the HTTPS URL. You can get the SSH URL from the GitHub repository page:

   - Go to the repository page on GitHub.
   - Click the green **Code** button.
   - Select the **SSH** option and copy the URL.

   Use the `git clone` command to clone the repository:

   ```bash
   git clone git@github.com:username/repository.git
   ```

   Make sure to replace `username` with your GitHub username and `repository` with the name of the repository.

2. **Change the URL of an Existing Repository to Use SSH:**
   If you already have a repository cloned via HTTPS and want to switch to SSH, use the following commands in the repository directory:

   ```bash
   git remote set-url origin git@github.com:username/repository.git
   ```

   This command changes the remote URL `origin` to use the SSH URL.
