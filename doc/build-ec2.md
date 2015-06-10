# Instructions for building on an Amazon AWS EC2 server

1. Setup an Amazon AWS account  https://aws.amazon.com

2. Provision an EC2 server (recommend t1.micro Spot Request for cheapest cost
   a. ssh -i nameOfThePEMfile.pem ubuntu@ipaddress

3. Install Apache2 Web Server and git
   a. sudo apt-get update
   b. sudo apt-get install apache2 git

4. Make a working directory for git and clone the simplepage.rwrt repo
   a. cd ~ && mkdir git && cd ~/git
   b. git clone https://github.com/archLinuxUser/simplepage.rwrt.git

5. Go to the apache web server root directory
   a. cd /var/www/html
   b. sudo mv -i index.html ~/git/original-index.html
   c. sudo cp -vr ~/git/simplepage.rwrt/. ./

5. Test the website by visiting http://ip.publicaddress.from.aws-dashboard

6. Create a swap file as this is a limited-memory t1.micro instance
   a. sudo su
   b. fallocate -l 1024M /swapfile
   c. chmod 600 /swapfile
   d. mkswap /swapfile
   e. swapon /swapfile
   f. nano /etc/fstab
   g. - add the line below to /etc/fstab
/swapfile       none    swap    defaults        0 0

7. reboot and check webserver (simplepage webpage) and the swap memory (cli)
   a. access http://ip.publicaddress.from.aws-dashboard via web browser
   b. free -mt

8. If everything there, then start to clean-up the simplepage (your webpage/website)
   a. cd /var/www/html && sudo nano index.html   # for modifying the links/personal link
   b. sudo nano style/script.css
	background-image			# background picture - remove or change
	html codes for font colors and font sizes, and background color
   c. sudo nano js/script.js

9. Save a backup of the AWS EC2 instance
