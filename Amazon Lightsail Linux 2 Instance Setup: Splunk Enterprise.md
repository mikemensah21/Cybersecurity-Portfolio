# Amazon Lightsail Linux 2 Instance Setup: Splunk Enterprise

This repository provides a step-by-step guide on creating an Amazon Lightsail Linux 2 instance with specific resource configurations and connecting to it via the browser's SSH client.

## Prerequisites

* An active Amazon Web Services (AWS) account.

## Steps

1.  **Log in to the AWS Management Console:**
    * Navigate to the AWS Management Console: [https://aws.amazon.com/console/](https://aws.amazon.com/console/)
    * Log in with your AWS credentials.

2.  **Navigate to Amazon Lightsail:**
    * In the AWS Management Console search bar, type "Lightsail" and select "Lightsail."

3.  **Create a Lightsail Instance:**
    * Click on "Create instance."
    * **Instance location:** Select the AWS Region and Availability Zone that best suits your needs.
    * **Pick your instance image:**
        * Choose "Linux/Unix."
        * Select "Amazon Linux 2."
    * **Choose your instance plan:**
        * Select the instance plan with the following specifications:
            * 2 GB Memory
            * 2 vCPUs Processing
            * 60 GB SSD Storage
            * 3 TB Transfer
    * **Identify your instance:**
        * Enter "Splunk-Enterprise-Instance" as the instance name.
    * **Choose or create an SSH key pair:**
        * Lightsail will create a default key pair for your region. You can use it, or create your own. For this tutorial we will use the default.
    * Click "Create instance."
      
![Image](https://github.com/user-attachments/assets/61909858-d9e6-4780-b37d-be7decd87492)

![Image](https://github.com/user-attachments/assets/da9168ea-3cef-4f75-a477-1768cbedf5b6)

![Image](https://github.com/user-attachments/assets/c73c4872-7ec9-4081-92f9-e70cdce60f8e)


4.  **Wait for Instance Creation:**
    * The instance creation process will take a few minutes. You can monitor the progress in the Lightsail console.

5.  **Connect to the Instance via Browser-Based SSH:**
    * Once the instance status is "Running," click on the "Splunk-Enterprise-Instance" instance name.
    * On the instance management page, you'll see a section labeled "Connect."
    * Click the "Connect using SSH" button. This will open a browser-based SSH terminal directly in your web browser.
    * You are now logged into your "Splunk-Enterprise-Instance" via SSH.
  
![Image](https://github.com/user-attachments/assets/4b0d7859-02f1-4634-8a6d-0caaa7c4a1e1)

![Image](https://github.com/user-attachments/assets/a0b79dfc-9b53-42c2-9841-96dfaa996411)

## Next Steps (Optional)

* Install Splunk Enterprise: After connecting to the instance, you can proceed with installing Splunk Enterprise.
* Configure firewall rules within the lightsail networking section to allow appropriate ports for Splunk and other services.
* Create a static IP address to prevent the ip address from changing.
* Attach a static disk to the instance for additional storage.

## Important Notes

* Ensure that you understand the pricing associated with the selected Lightsail instance plan.
* For production environments, consider using a more robust security setup, including key-based authentication and firewall configuration.
* Always keep your instance updated with the latest security patches.
* Consider creating a snapshot of the instance after the base configuration is complete.

