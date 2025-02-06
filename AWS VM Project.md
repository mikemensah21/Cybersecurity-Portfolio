# Creating a Personal Virtual Machine on AWS

This lab guides you through creating a personal virtual machine (VM) on Amazon Web Services (AWS) using the EC2 (Elastic Compute Cloud) service.  We'll cover launching an instance, connecting to it, and basic security best practices.

## Prerequisites

* An AWS account. If you don't have one, you can create one [here](https://aws.amazon.com/).  Be aware of AWS's free tier offerings, which may cover some of the costs associated with this lab (but not necessarily all).
* A basic understanding of cloud computing concepts.
* An SSH client (e.g., PuTTY on Windows, Terminal on macOS/Linux).

## Steps

### 1. Launching an EC2 Instance

1. **Log in to the AWS Management Console:** Go to [https://aws.amazon.com/console/](https://aws.amazon.com/console/) and log in with your credentials.

2. **Navigate to EC2:**  You can search for "EC2" in the services search bar or find it in the list of services.

3. **Launch Instances:** Click the "Launch Instances" button.

4. **Choose an Amazon Machine Image (AMI):**  An AMI is a template that defines the operating system and other software that will be installed on your instance.  For this lab, choose a suitable AMI.  Amazon Linux or Ubuntu Server are good choices.  Consider the "Free tier eligible" filter if you're concerned about costs.

5. **Choose an Instance Type:** This determines the hardware resources allocated to your VM (CPU, memory, storage).  `t2.micro` (or `t3.micro` if available) instances are typically sufficient for personal use and often fall within the free tier.

6. **Configure Instance Details:**  You can usually leave most of these settings at their defaults for a basic setup.  However, you might want to configure:
    * **Networking:**  Ensure the instance is launched in a public subnet if you want to access it from the internet.
    * **IAM role:**  (Optional but recommended)  Create an IAM role with appropriate permissions and associate it with the instance. This is a best practice for security.
    * **User data:** You can use this field to run commands when the instance starts.  This is useful for automating initial setup tasks.

7. **Add Storage:** The default storage is usually sufficient. You can increase the size if needed.  Consider using EBS (Elastic Block Store) volumes for persistent storage.

8. **Add Tags (Optional):**  Tags are key-value pairs that help you organize your resources.  Add a tag like `Name: MyPersonalVM` to easily identify your instance.

9. **Configure Security Group:**  A security group acts as a virtual firewall for your instance.  It's *crucial* to configure this correctly.
    * **Create a new security group:** Give it a descriptive name (e.g., `MyPersonalVM-SG`).
    * **Inbound Rules:**
        * **SSH (Port 22):**  Allow SSH access.  For initial setup, you might allow SSH from your IP address (or a specific range).  **For production, restrict SSH access as much as possible.**  Consider using a bastion host or AWS Systems Manager Session Manager for more secure access.
        * **HTTP/HTTPS (Ports 80/443):** If you plan to host a web server, open these ports.
        * **Other Ports:** Open any other ports required by your applications.
    * **Outbound Rules:** The default outbound rules usually allow all traffic, which is generally fine for personal VMs.

10. **Review and Launch:**  Review your instance configuration and click "Launch."  You'll be prompted to select or create a key pair.  **Download the private key file (.pem) and store it securely.**  You'll need it to connect to your instance.

### 2. Connecting to Your Instance

1. **Using SSH (Linux/macOS):**
    ```bash
    chmod 400 your-key-pair.pem  # Set permissions on the key file
    ssh -i your-key-pair.pem ec2-user@your-instance-public-dns  # Replace with your key file and instance's public DNS
    ```
    Replace `your-key-pair.pem` with the path to your downloaded key file and `your-instance-public-dns` with the public DNS name or IP address of your EC2 instance (found in the EC2 console).  The default username for Amazon Linux is `ec2-user`, and for Ubuntu it's `ubuntu`.

2. **Using PuTTY (Windows):**
    * Convert the .pem file to a .ppk file using PuTTYgen.
    * Open PuTTY and enter the public DNS name or IP address of your instance.
    * In the SSH settings, browse to your .ppk file.
    * Connect!

### 3. Basic Security Best Practices

* **Keep your instance updated:** Regularly run system updates (e.g., `sudo yum update` on Amazon Linux, `sudo apt update && sudo apt upgrade` on Ubuntu).
* **Use strong passwords:**  If you create any user accounts, use strong, unique passwords.
* **Restrict SSH access:** As mentioned earlier, restrict SSH access to only necessary IP addresses or use more secure methods like a bastion host or Session Manager.
* **Enable a firewall:**  Use a firewall like `iptables` (Linux) to further control inbound and outbound traffic.
* **Monitor your instance:** Use CloudWatch to monitor your instance's performance and security.
* **Regularly back up your data:**  Use EBS snapshots or other backup solutions.
* **Terminate unused instances:**  Stop or terminate instances when you're not using them to avoid unnecessary charges.

## Conclusion

This lab provides a basic introduction to creating a personal VM on AWS.  Remember to explore the AWS documentation for more advanced configurations and security best practices.  This is just the beginning of what you can do with EC2!
