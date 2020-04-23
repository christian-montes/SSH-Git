# SSH-Git
This repository will give instructions on how to create an SSH key, link it to GitHub, and how to expedite the process of pushing changes to GitHub through bash..

### Creating an SSH Key

1. Open Terminal

2. Paste the text below into the console:
```bash
$ ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```
This will create a new SSH key in the default file location.

3. When prompted to enter a passphrase, press enter to leave the SSH key without a passphrase. In practice, most SSH keys are without a passphrase. If you would like to add one to yours, feel free to read more [here][https://www.ssh.com/ssh/passphrase].