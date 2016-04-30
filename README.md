# AutoThreatLog
AutoThreatLog is a set of bash scripts that extract a list of IPs from a log file, check the IPs against specified blacklists, export the results to a text file, and then emails the results to specified receipients. 

## Requirements
1. A Linux environment with bash 
2. Syslog (exporting IP history to a log file)
3. Mutt (for emailing AutoThreatLog results)
4. grep
5. A file containing IP addresses to check against the blacklists

## About The Scripts - autothreatlog
The autothreatlog bash script reads the IP addresses from the log file to a text file. This text file is then checked for duplicate addresses. The resulting data in this text file is then passed to the blcheck script. After the ip data text file has been read, the autothreatlog script will check if the blcheck script created a blacklisted IP log, and then email this file to specified receipients. If the file was not created by the blcheck script, an email stating that no blacklisted IP activity detected is emailed to the speciefied receipients. 

## About The Scripts - blcheck
The blcheck bash script is a modification of a script created by J65nko on daemonforums (http://daemonforums.org/showthread.php?t=302). It also contains a modification by J.Reilink on saotn.org (https://www.saotn.org/bash-check-ip-address-blacklist-status/). 
The blcheck script receives IP addresses from the autothreatlog script, checks them against the specified blacklists, then returns the list of blacklisted IP addresses to a text file named with the current date (m-d-y_potential_threats.txt). Furthermore, if an IP is detected on a blacklist, information about the IP is passed to the aforementioned text file. This information includes the hostname, organization, country, region, city, post code, and geolocation of the IP address, if available. 

##Using The Scripts
Copy the two scritps to your /usr/bin/ folder, then run "sudo chmod +x blcheck && chmod +x autothreatlog"
Add the autothreatlog script to your cronjobs. On Ubuntu Server, this would be done by running "crontab -e" and adding the script to the users cronjob list. For more information on Cron, visit https://help.ubuntu.com/community/CronHowto
