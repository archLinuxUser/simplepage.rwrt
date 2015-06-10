
1. Setup an Amazon AWS account  https://aws.amazon.com

2. Provision an EC2 server (recommend t1.micro Spot Request for cheapest cost)
[code]
ssh -i nameOfThePEMfile.pem ubuntu@ipaddress
[/code]

3. Install Apache2 Web Server and git
[code]
sudo apt-get update
sudo apt-get install apache2 git
[/code]

4. Make a working directory for git and clone the simplepage.rwrt repo
[code]
cd ~ && mkdir git && cd ~/git
git clone https://github.com/archLinuxUser/simplepage.rwrt.git
[/code]

5. Go to the apache web server root directory
[code]
cd /var/www/html
sudo mv -i index.html ~/git/original-index.html
sudo cp -vr ~/git/simplepage.rwrt/. ./
[/code]

5. Test the website by visiting http://ip.publicaddress.from.aws-dashboard

6. Create a swap file as this is a limited-memory t1.micro instance
[code]
sudo su
fallocate -l 1024M /swapfile
chmod 600 /swapfile
mkswap /swapfile
swapon /swapfile

nano /etc/fstab

# modify /etc/fstab and add the line below
/swapfile       none    swap    defaults        0 0
[/code]

7. reboot and check webserver (simplepage webpage) and the swap memory (cli)
[code]
access http://ip.publicaddress.from.aws-dashboard via web browser
free -mt
[/code]

8. If everything there, then start to clean-up the simplepage (your webpage/website)
   a. cd /var/www/html && sudo nano index.html   # for modifying the links/personal link
   b. sudo nano style/script.css
	background-image			# background picture - remove or change
	html codes for font colors and font sizes, and background color
   c. sudo nano js/script.js

9. Save a backup of the AWS EC2 instance
