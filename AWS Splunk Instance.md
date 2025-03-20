# Splunk Home Lab on AWS

This repository documents my journey setting up a personal Splunk home lab on an AWS Lightsail instance. It's designed for learning Splunk and experimenting with data analysis.

## Objectives

* Gain hands-on experience with Splunk Enterprise installation and configuration.
* Learn to ingest and analyze various data sources using Splunk.
* Develop skills in creating Splunk dashboards and alerts.
* Explore Splunk's search processing language (SPL).
* Understand basic Splunk administration and maintenance.
* Document the process and best practices for future reference.
* Improve AWS Lightsail management skills.

## Skills Learned

* **AWS EC2 Management:**
    * Launching and configuring Lightsail instances.
    * Managing security groups and key pairs.
    * SSH access and basic Linux administration.
* **Splunk Enterprise Installation and Configuration:**
    * Downloading and installing Splunk on a Linux server.
    * Starting and stopping Splunk services.
    * Enabling boot start.
    * Basic Splunk configuration.
* **Data Ingestion:**
    * Adding data sources to Splunk.
    * Understanding different data input methods.
* **Splunk Search Processing Language (SPL):**
    * Writing basic and advanced Splunk searches.
    * Using SPL commands for data manipulation and analysis.
* **Dashboard Creation:**
    * Building interactive dashboards to visualize data.
    * Creating custom charts and visualizations.
* **Alerting:**
    * Setting up alerts to monitor critical events.
    * Configuring alert actions.
* **Splunk Administration:**
    * Basic user management.
    * Understanding Splunk's file structure.
* **Documentation:**
    * Documenting setup and configuration steps.
    * Creating clear and concise documentation.
* **Troubleshooting:**
    * Diagnosing and resolving Splunk installation and configuration issues.
    * Debugging SPL queries.

## Prerequisites

* **AWS Account:** You'll need an active AWS account.
* **Linux EC2 Instance:** An EC2 instance running a recent AWS Linux AMI.
* **SSH Access:** Secure Shell access to your EC2 instance.
* **Linux Command Line Familiarity:** Basic knowledge of Linux commands.

## Setup Steps

### Step 1: Prepare the AWS Linux Instance

1.  **Launch EC2 Instance:**
    * Launch a new EC2 instance in your AWS account.
    * Choose a recent Amazon Linux AMI (e.g., Amazon Linux 2 or Amazon Linux 2023).
    * Select an instance type suitable for your needs (t2.medium or larger recommended).
    * Configure security groups to allow SSH (port 22) and HTTP (port 8000) traffic.
    * Create or use an existing key pair for SSH access.
2.  **Connect via SSH:**
    * Use your SSH client to connect to the public IP address of your EC2 instance.

### Step 2: Download Splunk Enterprise

1.  **Navigate to /opt:**
    ```bash
    sudo su - # become root
    cd /opt/
    ```
2.  **Download Splunk:**
    * Replace the version and build with the latest Splunk Enterprise download link from the Splunk website.
    ```bash
    wget -O splunk-9.0.1-82c987350fde-Linux-x86_64.tgz "[https://download.splunk.com/products/splunk/releases/9.0.1/linux/splunk-9.0.1-82c987350fde-Linux-x86_64.tgz](https://download.splunk.com/products/splunk/releases/9.0.1/linux/splunk-9.0.1-82c987350fde-Linux-x86_64.tgz)"
    ```
3.  **Extract Splunk:**
    ```bash
    tar xvzf splunk-9.0.1-82c987350fde-Linux-x86_64.tgz
    ```

### Step 3: Install Splunk

1.  **Navigate to the Splunk bin directory:**
    ```bash
    cd splunk/bin
    ```
2.  **Start Splunk Installation:**
    ```bash
    ./splunk start --accept-license
    ```
    * You'll be prompted to create an administrator username and password. **Remember these credentials!**
3.  **Enable Boot Start:**
    ```bash
    ./splunk enable boot-start
    ```

### Step 4: Access Splunk Web Interface

1.  **Open Web Browser:**
    * Open your web browser and navigate to `http://<your-instance-public-IP>:8000`.
2.  **Login:**
    * Log in with the username and password you created during installation.

### Step 5: Start Exploring

1.  **Add Data:**
    * Begin adding data sources to Splunk. You can start by monitoring system logs, application logs, or other data sources.
2.  **Experiment:**
    * Explore Splunk's search capabilities, create dashboards, and set up alerts.
3.  **Document your findings:**
    * This repository will be used to document my findings, configurations, and experiments.

## Security Considerations

* **Security Groups:** Ensure your EC2 security groups are configured to allow only necessary traffic.
* **Strong Passwords:** Use strong, unique passwords for your Splunk administrator account.
* **Regular Updates:** Keep your Splunk installation and EC2 instance up to date with the latest security patches.
* **Restrict Access:** If this is a publicly accessible instance, consider implementing additional security measures, such as IP address restrictions or VPN access.
* **HTTPS:** For production or sensitive data, configure Splunk to use HTTPS.

## Future Enhancements

* **Data Ingestion:** Explore different methods for ingesting data into Splunk, such as forwarders and APIs.
* **Apps and Add-ons:** Install Splunk apps and add-ons to extend functionality.
* **Clustering:** Investigate Splunk clustering for high availability and scalability.
* **Alerting:** Set up custom alerts to monitor critical events.
* **Dashboards:** Create custom dashboards to visualize data and gain insights.
* **Version Control:** Track Splunk configuration changes using version control.
* **Automation:** Automate Splunk deployment and configuration using tools like Ansible or Terraform.
* **Cost Optimization:** Monitor AWS cost and optimize instance size based on usage.

## Contributing

Feel free to contribute to this repository by submitting pull requests or opening issues.
