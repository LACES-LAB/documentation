---
title: Set up SSH on lab computers for passwordless login to the Lab computers
---

1. Open a terminal window on your computer. On Windows, you can use the Git Bash terminal that comes with Git for Windows. On Mac, you can use the Terminal application. On Linux, you can use the terminal application that comes with your distribution.

2. Type the following command in the terminal window:

```bash
ssh-keygen -t rsa
```

3. When prompted, enter a filename and location in which to save the key pair. For example, you can enter `~/.ssh/id_rsa` to save the key pair in the `.ssh` directory in your home directory. You can also enter a passphrase to protect the private key. If you enter a passphrase, you will be prompted to enter it each time you use the key pair to log in to a remote computer.

4. After the key pair is generated, type the following command to copy the public key to the remote computer:

```bash
ssh-copy-id username@jumpgate.scorec.rpi.edu
```
replace `username` with your RCS ID.

4. **For windows**, `ssh-copy-id` is not available. You can manually copy the public key to the remote computer. 

    1. Open the public key file (e.g., `~/.ssh/id_rsa.pub`) in a text editor. 
    2. Copy the contents of the file to the clipboard.
    3. Log in to the remote computer with `ssh remote_name`.
    4. Open the `~/.ssh/authorized_keys` file in a text editor. And paste the contents of the clipboard to the end of the file. Save the file.

5. When prompted, enter the password for the remote computer. The public key will be copied to the remote computer and installed in the `~/.ssh/authorized_keys` file. You can now log in to the remote computer without entering a password.