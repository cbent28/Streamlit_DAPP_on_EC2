# Streamlit_DAPP_on_EC2
Deploying a Data App on AWS for Free
Let others have access to your data app in no time

Photo by Austin Distel on Unsplash
In an earlier post, we created a data app with Python and Streamlit. It only worked in the local machine so other people could not use it.

In this post, we will run our data app on an AWS EC2 instance so that other people can have access to it.

We just need to create a free tier account on AWS. It is very simple to create and we won’t be charged a dime if we stay within the limits of the free tier. The scope of the free tier is more than enough for learning purposes.

If you already have an AWS account or just created a free tier one, we are ready to start.

The outline of the post:

Creating an EC2 instance
Connecting to the EC2 instance (Linux, Mac, and Windows)
Running the app on the EC2 instance
Creating an EC2 instance
We need to open up the EC2 dashboard on AWS management console.


(image by author)
On the EC2 dashboard, scroll down a little and click on Launch Instance.


(image by author)
We first need to choose an Amazon Machine Image (AMI) which provides the information required to launch an instance. AMI contains the software configuration (i.e. operating system) and some pre-installed software packages.

There are many options for AMI. We will select the first one which is Amazon Linux 2.


(image by author)
You can select a different one but make sure it is free tier eligible.

The next step is to select the instance type. There is one that is eligible for free tier.


(image by author)
The next step is configuring the instance details but we can leave it with the default option. We can also skip the next two items which are “add storage” and “add tags”. The default storage option is enough.

The next step is configuring the security group. It can be considered as an instance-level firewall. Thus, it manages the traffic into and out of the instance.

We will add 2 new rules as below:


(image by author)
We will then review and launch. The final step is creating a key pair. Make sure you create a key pair and download it. We will need it to connect to the instance.


(image by author)
After downloading the key pair (.pem file), we can launch the instance. The instance will be ready in a few minutes and we can view it on the EC2 dashboard.

Connecting to the EC2 Instance
I’m currently using a windows computer so I will show you how to connect to the instance from a windows machine.

The connection procedure is much simpler if you use Linux or Mac. In fact, the steps are explicitly explained by AWS. On the EC2 dashboard, select your instance and click on “Connect”. A new page with instructions will be opened up:


(image by author)
Let’s go back to our windows machine case. We will use PuTTY which is a free SSH client for windows. You can download it from putty.org.

The first step is to create a ppk file using the key pair (pem file) we downloaded when launching the instance.

From the menu under PuTTY, open up PuTTYGen. Click on “Load” and then select the pem file.


(image by author)
Then click on “Save private key” to save the generated ppk file.


(image by author)
We now have the ppk file we need. For the next step, we will open up “PuTTY” from the menu under PuTTY.

On EC2 dashboard, click on the instance ID to view the instance details. Copy the IP address of the EC2 instance (IPv4 Public IP).


(image by author)
Then paste it in the Host Name box after typing “ec2-user@” as below:


(image by author)
Then select Connection -> SSH -> Auth -> Browse and upload the ppk file.


(image by author)
Do not click on “Open” yet. The next step is to give your session a name. Click on “Session” and type the name in the “Saved Sessions” box and save it.


(image by author)
Now we can click on “Open” to connect to the instance.


(image by author)
We are now connected to our instance. Putty will open up a terminal as below:


(image by author)
Running the app on EC2 instance
We are ready to upload the source code and dependencies on the instance.

This EC2 instance has Python 2.7 pre-installed but we need Python 3.6 or a later version for Streamlit. The following command will install Python 3.

sudo yum install python3
We will clone the source code from a Github repository so we will install git.

sudo yum install git
We can now clone the repository in our EC2 instance. Copy the address of the repository:


(image by author)
Then paste it in the terminal after “git clone”:

git clone https://github.com/SonerYldrm/stock-prices-app.git
Enter the repository:

cd stock-prices-app
The next step is to install the dependencies:

'''
sudo python3 -m pip install streamlit
sudo python3 -m pip install pandas
sudo python3 -m pip install pandas-datareader
Since this is a simple app, we do not have many dependencies.
'''

The source code is saved in the st1.py file. You can view the files in the repository by typing “ls” in the terminal.

We can now run the app with the following commands:

streamlit run st1.py

(image by author)
Congragulations! Our stock price data app is running on an EC2 instance and can be accessed from any where through a web browser.

Enter the external URL in your web browser and you will see the app is running. Here is a short screen recording of the app saved in a web browser.

