# Splunk Deployment Lab Setup (AWS Lightsail SSH)

This guide outlines the steps to deploy a Splunk Enterprise instance on an AWS Lightsail instance, leveraging SSH for initial setup and systemd for service management.

## Prerequisites

* An active AWS account.
* An AWS Lightsail instance running a Linux distribution (e.g., Ubuntu, CentOS).
* SSH access to your Lightsail instance.

## Step 1: Initial Linux Configuration

1.  **Connect to your Lightsail instance via SSH.**

    ```bash
    ssh <username>@<lightsail_public_ip>
    ```

2.  **Set a password for your user (if needed).**

    ```bash
    sudo passwd <username>
    ```

3.  **Create a dedicated Splunk user.**

    ```bash
    sudo useradd splunk
    ```

4.  **Create the Splunk installation directory.**

    ```bash
    sudo mkdir /opt/splunk
    ```

## Step 2: Download and Install Splunk Enterprise

1.  **Navigate to the `/opt` directory.**

    ```bash
    cd /opt
    ```

2.  **Download the Splunk Enterprise package.**

    * Replace the URL with the latest Splunk Enterprise download link.
    * You can obtain the latest download link from the Splunk website.

    ```bash
    sudo wget -O splunk-9.0.0-6818ac46f2ec-Linux-x86_64.tgz "[https://download.splunk.com/products/splunk/releases/9.0.0/linux/splunk-9.0.0-6818ac46f2ec-Linux-x86_64.tgz](https://www.google.com/search?q=https://download.splunk.com/products/splunk/releases/9.0.0/linux/splunk-9.0.0-6818ac46f2ec-Linux-x86_64.tgz)"
    ```

3.  **Extract the Splunk Enterprise package.**

    ```bash
    sudo tar xvzf splunk-9.0.0-6818ac46f2ec-Linux-x86_64.tgz -C /opt
    ```

4.  **Change the ownership of the Splunk directory to the `splunk` user.**

    ```bash
    sudo chown -R splunk:splunk /opt/splunk
    ```

## Step 3: Enable Boot Start with Systemd

1.  **Switch to the `splunk` user.**

    ```bash
    sudo su splunk
    ```

2.  **Navigate to the Splunk `bin` directory.**

    ```bash
    cd /opt/splunk/bin
    ```

3.  **Enable Splunk boot start with systemd.**

    ```bash
    ./splunk enable boot-start -systemd-managed 1 -systemd-unit-file-name splunk
    ```

4.  **Start Splunk Enterprise and accept the license agreement.**

    ```bash
    sudo ./splunk start --accept-license
    ```

5.  **Verify Splunk status.**

    ```bash
    ./splunk status
    ```

    * You should see output indicating that Splunkd is running.

## Step 4: Access Splunk Web Interface

1.  **Open a web browser and navigate to the public IP address of your Lightsail instance on port 8000.**

    * `http://<lightsail_public_ip>:8000`

2.  **Log in with the default credentials:**

    * Username: `admin`
    * Password: `changeme` (You will be prompted to change this password immediately after logging in.)

## Security Considerations

* **Change the default admin password immediately.**
* **Configure firewall rules on your Lightsail instance to restrict access to port 8000.**
* **Consider using HTTPS for Splunk Web interface access.**
* **Regularly update Splunk Enterprise to the latest version.**
* **Implement proper access controls and authentication mechanisms within Splunk.**
* **For production environments, consider using a more robust infrastructure setup.**
* **If you are running Splunk on a public facing instance, consider using a reverse proxy with SSL certificate to secure the Splunk web interface.**

## Notes

* Replace `9.0.0-6818ac46f2ec-Linux-x86_64.tgz` with the correct Splunk Enterprise package name.
* Replace `<lightsail_public_ip>` with your actual Lightsail instance's public IP address.
* Replace `<username>` with your Linux username.
* This setup is suitable for development and testing purposes. For production deployments, consider a more robust architecture.
* Always ensure that the download link for splunk is the most up to date link from the official Splunk website.
* Always check the Splunk documentation for the most up to date system requirements.
