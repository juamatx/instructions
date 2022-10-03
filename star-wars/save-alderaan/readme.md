#### * Note: It's better to learn by doing. For a more rewarding learning experience, try to use your own resources (a.k.a Google) to accomplish the requirements under [Create](https://github.com/juamatx/instructions/edit/main/star-wars/save-alderaan/readme.md#Create) . You can use this page to verify your final results. You will need to copy [User Data Script](https://github.com/juamatx/instructions/edit/main/star-wars/save-alderaan/readme.md#user-data-script) for the EC2 instance in us-east-1, the rest is wicked easy!

# Create: 
- 1 EC2 instance (us-east-1)
  - web server
- 1 EC2 instance (us-west-1)


## EC2 instance (us-east-1)
```
Name: Alderaan
Key Pair: Proceed without a key pair
```

* This instance will host the web server.

- To start, open the EC2 page and click on "Launch Instances". Make sure to be in the **"us-east-1"** region.

<img width="323" alt="image" src="https://user-images.githubusercontent.com/60664640/193567362-0e70dd33-6349-46ba-8c4c-0e4b17b5bfd2.png">


We are leaving most items as default, the following steps include only what needs to change:

- Typically, we create a key pair to connect to the instance but for this example we won't need to.

<img width="590" alt="image" src="https://user-images.githubusercontent.com/60664640/193573655-4cde75b4-6442-4bfc-b25a-cc41c53a378c.png">


User data. This is a command script will run when the instance launches. This is helpful because we can add software updates or change specific settings before we even connect to the server.

- Under network settings a new group will be created, only check "http access". why not https? our server will be only using http. https requires a more involved setup. Typically we'd want security groups to be more strict and specific, but we will keep it minimal for the sake of simplicity

<img width="594" alt="image" src="https://user-images.githubusercontent.com/60664640/193574096-ed7a903c-da0b-4564-bf8e-da20c93a0d68.png">

- Lastly, under advanced details, copy the script below in the "User data" box.


## User Data Script

This script will do the following:
 - Installing updates
 - Installing software to host a website (apache http server)
 - Copying the home page of the website (a list of Rebel Alliance Bases)
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
