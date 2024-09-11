Go to AWS console and creat an EC2 instance.
SSH into your Instance and Update your Linux Machine.
install Java,Jenkins,Docker,Git,AWSCLI on your machine via input to the userdata or bash scripting with the vi command into your machine.
Access the jenkins browser using https//:<Instance_ip>:8080
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
When you password comes up copy and paste to your browser to loggin
Create your Jenkins user and after the configuration is complete you should see your dashboard
Set up your AWS credentials in jenkins by going to Manage jenkins>credentials>system>global credentials
Then add credentials and add AWS username,password and Account ID
Since we have install docker in our userdate we need to give docker some permission
Go to Manage Jenkins>add plugging>select
Docker
Docker pluggin
Amazon ECR
Nodejs
Go to AWS ECR and creat a reprository to push image
Create an IAM Role with permission
Attach permission policies : AmazonEC2ContainerRegistryFullAccess
#Install AWS CLI on Ubuntu 22.04 LTS
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip 
sudo ./aws/install
go to jenkins dashboard and click New item select pipeline and paste code
then Build your pipeline as a script
Go to your AWS ECR to check if the Image has been pushed into your ECR repository.