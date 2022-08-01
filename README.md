# Linux-
Linux Usefull Commend /

---------- EXTRACTING BACKUP FILE ----------
tar -xzvf backup.tgz

---------- LIST ALL WP ADMINS ----------
wp user list --role=administrator

---------- CHANGE WP ADMIN PASSWORD ----------
wp user update user_email --user_pass="PASSWORD"

---------- FILE TRANSFER USING RSYNC ----------
rsync /home/simple.txt root@x.x.x.x:/home

---------- DB BACKUP USING MYSQLDUMP ----------
mysqldump -u <dbname> -p <dbname> > dump.sql
  
  ---------- RESTORE DB USING MYSQL ----------
mysql -p -u username database_name < file.sql

                                             
     ---------- TO CHECK ANY PHP PKG ----------
php -m | grep <pkg-name>
  
---------- CRON DAEMON RUNNING? ----------
systemctl status cron
  
---------- SEARCH & REPLACE ----------
wp search-replace "wordpress url" "custom url" --all-tables --dry-run
grep -lr <old-url>
  
--------- DOWNGRADE TO BREEZE PREVIOUS VERSION ----------
wp plugin update breeze --version=1.1.11
  
---------- CHECK REDIS IS WORKING OR NOT ---------
Run in the public_html:
redis-cli PING
  
  
---------- CLEAR REDIS CACHE ----------
redis-cli FLUSHALL
  
---------- For checking complete sorted out apache logs of single application in Cloudways (Need to be run in log folder of application) ----------
for A in $(ls | awk '{print $NF}'); do echo $A && cat $A/logs/apache_*.access.log | cut -f 1 -d ' '|sort|uniq -c|sort -nr| head -n 15 | awk -F";" '{print $1}' ; done

  
  ---------- Search particular process ----------
ps -ax  | grep -i <process_name>
  
 ---------- Forcefully deactivate plugin ----------
wp --skip-plugins --skip-themes plugin deactivate <plugin>
  
 
---------- Block bad BOTS ----------
RewriteEngine On
RewriteCond %{HTTP_USER_AGENT} ^.*(AhrefsBot|BLEXBOT|yacybot|petalbot|LinkpadBot|Wotbox|woobot|linkdexbot|Baiduspider|semrush|Exabot|MJ12bot|msnbot|HaosouSpider).*$ [NC]
RewriteRule .* - [F,L]
  
  
---------- Check WP version ----------
wp core version --allow-root
  
Number of hits app-wise:
cd applications
for A in $(ls | awk '{print $NF}'); do echo $A && cat $A/logs/apache_*.access.log | cut -f 1 -d ' '|sort|uniq -c|sort -nr| head -n 15 | awk -F";" '{print $1}' ; done
  
  
 App-wise file requests from IPs:
for A in $(ls -l /home/master/applications/| grep "^d" | awk '{print $NF}'); do echo $A && awk '{print $1,$7}' /home/master/applications/$A/logs/apache_*.access.log | cut -d? -f1 | sort | uniq -c |sort -nr | head -n 5 | awk -F";" '{print $1}' ; done
  
  
 FOR CHECKING HITS BY BOTS IN ACCESS LOG:
cat logs/apache_*.access.log | awk -F\" '{print $6}' | sort | uniq -c | sort -nr | head -20
  
  
  
 Solved WordPress Error – Download failed destination directory for streaming does not exist or is not writable
 
 define('WP_TEMP_DIR', ABSPATH . '/../temp/');

  3.1. Enabling Automatic Updates Manually

  define ('WP_AUTO_UPDATE_CORE', true);

  Set the value to “false” to disable automatic updates.


  To enable automatic updates for minor WordPress versions, add the following code to the wp-config.php file:
  
  define ('WP_AUTO_UPDATE_CORE', minor);

  This function helps disable automatic updates for any major WordPress version.

To enable automatic updates for your WordPress plugin or theme versions, add the following code to the auto_update_$type filter in the wp-admin folder of your WordPress installation:
  
  For plugins:

add_filter('auto_update_plugin', '__return_true');

  For themes:

add_filter('auto_update_theme', '__return_true');

  
  

