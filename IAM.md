- - - 
### **IAM - Identity and Access Management**
- Global Service 

`Root Account` - created by default, shouldn't be shared/used
`Users` - people within the organization, can be grouped.

`Groups` contain only `users` and not other groups

![[Pasted image 20240807214306.png]]

**IAM : Permissions**

`users or groups` : can be assigned with policies 
- policies define what an user can access and what they can't 
- policies are written in JSON format 
- `least privilege principle` : don't give user more permission that a user needs. 

--- 

### **IAM - Policies**: 

![[Pasted image 20240807214920.png|500]]

IAM policy consists of 

`version`
`id` : policy id (optional)
`statement [{` : one or more statements 
- `sid`: statement id
- `effect` : allow/deny access
- `principle`: account/user to which the policy is applied to 
- `resource` : list of resource to which the policy is applied to 
`}]`

--- 

### **IAM Password Policy**

Strong password = high security
- include uppercase letters
- lowercase letters
- numbers
- special characters

Password expiration - requires users to change passwords after a certain period of time 

Prevent password re-use 

`MFA - Multi Factor Authentication `

- MFA = password you _know_ + device your _own_
- if password is hacked, the account is not compromised because the device is still required to login to the account. 

Examples of MFA options in AWS
1. google authenticator
2. authy
3. yubikey
4. hardware key fob 

--- 
### **AWS Access Keys, CLI**

Three ways a user can access AWS
1. AWS Management Console - protected by (password + MFA)
2. AWS Command Line Interface(CLI) - protected by access keys
3. AWS Software Development Kit (SDK) - protected by access keys

Access Keys are `secret` DON'T SHARE! 
- Access Keys ~= username
- Secret Access Keys ~= Password

AWS CLI
- tool that enables you to access AWS services using commands in command line interface. 
- alternate to AWS management console.

---

### **IAM Roles** 

- AWS services needs to perform actions on your behalf 
- we will assign permissions to AWS Services using `IAM Roles`

Common Roles
- EC2 Instance Roles
- Lambda Function Roles
- Roles for CloudFormation

![[Pasted image 20240807222925.png|200]] 

--- 
### **IAM Security Tools**

- IAM Credentials Report (account - level)
	- lists all your account's users and the status of their credentials 

- IAM Access Advisor (user - level)
	- shows permissions granted to the user and when those services were last accessed
	- used to keep the `least privilege principle` in check. 

--- 
![[Pasted image 20240807223947.png|500]]

---

Date : 07/08/2024
Vivek Malapaka

---

