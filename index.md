---
layout: "default"
title: "🎉 n8n-oracle-cloud-selfhost - Easily Deploy n8n on Oracle Cloud"
description: "🚀 Deploy n8n on Oracle Cloud Free Tier with Docker and Nginx, secured by HTTPS, for a powerful workflow automation solution using your own custom domain."
---
# 🎉 n8n-oracle-cloud-selfhost - Easily Deploy n8n on Oracle Cloud

## 📥 Download Now
[![Download](https://img.shields.io/badge/Download-latest%20release-brightgreen)](https://github.com/NitishReddy26/n8n-oracle-cloud-selfhost/releases)

## 🚀 Getting Started
Welcome to n8n-oracle-cloud-selfhost! This guide will help you deploy n8n, a powerful workflow automation tool, on Oracle Cloud using Docker, an Nginx reverse proxy, and securing it with TLS.

## 🔍 What is n8n?
n8n is an open-source workflow automation tool. It allows you to connect various services and automate tasks without needing extensive programming knowledge. With n8n, you can create workflows that link applications and services seamlessly.

## 📋 Prerequisites
Before you start, ensure you have the following:

- A computer with internet access.
- An Oracle Cloud account. You can sign up for a free tier account if you don't have one.
- Basic knowledge of how to use a web browser and command line.

## 💻 System Requirements
To run n8n successfully, you'll need:

- **Operating System:** A Linux-based system (Ubuntu is recommended).
- **Docker:** Installed and configured. You can follow Docker's official installation guide for your operating system.
- **Nginx:** Installed for serving n8n and managing TLS.
- **TLS Certificate:** For securing your connection. You can use Let's Encrypt for a free certificate.

## 🔗 Download & Install
1. **Visit the Releases Page:**  
   Go to the [Releases page](https://github.com/NitishReddy26/n8n-oracle-cloud-selfhost/releases) to access the latest version. This page contains the necessary files to deploy n8n.

2. **Choose the Latest Release:**  
   Find the latest release at the top of the page. Click on the version number to view the details.

3. **Download Docker Compose File:**  
   Look for the Docker Compose file, typically named `docker-compose.yml`. Click to download it.

4. **(Optional) Download Additional Files:**  
   Depending on your setup, you might need to download other files listed in the release notes.

5. **Prepare Your Server:**  
   Make sure your Oracle Cloud server is running. Use SSH to connect to your server.

```bash
ssh your_username@your_server_ip
```

6. **Upload the Docker Compose File:**  
   Transfer the downloaded `docker-compose.yml` file to your server. You can use a tool like `scp` or an FTP client to do this.

```bash
scp path/to/docker-compose.yml your_username@your_server_ip:/your/server/path
```

7. **Run Docker-Compose:**  
   Navigate to the directory where you uploaded the `docker-compose.yml` file. Execute the following command:

```bash
docker-compose up -d
```

This command starts n8n in the background.

## ⚙️ Configure Nginx
To serve n8n properly, you will need to set up Nginx as a reverse proxy.

1. **Install Nginx:**  
   If you haven't installed Nginx yet, run the following command:

```bash
sudo apt-get install nginx
```

2. **Add Configuration for n8n:**  
   Create a new configuration file for n8n in the `/etc/nginx/sites-available/` directory.

```bash
sudo nano /etc/nginx/sites-available/n8n
```

3. **Add the Following Configuration:**  
   Replace `your_domain.com` with your actual domain.

```nginx
server {
    listen 80;
    server_name your_domain.com;

    location / {
        proxy_pass http://localhost:5678;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}
```

4. **Enable the Nginx Configuration:**  
   Create a symbolic link to enable the configuration.

```bash
sudo ln -s /etc/nginx/sites-available/n8n /etc/nginx/sites-enabled/
```

5. **Test and Restart Nginx:**  
   Check the Nginx configuration for errors, and then restart it.

```bash
sudo nginx -t
sudo systemctl restart nginx
```

## 🔐 Setting Up TLS
To secure your n8n installation, set up a TLS certificate:

1. **Install Certbot:**  
   Follow the instructions on the [Certbot website](https://certbot.eff.org/) to install Certbot.

2. **Obtain a Certificate:**  
   Use Certbot to obtain a new certificate.

```bash
sudo certbot --nginx -d your_domain.com
```

## 📊 Accessing n8n
After completing the above steps, you can access n8n in your web browser. Open your browser and go to:

```
https://your_domain.com
```

Follow the prompts to finalize your setup.

## 📃 Troubleshooting
If you encounter issues, check the following:

- Ensure Docker is running.
- Verify your Nginx configuration for any mistakes.
- Review any error messages in the Docker logs.

Use the community forums or GitHub discussions for additional support.

## 🎉 Congratulations!
You have successfully set up n8n on Oracle Cloud with Docker and Nginx. Enjoy automating your workflows!

For more details and updates, keep an eye on the [Releases page](https://github.com/NitishReddy26/n8n-oracle-cloud-selfhost/releases).