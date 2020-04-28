# SSH-Git
This repository will give instructions on how to create an SSH key, link it to your GitHub accout, and how to expedite the process of making commits to your remote repository on Mac.

### Creating an SSH Key

1. Open Terminal

2. Paste the following text after the $ symbol into the console replacing your GitHub email in the quotes. You can find your primary GitHub email by traveling to your Personal settings -> Emails. This will create a new SSH key in the default file location.
```bash
$ ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```

3. When prompted to enter a passphrase, press enter to leave the SSH key without a passphrase. In practice, most SSH keys are without a passphrase. If you would like to add one to yours, feel free to read more [here](https://www.ssh.com/ssh/passphrase).

### Adding SSH Key to the ssh-agent.

1. Start the ssh-agent by pasting the text after the $ symbol. The line below should appear.
```bash
$ eval "$(ssh-agent -s)"
> Agent pid 59566
```

Most newer Macs will be using an Operating System newer than MacOS 10.12.2. Therefore, you will need to modify your `config` file in the `~/.ssh/config` directory.

2. To travel to the *hidden* ssh directory paste the following into terminal.
```bash
$ cd ~/.ssh
```

3. After travelling to the ssh directory, check to see if a `config` file exists in the directory by typing the following:
```bash
$ ls
```
This will list all the files present in the current directory.


* If a config file does does not exist in the directory, you will need to create one. Create one by entering the following into your terminal:
```bash
$ touch config
```

* If a config file exists in the ssh directory, open it in your favorite text editor by entering the following and replacing your preferred app in the quotes. 

> Note: The application's name must be its exact name. For example, to open in Sublime text editor, enter 'Sublime Text'. To find an applications exact name, hover over the app's icon and the app's full name will appear above it.

```bash
$ open -a 'Application name' config
```

4. Once you have your `config` file open in your text editor, paste the following text into the file, and save the changes made to the file.
```
Host *
  AddKeysToAgent yes
  UseKeychain yes
  IdentityFile ~/.ssh/id_rsa
```


