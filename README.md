# Terraform-

> This space will keep on updating, so check this regularly for an update
Download Terraform from official site
https://www.terraform.io/downloads.html

Set Up patch variable for this as per doc and check your tf version

![tf1](https://user-images.githubusercontent.com/51450944/87386428-74826b00-c56e-11ea-9896-559576d5752e.PNG)

Create a terraform user to integrate AWS with terraform. I have  created a user terraform.
![tf2](https://user-images.githubusercontent.com/51450944/87386444-7d733c80-c56e-11ea-9c99-0185dfacf0a9.PNG)

Provide Administrator access policy to this user
![tf3](https://user-images.githubusercontent.com/51450944/87386446-7d733c80-c56e-11ea-8fd5-a3850298368e.PNG)

Download Access key id. Create a credential in order to authenticate with AWS by default.
![tf4](https://user-images.githubusercontent.com/51450944/87386447-7d733c80-c56e-11ea-8b1f-e7abe59fa5e5.PNG)

Create a .aws folder inside the user folder and save your cred.(You can choose any other folder)
Save your cred inside the c\users\username\.aws  
![tf5](https://user-images.githubusercontent.com/51450944/87386448-7d733c80-c56e-11ea-9bad-408420539b71.PNG)

I’ll use Git here to integrate terra with AWS so ensure you have Git installed to follow along. You can also use other command line as well to work with.Create a folder & Initialize your git repos
![tf6](https://user-images.githubusercontent.com/51450944/87386449-7e0bd300-c56e-11ea-99c5-7de4f3e63697.PNG)

Create a file and add the below tf code to create a bucket in aws.
![tf7](https://user-images.githubusercontent.com/51450944/87386450-7e0bd300-c56e-11ea-8cf5-2fa1f21ea42f.PNG)

> provider "aws" {     # Terraform is used to create, manage, and update infrastructure resources such as physical machines, VMs, network switches, containers, and more. Almost any infrastructure type can be represented as a resource in Terraform.

A provider is responsible for understanding API interactions and exposing resources. Providers generally are an IaaS (e.g. Alibaba Cloud, AWS, GCP, Microsoft Azure, OpenStack), PaaS (e.g. Heroku), or SaaS services (e.g. Terraform Cloud, DNSimple, Cloudflare).

  profile = "default" # this is your default profile to authenticate to aws using your saved cred
  region = "us-west-2"
}

resource "aws_s3_bucket" "tf_course" {  # what resources you are using need to be place here. in this ex s3. resource name is tf_course this is how terraform define
  bucket = "tf-aws-june28" # this is consider as arguments in terraform and we use this in "". this is how aws define this name
  acl    = "private" # an argument to define it is a private bucket
}


Use git add to add this file in local git repo

Commit your repo using git commit and it it ask for id provide your github account details
![tf8](https://user-images.githubusercontent.com/51450944/87386451-7e0bd300-c56e-11ea-85b2-3078bdfce36f.PNG)
\
Initialize your tf directory.
Once initialize we are ready to deploy our code to aws
![tf9](https://user-images.githubusercontent.com/51450944/87386452-7e0bd300-c56e-11ea-8c2b-2607f69a05f1.PNG)

Now use **terraform apply**. This will ask you to complete the changes on AWS, put yes, if you don’t want this to ask you yes or no, you can simply write in the beginning as

![tf10](https://user-images.githubusercontent.com/51450944/87386475-89f79500-c56e-11ea-90a2-956c9740e1c1.PNG)

Terraform apply -auto-approve

![tf11](https://user-images.githubusercontent.com/51450944/87386476-89f79500-c56e-11ea-9e3c-c1b4187f433f.PNG)

As soon as you hit yes within a sec this will deploy a bucket in your aws console
![tf12](https://user-images.githubusercontent.com/51450944/87386477-89f79500-c56e-11ea-9bf7-678ca1229e22.PNG)

Login and check in your console

![tf13](https://user-images.githubusercontent.com/51450944/87386478-89f79500-c56e-11ea-95b4-5bbf4a5bc316.PNG)

You can also save this plan to a file to see what exactly it is going to do

Use terrafor show command to check the result

![tf14](https://user-images.githubusercontent.com/51450944/87386479-8a902b80-c56e-11ea-8a0f-594c50482778.PNG)

Terraform graph - so i have one S3 bucket in my account and lets see what we get when we generate the graph for it

![tf15](https://user-images.githubusercontent.com/51450944/87386480-8a902b80-c56e-11ea-9d45-a52ea099550b.PNG)

How does TF work  ?

IaC - This is an Infrastructure as Code. We can define resources based on tf code. You can build your infrastructure using a code, share it with others. You need to plan your execution well.
**Resources** - Building blocks of Terraform code
Define the “what” of your infrastructure
Different settings for every provider like (AWS,Azure,GCP etc..)

**Code> State> Plan > Apply**    =  Always remember this.

**Terraform plan --help** = this will give you what options we can use with plan

![tf16](https://user-images.githubusercontent.com/51450944/87386481-8a902b80-c56e-11ea-8cb3-714aead347bd.PNG)


As we have destroyed our previous bucks env, Now lets add VPC in our tf code 
Create a new prod .tf file and add below
![tf17](https://user-images.githubusercontent.com/51450944/87386482-8a902b80-c56e-11ea-91b5-6168c7c4b050.PNG)


Use terraform plan to see what it is going to do. As you can see using plan we can see this is going to create a default vpc
![tf18](https://user-images.githubusercontent.com/51450944/87386483-8a902b80-c56e-11ea-811c-f7fa2ee7ab1d.PNG)

Add this file using git add prod.tf command
![tf19](https://user-images.githubusercontent.com/51450944/87386486-8b28c200-c56e-11ea-8cdd-5ef84be149dd.PNG)

> And use git status to trak the file. As you can see git has found the previous .tf file has been deleted so we need to use git add firs_code.tf to add this file to repo

![tf20](https://user-images.githubusercontent.com/51450944/87386487-8b28c200-c56e-11ea-8bd6-acebb890c774.PNG)

Now you can use git commit command to add the vpc  changes to it.
![tf21](https://user-images.githubusercontent.com/51450944/87386492-8fed7600-c56e-11ea-8dd8-89d104a25fa4.PNG)

> this is it now new bucket deployed under default vpc.

















