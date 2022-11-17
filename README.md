Deploying an EC2 instance to run a streamlit DAPP
===================================

## Step 1: Launch an instance<a name="ec2-launch-instance"></a>

You can launch a Linux instance using the AWS Management Console as described in the following procedure\. This tutorial is intended to help you quickly launch your first instance, so it doesn't cover all possible options\. For information about advanced options, see [Launch an instance using the new launch instance wizard](ec2-launch-instance-wizard.md)\. For information about other ways to launch your instance, see [Launch your instance](LaunchingAndUsingInstances.md)\.

**To launch an instance**

1. Open the Amazon EC2 console at [https://console\.aws\.amazon\.com/ec2/](https://console.aws.amazon.com/ec2/)\.

1. From the EC2 console dashboard, in the **Launch instance** box, choose **Launch instance**, and then choose **Launch instance** from the options that appear\.

1. Under **Name and tags**, for **Name**, enter a descriptive name for your instance\.

1. Under **Application and OS Images \(Amazon Machine Image\)**, do the following:

   1. Choose **Quick Start**, and then choose Amazon Linux\. This is the operating system \(OS\) for your instance\.

   1. From **Amazon Machine Image \(AMI\)**, select an HVM version of Amazon Linux 2\. Notice that these AMIs are marked **Free tier eligible**\. An *Amazon Machine Image \(AMI\)* is a basic configuration that serves as a template for your instance\.

1. Under **Instance type**, from the **Instance type** list, you can select the hardware configuration for your instance\. Choose the `t2.micro` instance type, which is selected by default\. The `t2.micro` instance type is eligible for the free tier\. In Regions where `t2.micro` is unavailable, you can use a `t3.micro` instance under the free tier\. For more information, see [AWS Free Tier](https://aws.amazon.com/free/)\.

1. Under **Key pair \(login\)**, for **Key pair name**, choose the key pair that you created when getting set up\.
**Warning**  
Do not choose **Proceed without a key pair \(Not recommended\)**\. If you launch your instance without a key pair, then you can't connect to it\.

1. Next to **Network settings**, choose **Edit**\. For **Security group name**, you'll see that the wizard created and selected a security group for you\. You can use this security group, or alternatively you can select the security group that you created when getting set up using the following steps:

   1. Choose **Select existing security group**\.

   1. From **Common security groups**, choose your security group from the list of existing security groups\.

1. Keep the default selections for the other configuration settings for your instance\. 

1. Review a summary of your instance configuration in the **Summary** panel, and when you're ready, choose **Launch instance**\.

1. A confirmation page lets you know that your instance is launching\. Choose **View all instances** to close the confirmation page and return to the console\.

1. On the **Instances** screen, you can view the status of the launch\. It takes a short time for an instance to launch\. When you launch an instance, its initial state is `pending`\. After the instance starts, its state changes to `running` and it receives a public DNS name\. If the **Public IPv4 DNS** column is hidden, choose the settings icon \( ![\[Image NOT FOUND\]](http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/images/settings-icon.png) \) in the top\-right corner, toggle on **Public IPv4 DNS**, and choose **Confirm**\.

1. It can take a few minutes for the instance to be ready for you to connect to it\. Check that your instance has passed its status checks; you can view this information in the **Status check** column\.

## Step 2: Connect to your instance<a name="ec2-connect-to-instance-linux"></a>

There are several ways to connect to your Linux instance\. For more information, see [Connect to your Linux instance](AccessingInstances.md)\.

**Important**  
You can't connect to your instance unless you launched it with a key pair for which you have the `.pem` file and you launched it with a security group that allows SSH access from your computer\.

1. On EC2 dashboard, click on the instance ID to view the instance details. Copy the IP address of the EC2 instance (IPv4 Public IP).

2. Next Open your terminal

3. Then paste it in the Host Name box after typing “ec2-user@” as below:

4. Then select Connection -> SSH -> Auth -> Browse and upload the ppk file.

5. Do not click on “Open” yet. The next step is to give your session a name. Click on “Session” and type the name in the “Saved Sessions” box and save it.

6. Now we can click on “Open” to connect to the instance.


## Step 3: Upload the source code and dependencies on the instance.

1. This EC2 instance has Python 2.7 pre-installed but we need Python 3.6 or a later version for Streamlit. The following command will install Python 3.

```
sudo yum install python3
```

2. We will clone the source code from a Github repository so we will install git.

```
sudo yum install git
```

3. We can now clone the repository in our EC2 instance. Copy the address of the repository:

Then paste it in the terminal after “git clone”:
```
git clone git@github.com:cbent28/Streamlit_DAPP_on_EC2.git
```

4. Navigate to the repository in your terminal.

5. The next step is to install the dependencies:

```
sudo python3 -m pip install streamlit
sudo python3 -m pip install pandas
sudo python3 -m pip install pandas-datareader
```

Since this is a simple app, we do not have many dependencies.

The source code is saved in the app.py file. You can view the files in the repository by typing “ls” in the terminal.

6. We can now run the app with the following commands:

```
streamlit run app.py
```


Congragulations! Our app is running on an EC2 instance and can be accessed from any where through a web browser.

Enter the external URL in your web browser and you will see the app is running!
