
Step 1: Install Apache

sudo apt update
sudo apt install apache2 -y
Step 2: Move the Game Files
sudo mv ColorGame /var/www/html/color-game
Step 3: Restart Apache
sudo systemctl restart apache2
Step 4: Access the Game
Open your browser and visit:

http://your-server-ip/color-game

=======================
IF ANY ISSUES
=======================

🔹 Step 1: Check the Apache Root Directory
The default Apache root directory in Ubuntu is:

/var/www/html
Your Color Game files should be inside this directory.

Move the Game Files to Apache Root
If your game files are in /var/www/html/color-game, you can move them to the root:

sudo mv /var/www/html/color-game/* /var/www/html/

Then, remove the empty folder:

sudo rm -r /var/www/html/color-game
🔹 Step 2: Remove the Default Apache Index Page
Apache’s default page is served by /var/www/html/index.html. To replace it with your game’s page, remove the default one:

sudo rm /var/www/html/index.html
🔹 Step 3: Restart Apache
After moving the files, restart Apache to apply changes:

sudo systemctl restart apache2
🔹 Step 4: Check Permissions
Ensure Apache has the right permissions to serve your files:

sudo chmod -R 755 /var/www/html
sudo chown -R www-data:www-data /var/www/html
🔹 Step 5: Access the Game in Browser
Now, go to your browser and visit:

http://your-server-ip
Your Color Game should now be visible!

=========================================
IF AGAIN ANY ISSUES
========================================

Step 1: Check if index.html Exists
Run the following command:

ls -l /var/www/html/
If index.html is missing, move it to the directory:


sudo mv /home/username/ColorGame/index.html /var/www/html/
🔹 Step 2: Disable Directory Listing
Apache is listing the directory because no default file (index.html) is found. To disable directory listing:

Open the Apache config file:


sudo nano /etc/apache2/apache2.conf
Scroll down and look for this section:
apache
<Directory /var/www/>
    Options Indexes FollowSymLinks
    AllowOverride None
    Require all granted
</Directory>
Change:
apache
Options Indexes FollowSymLinks
to:

apache
Options -Indexes +FollowSymLinks
Save the file (CTRL + X, then Y, then Enter).
🔹 Step 3: Restart Apache
Apply the changes by restarting Apache:

sudo systemctl restart apache2
🔹 Step 4: Test the Website
Now, open your browser and visit:

http://your-server-ip
Your Color Game should load properly.
