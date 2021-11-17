# Version Control

Version control refers to a version control application such as git, subversion, or mercurial in addition to a version control platform such as GitHub and GitLab.  This document will give you the quick overview of how to use Git and GitHub.  

## Install git

Refer to [this page](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git) for how to install git.  

To install on a Mac, download the macOS Git installer [here](https://git-scm.com/download/mac). 

Use this command to verify it's installed. 
```
git --version
```

## Create a GitHub account

Create a free GitHub account by going to [G]itHub.com](http://www.github.com).   To complete signup, you'll need to verify your email address.

### Configure Multi-factor Authentication for your GitHub account

It is strongly recommended to set up two factor authentication in your GitHub account.  Learn more on the [GitHub Docs Configuring two-factor authentication page](https://docs.github.com/en/authentication/securing-your-account-with-two-factor-authentication-2fa/configuring-two-factor-authentication). 

## Gitting Started: Setting Up your SSH Keys for GitHub

### Generating New Keys
For an in depth guide, see GitHub's documentation for [Generating a new SSH keypair and adding it to the ssh-agent](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)

This will require five main steps.
1. Check to see if you have an existing ssh keypair
1. Generate a new ssh keypair if needed
1. Add the key to your ssh-agent and update your configuration file
1. Add your public key to your GitHub account
1. Test your connection

### 1. Check to see if you have an existing SSH keypair

1. Check to see if you have existing SSH keys.  Type the following command to list the contents of your .ssh directory.  
```
ls -al ~/.ssh
```

If the output lists id_rsa.pub, id_ecdsa.pub, or id_ed25519.pub then you probably already have a keypair. 

If you get an error that the directory doesn't exist, then you likely don't already have a keypair. 

### 2. Generate a new ssh keypair

Use the following command to generate a new keypair. Replace the email address with the email associated with your GitHub account. 
```
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```
This will create a new keypair and give you three prompts.  Just press enter without typing anything.  

Verify the keys have been generated.  
```
ls -al ~/.ssh
```

You should see `id_rsa` and `id_rsa.pub`.   `id_rsa` is your private key.  Do not share it with anyone.  Never allow your private key to be committed to your version control system with your code.  `id_rsa.pub` is your public key.  It can be shared with GitHub.  

### 3. Add the key to your ssh-agent and update your configuration file

Start the ssh-agent
```
eval "$(ssh-agent -s)" 
```

Check to see if you already have a ssh configuration file
```
open ~/.ssh/config
```

If you get an error that the file does not exist, create one now.
```
touch ~/.ssh/config
```

Add the following text to your config file.  
```
Host github.com
  User lindyslewis
  IdentityFile ~/.ssh/id_rsa
```

Add your ssh private key to the ssh-agent
```
ssh-add ~/.ssh/id
```

### 4. Add your public key to your GitHub account

Copy the contents of your public key to your clipboard. 
```
pbcopy < ~/.ssh/id_rsa
```

In your browser, navigate to your GitHub account.  In the upper right corner, click on your profile photo.  Click settings.  On the left sidebar of the settings page, click `SSH and GPG keys`.  Click `New SSH Key`.  

In the title field, enter something descriptive such as "Stelligent MacBook Pro" or "Personal Macbook Air".  

In the key field, paste your key. Click Add SSH Key. Confirm your password if prompted. 

### 5. Test your connection

Test your connection with the following command
```
ssh -T git@github.co
```

You should see a warning about the authenticity of the host.  Click yes that you are okay to continue.  