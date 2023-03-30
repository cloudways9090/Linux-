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

  
  TroubleShoot High CPU Usage Commend 
  
  1) sudo apm 
  2) sudo apm php -s dbname <inside application >
  3) sudo apm mysql -s dbname 
  4) sudo apm -s dbname traffic -l24h 
  
  Run commend insdie application )
  
  for A in $(ls -la | awk '{print $NF}'); do echo $A && awk '{print$1,$7}' $A/logs/apache_*.access.log | cut -d? -f1 | sort | uniq -c | sort -nr | head -n 5 | awk -F";" '{print $1}' ; done
  
1)  for A in $(ls | awk '{print $NF}'); do echo $A && /usr/local/sbin/apm traffic -s $A -l 1h; done
  
2) for A in $(ls | awk '{print $NF}'); do echo $A && sudo /usr/local/sbin/apm mysql -s $A -l 1h; done
  
3) for A in $(ls | awk '{print $NF}'); do echo $A &&  /usr/local/sbin/apm php -s $A -l 1h; done

                                               High CPU Case Issue 
                                               
1- Check graphs and HTOP to know whether CPU is still high or went high in past.

2- Check Varnish, if it's working or not.

3- Track traffic via APM or by running curl https://raw.githubusercontent.com/ahmedeasypeasy/New-Cpu/main/Cpu.sh | bash  in /home/master

4- If you find higher rate Google bot crawling, tell the customer to add crawl delay via robots.txt max of 2secs

5- If wp-cron is being called in huge number, disable it via WordPress config and enable it via server using wp cli approach.

6- if there are IPs accessing application mostly, so check first if it's server ip or not. If not then use abuseipdb.com to verify if it's attackers IP or not.

7- If MySQL is consuming high CPU, so check the query.
8- If nothing is appearing, check TTFB of server by creating phpinfo in any of application and check firstbyte against it. It shouldn't be more than 300ms.

9- Also check if there is any slow plugin other than elementor|wocommerce.

Mostly plugins consume high CPU where they call external URL, function would be LIKE wp_remote_get().
Follow above approach in every high CPU usage case and let me know if you find anything different than above
  
  
  Default index.php files 
  
  <?php
/**
 * Front to the WordPress application. This file doesn't do anything, but loads
 * wp-blog-header.php which does and tells WordPress to load the theme.
 *
 * @package WordPress
 */
/**
 * Tells WordPress to load the WordPress theme and output it.
 *
 * @var bool
 */
define( 'WP_USE_THEMES', true );
/** Loads the WordPress Environment and Template */
require __DIR__ . '/wp-blog-header.php';


2) Then use root-user to update the plugin:
wp plugin update elementor-pro --allow-root
(make sure to reset the permissions as per the permissions set on other files in that directory)

3) If site is still redirecting, then check site URL and home URL
wp option get siteurl
wp option get home

(Only update the one that is not correct)
wp option update siteurl 'http://example.com'
wp option update home 'http://example.com'


