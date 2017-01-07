# Setup GitHub Account, Organization, and Team
We're going to use GitHub for our Git repository hosting service.  

### STEP 1: Go To https://github.com/

### STEP 2: Sign Up
- Pick a Username
- Enter an Email Address (e.g. Your Admin Email)
- Create a Password (e.g. Generate Strong Password)

Don't forget to update your password vault. (e.g. LastPass!)

### STEP 3: Create New Organization
- Organization Name: <your domain or team name> (e.g. Copyleft-Cloud)
- Billing Email: <your admin email>
- Plan: Select Unlimited Members and Public Repositories for Free
- Click Create Organization

### STEP 4: Invite Team Members
- Search by Username, Full Name, Email Address  (e.g. john.doe@example.com)
- Click Finish

### STEP 5: Create New Team
- Team Name: (e.g. Engineers)
- Description: (e.g. Copyleft Cloud Engineers)
- Team Visibility: Visible
- Click Create Team

### STEP 6: Check Your Inbox
Check your inbox for the invitation to join the new organization.
- Click Join

### STEP 7: Add your SSH Key
- Add your SSH Public Key to your individual account (e.g. john.doe@example.com)
- Under your Profile - Settings... Click SSH & GPG Keys
- Add Your SSH Public Key (e.g. id_john_doe_example_com.pub)

### STEP 8: Setup your Workspace on your Local Machine
On your Local Workstation… let’s create a workspace directory where we will manage our Repositories for Copyleft Cloud

    # Let’s Create a Main Github Directory
    mkdir Github && cd $_

    # Within that directory, let’s create a directory for our Organization
    # This is where we will keep all of our git repos associated with this Organization
    mkdir copyleft-cloud && cd $_

    # As we create git repos on GitHub this is the directory where we will clone our git repos
    pwd /Users/brian.hooper/Github/copyleft-cloud


## Summary
We've created our GitHub Organization and Team... invited new Team Member(s) and uploaded our SSH Public Key to our Profile.

As we continue, we'll be using GitHub to centrally manage the source code repositories for our team's work.  It's Infrastructure as Code... woot! woot!
