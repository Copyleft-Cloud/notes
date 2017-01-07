# Setup AWS Account

### STEP 1: Go To https://aws.amazon.com/

### STEP 2: Sign Up for an AWS Account
- We'll be signing up using the Admin Account
- Email: (e.g. admin@example.com)
- Name: (e.g. Domain Administrator)
- Password: (e.g. Generate a Strong Password)

Reminder: Let’s Use our Password Vault to Generate and Store another Kickass Password!

### STEP 3: Complete the Sign Up Form
- Accept the Terms
- Provide Payment Information
- Identity Verification
     - Automated Phone Call + Pin
- Support Plan
     - Select Basic, which is Free.
     - Other plans are available starting at $29 per month… select what works best for you and your team.
- Complete Sign-Up

### STEP 4: Sign-In Using Your New Account
- Last Pass is great isn’t it?

### STEP 5: You Should Receive Multiple Emails from AWS
-GETTING STARTED GUIDES https://aws.amazon.com/getting-started/


### STEP 6: Explore around the AWS Services
- Take a few minutes to learn your way around the AWS Services.
- (e.g. https://console.aws.amazon.com/console/home?region=us-east-1#)

Under the Profile Dropdown (Cloud Administrator)
- You can view all of your admin account information
- You can view your Billing Dashboard
     - Note: $0
- You can view your Security Credentials

### STEP 7: Let’s Setup some Security  
- Click Security Credentials under Admin Profile

```
    You are accessing the security credentials page for your AWS account. The account credentials provide unlimited access to your AWS resources.

    To help secure your account, follow an AWS best practice by creating and using AWS Identity and Access Management (IAM) users with limited permissions.
```

- Click Get Started with IAM User (Identity and Access Management)

From here we can add and manage accounts which have access to our AWS Account.
- https://console.aws.amazon.com/iam/home?#/users

### STEP 8: Let’s Create a Security Group
- We need a security group for our team of Cloud Engineers the more declarative the better…

- Group Name: &lt;domain&gt;Engineers  (e.g. CopyleftCloudEngineers)

Let’s Select a Few Policies to Associate with our Security Group
```
    AmazonVPCFullAccess
    - Provides full access to Amazon VPC via the AWS Management Console.

    AmazonEC2FullAccess
    - Provides full access to Amazon EC2 via the AWS Management Console.

    AmazonRDSFullAccess
    - Provides full access to Amazon RDS via the AWS Management Console.

    AmazonS3FullAccess
    - Provides full access to all buckets via the AWS Management Console.

    AmazonElasticFileSystemFullAccess
    - Provides full access to Amazon EFS via the AWS Management Console.
```

- Create the Group… and Now you should see all of the attached Policies.

Important Note:
- CloudEngineers do not have IAM Admin Access to manage User and Permissions… only your admin account does.
- If your team grows, simply create an AccessAdmin Group and attach the appropriate Policy. You can do the same for Billing and other roles.  
- To keep things simple for now we’ll just leave those functions consolidated with our Admin Account.

Now that our Group Exists… let’s add Users as Members…

### STEP 9: Let’s Add Users and Setup Permissions
- Click Add User
```
     Username (e.g. john.doe@example.com)
     AWS Access Type
          - (YES) Programmatic access - Enables an access key ID and secret access key for the AWS API, CLI, SDK, and other development tools.
          - (YES) AWS Management Console access - Enables a password that allows users to sign-in to the AWS Management Console.
     Console Password
          - Select Custom Password and Use LastPass to Generate
          - Deselect Require Password Reset for this time around… as it is your individual account and you’ve already created a strong password via LastPass
     Set Permissions
          - Select CopyleftCloudEngineers (Role/Group)
          - Click Next: Review
     Review
          - Review the Settings
          - Click Create User

     Success!
          - Download Your Credentials (Access Key ID, Secret Access Key)
          - This is the last time these credentials will be available to download. You can always create new credentials at anytime.
          - You'll be provided with AWS Management Console Sign-In URL for your Account

          # Users with AWS Management Console access can sign-in at:
          https://<aws_account_id>.signin.aws.amazon.com/console


```

### STEP 10: Lets Test Console Login
- Our New User Account is Active.  Let’s test the login at the console sign-in URL…
- TEST AWS CONSOLE ACCESS
    - URL https:// &lt;aws_account_id&gt; .signin.aws.amazon.com/console
    (This is provided during IAM User Setup)

#### TIP:
Add This Link To Your Bookmarks (e.g. AWS Console)
Save this new site and credentials to your Project/Domain Folder in LastPass

### STEP 11: Success!
SWEET… SUCCESS, All the Access Permissions are working as expected.

By Default when we setup our AWS Account we get a few things out of the gate… take a few minutes to navigate down the Sidebar of the VPC Dashboard
DASHBOARD https://console.aws.amazon.com/vpc/home?region=us-east-1


EXPLORE VPC DASHBOARD
- Note: By Default we are in the US-EAST-1 REGION (US. East. N Virginia)
- Note: This same basic default setup is present in every region by default.  Use the Drop Down to Change Regions and See For Yourself.

### STEP 12: Explore Default Setup
WHAT WE GOT OUT OF THE GATE…

#### 1 VPC
Our Default Virtual Private Cloud.

#### 4 SUBNETS
Our Default Subnets Associated with Default VPC
- Each Subnet is in a Different Availability Zone
- Each Subnet is Associated with the Main Route Table
- Each Subnet is Associated with the Main Network ACL


#### 1 ROUTE TABLE
Our Main Route Table
- Check out the Routes

Checkout Subnet Associations
- You’ll see all of our default subnets

#### 1 INTERNET GATEWAY
Our Default Internet Gateway Attached to our Default VPC

#### 0 NAT GATEWAYS
By Default, we do not have any NAT Gateways

NAT Gateways in a Public Subnet are used by Private Subnets with Defined Routes to access the Internet through the Internet Gateway attached to your VPC.

Note: There is a running Monthly Charge for a NAT Gateway.

#### 1 NETWORK ACL
Our Default Network ACL (Access Control List)


#### 1 SECURITY GROUP
Our Default Security Group

#### 1 DHCP Options Set
Our Default DHCP Options Set


#### 0 VPN CONNECTIONS
- No Customer Gateways Defined
- No Virtual Private Gateways Defined
- No VPN Connections Defined

#### 0 ELASTIC IPs
- No Elastic IP Addresses

#### 0 ENDPOINTS
- No Endpoints Defined

### STEP 13: EXPLORE: EC2 DASHBOARD
- Not much to see here… yet, just the Default Security Group.


### STEP 14: CREATE A KEY PAIR
This will be the key that we use to SSH into any new EC2 Instances which are provisioned under our account.  

#### TIP
It is often helpful to have a single SSH Key that our Engineers and scripts use to SSH into new Hosts as they are initially provisioned

- From the EC2 Dashboard Select Key Pairs under Network & Security
- KeyPair Name: &lt;domain name&gt; (e.g. copyleft)
- Click Create
- A New PEM Key (copyleft.pem) is downloaded your local machine
- Store this PEM Key in your .ssh/ directory we will be using it soon!


## Summary
- We’ve Created an AWS Account using our Admin Account
     - We’ve Reviewed the Billing Dashboard (currently $0)
     - Basic Account Mgmt Details and Security Setup
- We’ve Implemented IAM Users and Security Groups
     - AWS Console Access for our Users (Custom URL)
- We’ve Created our First IAM User Account and Downloaded our Credentials
     - Access Key ID
     - Secret Key
- We’ve Explored our Default VPC and EC2 Setup
     - We’ve use the Console to Update Names / Tags on some of the Default Resources in US-EAST-1 Region
     - Note: This same default setup exists in every region.  (Check it out)
- We’ve Created a KEY PAIR that our Team will use for Provisioning
- Ok, we’re all set up for now… let’s move on!
