# SSH-Git
This repository will give instructions on how to create an SSH key, link it to GitHub, and how to expedite the process of pushing changes to GitHub through bash on Mac.

### Creating an SSH Key

1. Open Terminal

2. Paste the text after the $ symbol into the console replacing your email in the quotes:
```bash
$ ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```
This will create a new SSH key in the default file location.

3. When prompted to enter a passphrase, press enter to leave the SSH key without a passphrase. In practice, most SSH keys are without a passphrase. If you would like to add one to yours, feel free to read more [here](https://www.ssh.com/ssh/passphrase).

### Adding SSH Key to the ssh-agent.

1. Start the ssh-agent by pasting the text after the $ symbol. The line below should appear.
```bash
$ eval "$(ssh-agent -s)"
> Agent pid 59566
```

Most newer Macs will be using an Operating System newer than MacOS 10.12.2. Therefore, you will need to modify your `config` file in `~/.ssh/config`.

2. To travel to the hidden ssh directory paste the following into terminal.
```bash
$ cd ~/.ssh
```