# Getting Started
This is the beginning...

## Summary
To get things kicked off on the right foot, we're gonna knock out quite a few administrative tasks that will get us in a great spot to get moving more quickly.

Assuming that you are working as part of a team, we're going to get things setup correctly from the beginning so that as team members join in the fun, we can streamline the administrative tasks and prevent headaches.

Simply put, here is what we need to get done...
- Install Some Tools
- Create some SSH Keys
- Create some Accounts
  - An Admin Account that will be used to Register our Team Accounts.
  - An Individual Account that you will use.


## Tools
We're gonna take a few minutes to install a few tools, just enough to get us started...

- ATOM (Text Editor) https://atom.io/
- GIT (Source Code ) https://git-scm.com/
- NODE + NPM (Node JS) https://nodejs.org/en/
- LASTPASS (Password Vault) https://lastpass.com


## SSH Keys
We're going to create some SSH Keys... one set for an admin account and another our own individual accounts for each member of the team.

SSH keys provide a more secure way of logging into servers with SSH than using a password. We will be using SSH Keys quite extensively.

- Generating a Key Pair is simple.
- You will have a Public and Private Key.
- You place the Public Key (.pub) on any server.
- You unlock the Public Key with your Private Key on your local workstation.
- You do not share your Private Key. Ever.


We're going to create an SSH Key Pair for an Admin Account (e.g. admin@example.com)

### EXAMPLE:
STEP 1: Create the RSA Key Pair
```
    ssh-keygen -t rsa -C "admin@example.com"
    Generating public/private rsa key pair.
```

STEP 2: You'll be prompted with several additional questions...
```
    Enter file in which to save the key (/Users/john.doe/.ssh/id_rsa): id_admin_example_com
    Enter passphrase (empty for no passphrase): <leave blank>
    Enter same passphrase again: <leave blank>
    Your identification has been saved in id_admin_example_com
    Your public key has been saved in id_admin_example_com.pub
```

We're going to create an SSH Key Pair for your Individual Account (e.g. john.doe@example.com)

### EXAMPLE:
STEP 1: Create the RSA Key Pair
```
    ssh-keygen -t rsa -C "john.doe@example.com"
    Generating public/private rsa key pair.
```

STEP 2: You'll be prompted with several additional questions...
```
    Enter file in which to save the key (/Users/john.doe/.ssh/id_rsa): id_john_doe_example_com
    Enter passphrase (empty for no passphrase): <leave blank>
    Enter same passphrase again: <leave blank>
    Your identification has been saved in id_john_doe_example_com
    Your public key has been saved in id_john_doe_example_com.pub
```

### TIP:
Good Practices for SSH Keys make it much more simple to manage down the road for yourself and the team.  The more declarative the better is a good rule of thumb.


## CREATE ACCOUNTS
We're gonna take some time to create a couple of accounts for various services.

Let's start with the assumption you have your own domain... and existing email accounts.

- Admin Email account (e.g. admin@example.com)
- Individual Email Account (e.g. john.doe@example.com)

### Setup Guides
If you don't have accounts for the following services, here are a few quick guides that we've pulled together that will get you on your way.  Most of these services have excellent documentation, so definitely take some time to read and review.  We'll just be covering the basics to get you and your team moving quickly.

Here is a list of the Accounts and Services we'll be starting off with...
- Setup LastPass Account
- Setup GitHub Account, Organization, and Team
- Setup Travis-CI Account
- Setup DigitalOcean Account
- Setup AWS Account
- Setup DockerHub Account
