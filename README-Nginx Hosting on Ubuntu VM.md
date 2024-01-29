# Hosting Website on Nginx Server

This README provides instructions for hosting your website on an Nginx server running on an Ubuntu virtual machine (VM). Follow these steps to deploy your website for public access.

## Prerequisites

- Ubuntu virtual machine (VM) with Nginx installed
- Website files ready for deployment

## Steps

### 1. Install Nginx

If Nginx is not already installed on your Ubuntu VM, you can install it using the following command:

```bash
sudo apt update
sudo apt install nginx
```

### 2. Transfer Website Files

Copy your website files to the appropriate directory on the Ubuntu VM. Typically, Nginx serves files from the `/var/www/html` directory. You can use the `scp` command to securely transfer files from your local machine to the VM:

```bash
scp -r /path/to/your/website user@your_server_ip:/var/www/html
```

OR if you are using Oracle VM virtualbox, use the shared files feature to copy the files from your local machine to your VM.

### 3. Configure Nginx

Edit the Nginx configuration file to server your website. You can find the default configuration file at `/etc/nginx/sites-available/default`

```bash
sudo nano /etc/nginx/sites-available/default
```
Update the 'server_name' directive to specify your server's IP address or domain name:

```bash
server {
    listen 80 default_server;
    listen [::]:80 default_server;

    root /var/www/html;
    index index.html index.htm index.nginx-debian.html;

    server_name your_server_ip;

    location / {
        try_files $uri $uri/ =404;
    }
}
```
Save the changes and exit the text editor

### 4. Restart Nginx

After making changes to the Nginx configuration, restart the Nginx service to apply the changes:
```bash
sudo systemctl restart nginx
```

### 5. Verify Deployment
Open a web browser and enter your VM's IP address (or domain name, if available) in the address bar. You should see your website displayed

### Conclusion
Congratulations! Your website is now hosted on an Nginx server and accessible to the public. If you encounter any issues, refer to the Nginx documentation or seek assistance from the community


Feel free to customize this README file with your specific details and additional information as needed
