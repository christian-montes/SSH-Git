# SSH-Git
This repository will give instructions on how to create an SSH key, link it to your GitHub accout, and how to expedite the process of making commits to your remote repository on Mac.

### Creating an SSH Key
---

1. Open Terminal

2. Paste the following text after the $ symbol into the console replacing your GitHub email in the quotes. You can find your primary GitHub email by following these steps:
	<ol>
		<li>Click on your profile photo in the top-right corner of any page</li>
		<li>Select settings</li>
		<li>Select 'Emails' from the menu on the left</li>
	</ol>
Your primary email address will have a green 'primary' tag on it.

```bash
$ ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```

3. When prompted to enter a passphrase, press enter to leave the SSH key without a passphrase. In practice, most SSH keys are without a passphrase. If you would like to add one to yours, feel free to read more here: [SSH passphrases](https://www.ssh.com/ssh/passphrase).

### Adding SSH Key to the ssh-agent
---

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
This will list all the files present in the current directory. Make sure that a file called `id_rsa.pub` exists in the directory. This is your SSH key.


* If a config file does does not exist in the directory, you will need to create one. Create one by entering the following into your terminal:
```bash
$ touch config
```

* If a config file exists in the ssh directory, open it in your favorite text editor by entering the following and replacing your preferred app in the quotes. 

> Note: The application's name must be its exact name. For example, to open in Sublime text editor, enter 'Sublime Text'. To find an application's exact name, hover over the app's icon and the app's full name will appear above it.

```bash
$ open -a 'Application name' config
```

4. Once you have your `config` file open in your text editor, paste the following text into the file, and save the changes made to the file before closing it.
```
Host *
  AddKeysToAgent yes
  UseKeychain yes
  IdentityFile ~/.ssh/id_rsa
```

5. Finally, add your SSH key to the ssh-agent by entering the following:
```bash
$ ssh-add -K ~/.ssh/id_rsa
```

### Adding your SSH key to your GitHub account
---

1. Open your public SSH key and copy the contents to your clipboard:
```bash
$ open -a 'Application name' id_rsa.pub
```

2. Go to your SSH key settings by:
	<ol>
		<li>Click on your profile photo in the top-right corner of any page</li>
		<li>Select settings</li>
		<li>Select 'SSH and GPG keys' from the menu on the left</li>
	</ol>

3. Click __New SSH key__ or __Add SSH key__.

4. Add a description of your key in the _Title_ field and paste your SSH key into the _Key_ field.

5. Click __Add SSH key__ and enter your password if prompted.

> Your SSH key should now be added to your GitHub account. Verify that the SSH key is in the __SSH and GPG keys__ settings.

### Creating .bash_profile to make commits quicker
---

To expedite the process of making commits to your remote repository, you will write a function within a `.bash_profile` that can be accessed from any directory you are working in. This `.bash_profile` will exist in your home directory- this will allow access from any directory.

1. Enter the following into terminal to travel to your home directory:
```bash
$ cd ~
```

2. Create a `.bash_profile` by using the touch command
```bash
$ touch .bash_profile
```

3. Open your `.bash_profile` in a text editor by entering the following. Replace the editor's name in the quotes
```bash
$ open -a 'App name' .bash_profile
```

4. Skip a few lines at the end of the file. This is where you will write your function to make the process of committing quicker. Adding a function to the `.bash_profile` allows you to pass arguments to the function. Below is the function 'easygit' that I added to mine. Feel free to name your function whatever you please.

```
function easygit() {
    git add .
    git commit -a -m "$1"
    git push "$2"
}
```

This function allows you to pass a custom message for every commit as well as the remote repo where the changes will be going. This can be done in terminal as follows:
```bash
$ easygit 'Commit message' 'git@github.com:username/repo-name.git'
```

For other solutions that do not involve making a function in your `.bash_profile`, check out the following page in Stack Overflow where I found the solution I used: [Stack Overflow](https://stackoverflow.com/questions/19595067/git-add-commit-and-push-commands-in-one 'Git add, commit, and push in one line').










