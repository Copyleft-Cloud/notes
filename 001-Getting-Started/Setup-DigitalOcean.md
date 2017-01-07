# Setup DigitalOcean Account

### STEP 1: Go To https://cloud.digitalocean.com

### STEP 2: Sign-Up with your Admin Account
- Email: (e.g. admin@example.com)
- Password: (e.g. Generate Strong Password)

Don't forget to update your password vault. (e.g. LastPass!)

### STEP 3: Confirm Registration
- You’ll Receive an Email and Confirm your Registration
- Follow the Link to complete Registration

### STEP 4: Payment Details
- Provide a Credit/Debit Card for Payment Details
- We’ll need this to create droplets

### STEP 5: Create a Team!
- Pick a Team Name  (Copyleft)
- Convert your existing account into a team account (Yes)
- Click Continue
- Update the Billing Method for the Team (Select the Credit Card to Use)
- Invite Team Members  (can skip this step for now and send invitations later)
- You’ll Receive a confirmation email to the Admin Account
     - Now you can share resources and work collaboratively with your teammates.
     - Introduction to Teams on DigitalOcean (https://www.digitalocean.com/community/tutorials/how-to-use-teams-on-digitalocean)
     - Follow the Link and Check out your New Team Page! https://cloud.digitalocean.com/settings/team/?i=b1a30a

### STEP 6: Team Configuration
From your Team Page you can invite new team members… set Team Permissions… set up Two Factor Authentication… add SSH Keys… etc.

- Invite yourself to the party!
- We’ll use the Admin Account for managing all of the Billing and Administrator stuff etc… however we need to setup individual accounts for ourselves and future team members
- From the Team Page send yourself an invitation
- You’ll get an Invitation Email… Follow the Link to Create your Account and Join the Team
     - Use LastPass to Generate your Password and Store the Credentials
     - This will save you a shit ton of time later… and will help you manage strong passwords for all of your accounts

Email: (e.g. john.doe@example.com)
Password: (e.g. generate a strong password)

From here you should see yourself as a Member.

### STEP 7: Add your SSH Public Key
- Login under your Individual Account (e.g. john.doe@example.com)
- Click on Security under your profile… and Add SSH Key
- Paste in your Public Key (id_john_doe_example_com.pub)
- Provide a Name… I’d recommend using the same name as the private key file in your .ssh directory


### STEP 8: Add the Admin SSH Key
- Switch to the Admin/Team Account
- Click on Security under the Admin profile… and Add SSH Key
- Paste in the Admin Public Key (id_admin_example_com.pub)
- Provide a Name… I’d recommend using the same name as the private key file in your .ssh directory

## Summary
- We’ve Created an Admin Account and converted it to a Team
- We’ve Invited ourselves to the new Team
- We’ve created SSH Keys and Uploaded them to our Team and Individual Profiles
- Ok, we’re all set up for now… let’s move on to AWS
