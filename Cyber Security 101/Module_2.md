#  Linux  
https://tryhackme-images.s3.eu-west-1.amazonaws.com/room-icons/1773400244147-linuxfundamentalspart1.png  
pwd  
ls  
ls -a  
ls -la [list of all]  
find ~ -name FILE_NA*   
cat FILE_path  [get file content]  
whoami [says the user]  
uname -a [full data about user and os]  
df -h [directory data size , ...]  

# Linux Fundamentals Part 2   
touch file.txt [create file]  
mv file NEW_PATH [move file]  
su user2 [switch to user 2]  
/var/logs [directory of logs]  
/tmp [is similar to RAM]  
## File permissions
ls -lh : list of files with permssion  
permisions: read write execution (rwe)  
r=4 w=2 e=1 
3first: owner 3next:group 3last:others  
rwxr-xr-x : 755 
rw-r--r-- : 644  
rwx------ :700
chmod 750 system_overview.txt  
## Directories
/etc : store system files that are used by your operating system.  
/var :  data that is frequently accessed or written by services or applications running on the system like log files.  
/root : home directory for root user  


# Linux Fundamentals Part 3   
editors: nano / vim  or "echo >"   
scp user@ip:/server_file_PATH local_file_PATH [transfer file from server]  
ip a [get ip from inet]  
python3 -m http.server [run server on port 8000]  
ps [show running processes in a session]  
ps aux [other user session process] 
top [shows real time running process every 10 sec]  

kil 1337 [stop pid 1337]  
systemctl [stop/start/enable/disable system and service]  
systemctl [option] [service] :systemctl start apache2    
& end of process or Ctrl+z [run in background]  
fg [ bring bg process to foreground]  - we can see background process with ps last column  

cron  
crontab -e [show crons]  
example: 0 */12 * * * cp -R /home/cmnatic/Documents /var/backups/  


