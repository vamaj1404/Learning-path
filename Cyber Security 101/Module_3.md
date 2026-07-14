# Windows and AD Fundamentals
## Basic requirements :
msconfig  
taskmgr  
### In Windows server :
win +r / shell:startup  
for more settings: serach : View advanced system settings  
  Advanced > prformance > settings > virtual RAM  
  Advanced > startup and recovery  > settings > info about Blue Screen of Death ,....   

System Configuration : Has a lot of system tools such as
  - computer management >
    -  Task Scheduler
    -  event viewer
    -  shared folders
  - CMD:  
    - hostname  
    - whoami  
    - ipconfig  
    - for help in commands : "/?"  > ipconfig /?  
    - cls : clear command prompt  
    - netstat  
    - net  


### ssh in linux to windows server :  
[for exaple ls not work when target is windows , we should use dir]
  - set  
  - ver  
  - systeminfo
  - tracert example.com
  - nslookup example.com [return host ip]
  - nslookup example.com 1.1.1.1 [to use specific dns]
  - netstat -abon
  - dir /a [show all]
  - dir /s [all and subdirectories]
  - tree [show directory in tree view]
  - mkdir [make dir]
  - rmdir [remove dir]
  - type [like cat in linux] - use more for long files
  - copy file1 file2
  - move file1 .. [moves to upper dir]
  - del / erase
  - copy *.md C:\Markdown
  - tasklist
  - tasklist /?  [show available filters]
  - chkdsk: checks the file system and disk volumes for errors and bad sectors.
  - driverquery: displays a list of installed device drivers.
  - sfc /scannow: scans system files for corruption and repairs them if possible.
  - some_command | more [pipe command]

## Windows fundamentals 3  
task2: windows update > view update history > 5/3/2021  
task3: settings > windows security > virus & threat protection  
task4: real-time protection is off   
task5: firewall protect what can pass through ports . public network  
task6: app&browser controll in windows security   
task7: device security : core isolation / memory integrity /   
		security processor / trusted platform module : phisical security processor for more protection and encryption    
task8: Bitlocker : encryption to protect data on computer  / answer: USB startup key  
task9: shadow copy / snapshot .. my pc > r-click on partition > config shadow copies > good but vulnarable in malwares .  
better way: offline copy  
answer: volume shadow copy service  

## Active directory
search : 	
acrive direcory	... : make Organizational Unit for server / workstaions etc	 
group policy management	: to link policies to Organizational Units  
to change policy: r-click > edit > ... for exaple: Computer Configurations -> Policies -> Windows Setting -> Security Settings -> Account Policies -> Password Policy for minimum pass lenghth  
GPOs are distributed to the network via a network share called ‍‍‍‍‍‍`SYSVOL`  
task6:  
The SYSVOL share points by default to the `C:\Windows\SYSVOL\sysvol\`  
change has been made to any GPOs, it might take up to 2 hours for computers to catch up. to firce : `PS C:\> gpupdate /force`  
to apply polycies:  
- first find and enable policy e.g.  
  <img width="919" height="565" alt="image" src="https://github.com/user-attachments/assets/d5af591f-757a-41e8-94a7-6e9684da9cf1" />
- then link to users:
  <img width="923" height="619" alt="image" src="https://github.com/user-attachments/assets/40e5d534-4411-4da9-a9f8-c4ccd43a1276" />
`gpupdate /force` to force GPOs to be updated  
task7:







		


    


  
