# SSH-Git
This repository will give instructions on how to create an SSH key, link it to your GitHub accout, and how to expedite the process of making commits to your remote repository on Mac.

> Note: The following instructions are an edited version of those found on [Github](https://help.github.com/en/github/authenticating-to-github/connecting-to-github-with-ssh) that include extra steps that are skipped on the page and instructions on how to create a `.bash_profile` to speed up the process of making commits to your remote repo.

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

<br>

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

2. Go to your SSH key settings:
	<ol>
		<li>Click on your profile photo in the top-right corner of any page</li>
		<li>Select settings</li>
		<li>Select 'SSH and GPG keys' from the menu on the left</li>
	</ol>

3. Click __New SSH key__ or __Add SSH key__.

4. Add a description of your key in the _Title_ field and paste your SSH key into the _Key_ field.

5. Click __Add SSH key__ and enter your password if prompted.

### Testing connection

Your SSH key should now be added to your GitHub account. Verify that the SSH key is linked to your account by testing your connection.

1. Enter the following in terminal that attempts to ssh to GitHub
```bash
$ ssh -T git@github.com
```

This will lead to one of two following warnings showing up:
```
> The authenticity of host 'github.com (IP ADDRESS)' can't be established.
> RSA key fingerprint is 16:27:ac:a5:76:28:2d:36:63:1b:56:4d:eb:df:a6:48.
> Are you sure you want to continue connecting (yes/no)?
```

or
```
> The authenticity of host 'github.com (IP ADDRESS)' can't be established.
> RSA key fingerprint is SHA256:nThbg6kXUpJWGl7E1IGOCspRomTxdCARLviKw6E5SY8.
> Are you sure you want to continue connecting (yes/no)?
```

2. Make sure that the warning that shows up matches on of the two above and type 'yes'.

3. A message like the one below should come up if everything went well.
```
> Hi christian-montes! You've successfully authenticated, but GitHub does not
> provide shell access.
```

Make sure that your username is contained in the message.

### Creating .bash_profile to make commits quicker
---

To expedite the process of making commits to your remote repository, you will append a function to a `.bash_profile`. This `.bash_profile` will exist in your home directory- this will allow access from any working directory.

> Note: These instructions are an edited version of instructions on how to create a `.bash_profile` that can be found here: [Redfin Solutions](https://redfinsolutions.com/blog/creating-bashprofile-your-mac 'Creatng a .bash_profile')

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

4. Skip a few lines at the end of the file. This is where you will write your function to make the process of committing quicker. 

Adding a function to the `.bash_profile` allows you to pass arguments to the function. Below is the function 'easygit' that I added to mine. Feel free to name your function anything you please. The first argument accepted by the function, "$1", is the commit message; the second argument, "$2", is the SSH URL of the repository.

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

> For other solutions that do not involve making a function in your `.bash_profile`, check out the following page in Stack Overflow where I found the solution I used: [Stack Overflow](https://stackoverflow.com/questions/19595067/git-add-commit-and-push-commands-in-one 'Git add, commit, and push in one line').

5. After adding your function to your `.bash_profile`, save all changes and close the file.

6. Finally, paste the following into terminal to reload the profile and update any functions that were added.
```bash
$ . .bash_profile
```

You are now ready to make quicker commits using terminal.









