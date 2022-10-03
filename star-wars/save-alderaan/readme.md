#### * Note: It's better to learn by doing. For a more rewarding learning experience, try to use your own resources (a.k.a Google) to accomplish the requirements under [Create](https://github.com/juamatx/instructions/edit/main/star-wars/save-alderaan/readme.md#Create) . You can use this page to verify your final results. You will need to copy [User Data Script](https://github.com/juamatx/instructions/edit/main/star-wars/save-alderaan/readme.md#user-data-script) for the EC2 instance in us-east-1, the rest is wicked easy!

# Create: 
- 1 EC2 instance (us-east-1)
  - web server
- 1 EC2 instance (us-west-1)


## EC2 instance (us-east-1)

*This instance will host the web server.

- To start, open the EC2 page and click on "Launch Instances". Make sure to be in the **"us-east-1"** region.

<img width="323" alt="image" src="https://user-images.githubusercontent.com/60664640/193567362-0e70dd33-6349-46ba-8c4c-0e4b17b5bfd2.png">



#### Leave everything as default, only change the following:

- **Name:** The instance name can be anything you want, for this example it will be "Alderaan".

- **Key pair:** Typically, we create a key pair to connect to the instance but for this example we won't need to. Choose "proceed without a key pair"

<img width="590" alt="image" src="https://user-images.githubusercontent.com/60664640/193573655-4cde75b4-6442-4bfc-b25a-cc41c53a378c.png">


- **Network settings:** a new  security group will be created, only check "Allow HTTP traffic from the internet". Why not HTTPS? our server will be only using HTTP. HTTPS requires a more involved setup. Typically we'd want security groups to be more strict and specific, but we will keep it minimal for the sake of simplicity

<img width="594" alt="image" src="https://user-images.githubusercontent.com/60664640/193574096-ed7a903c-da0b-4564-bf8e-da20c93a0d68.png">

- **Advanced details:** paste the script below to the "User data" box. Then, "Launch Instance"

### User Data Script
This command script will run when the instance launches. Adding a script helps automate tasks to run before even connecting to the server (e.g. install software updates, change settings, add data/directories, etc)

This script will do the following:
 - Install updates
 - Install software to host a website (apache HTTP server)
 - Copy the home page of the website (a list of Rebel Alliance Bases)
```
#!/bin/bash
yum update -y
yum install -y httpd
systemctl start httpd
systemctl enable httpd
echo "<h1>
TOP SECRET
</h1>
<h2>Rebel Alliance Bases:</h2>

<ul>
<li>Dantooine</li>
<li>Yavin 4</li>
<li>Mako-Ta</li>
<li>Clabburn Range</li>
<li>5251977</li>
</ul>" > /var/www/html/index.html
```

### Did it work?
After a few minutes, your instance should be ready to go. You should be able to access your server's web page by selecting your ec2 instance > opening the "details" tab > copy either the "Public IPv4 DNS" or "Public IPv4 address" and paste it in your browser's search bar. You should see the website below!

<img width="320" alt="image" src="https://user-images.githubusercontent.com/60664640/193589447-df3e060c-fc59-4759-8487-49e645ef8221.png">


## EC2 instance (us-west-1)

Time to build the second server. This server won't be hosting anything initially.

Make sure to switch regions to **us-west-1**

<img width="389" alt="image" src="https://user-images.githubusercontent.com/60664640/193585419-35d972ff-0ec7-46ff-b490-1a755e057cf5.png">

Follow the same steps as before. The only exception :
- 🔄 Pick a different name. I will use "Dantooine"
- ❌ No need for the "User data" script

### We now have 2 instances running
1. Alderaan in **us-east-1** (web server)
2. Dantooine in **us-west-1**

#### ⚠️ when the tutorial is over, make sure to "Terminate" both instances
<img width="235" alt="image" src="https://user-images.githubusercontent.com/60664640/193592870-b716c4ac-7f51-439a-ad72-d6d5b4a59653.png">
