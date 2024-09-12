Go to AWS console and creat an EC2 instance.
SSH into your Instance and Update your Linux Machine.
install Java,Jenkins,Docker,Git,AWSCLI on your machine via input to the userdata or bash scripting with the vi command into your machine.
Access the jenkins browser using https//:<Instance_ip>:8080
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
When you password comes up copy and paste to your browser to loggin
Create your Jenkins user and after the configuration is complete you should see your dashboard
# aws-ECR-node-jenkins
a project installing nodejs on jenkins and pushing it to aws-ECR
# nod-jenkins
a node-jenkis project  running it on a jenkins server
STEPS
Add AWS credentials in Jenkins
We may also set up AWS credentials in Jenkins so that it facilitates the Docker push to the ECR repository.

GO to the Manage Jenkins>>Credentials>>>>Add credentials>>Global


Then add credentials and here add AWS username and password and account ID


STEP #2
Installing plugins in Jenkins
Now go to manage Jenkins go to plugins 

-Click on available plugins

-Search for nodejs and install

-Go to tools and search nodes installation and add node (in the textbox)

And save 

-now go back to manage Jenkins and click on available pluggins

Go to the manage Jenkins>>Plugins>>Available Plugin>>search for the pluggins below and install

Docker
Docker Pipeline
Amazon ECR plugin



Now go to github and create a new project call it aws-ECR-node-jenkins

Enter description of your choice and add Readme and create the project 

Now clone the project to your vscode

-Now in vscode change directory to the project 

-create index.js ,Dockerfile, .gitignore , .dockerignore , jenkinsfile (take sample contents from last node project but make sure its on port 3000 for both Dockerfile and the application index.js)


Edit your jenkinsfile to reflect  the new pipeline for this project


#Now run the following commands
node v

npm init -y

npm install express

# check if the application is working

By running the command below

node index.js

Check on the browser

localhost:3000

NOTE: if u dont run the above commands the localhost wont work on the browser
#If it works then 

‘Press control c

And push all files to GitHub


STEP #4
CREATING IN AWS YOUR ECR AND IAM ROLE

-search for ECR
-create repository
-private
-type repository name
-create repository(optional:after the ECR has being created you can view your push commands)

CREATE IAM ROLE
search for IAM
-Roles
-create roles
-Aws service
-Service or use case
-EC2
-Next
-Add permissions
-Amazon EC2 Container Registry Full Access(check it)
-Next
-Role details
-Role name(type a role name)
-create role

STEP #5
-Now go back to EC2 instance
-click on the instance
-Actions
-security
-modify IAM role
-IAM role click on the drop down
-select ECR role
-update IAM role


STEP #6
Install AWS CLI on Ubuntu machine on vscode

curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip 
sudo ./aws/install

STEP #7
Now go back to jenkins dashboard

-Click New item

-enter pipeline  project name

-Check github project and 

-Enter project url  you clone from  GitHub the new project you just created and add / after it

- click on script drop down and select 
-pipeline script
-write your pipeline or copy and paste from the modified jenkinsfile on vscode

-APPLY and SAVE
BUILD NOW

ISSUES ENCOUNTERED
Check if the project its on master or main branch(main triggered error despite the fact my github was on MAIN till i switched to MASTER)

NOTE:if you encounter an error when you build and your console output displays 
ERROR: permission denied while trying to connect to the Docker daemon socket at unix:///var/run/docker.sock: Get "http://%2Fvar%2Frun%2Fdocker.sock/_ping": dial unix /var/run/docker.sock: connect: permission denied

SOLUTION
on vscode ssh to your ec2 instance jenkins server and run the following commands

newgrp docker

 #is used to grant full read, write, and execute permissions to all users for the Docker socket file, which allows unrestricted access to the Docker daemon # and is a significant security risk.

sudo chmod 777 /var/run/docker.sock    

