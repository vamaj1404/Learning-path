# Command Line
## Windows PowerShell
Powershell  combines a command-line interface and a scripting language built on the .NET framework.  
expanded to support macOS and linux  / object-orienterd

In programming, an object represents an item with properties (characteristics) and methods (actions). For example, a car object might have properties like Color, Model, and FuelLevel, and methods like Drive(), HonkHorn(), and Refuel().  

Remmina client : to connect to the target VM via SSH in Linux

Running powerdhell: start> powershell or cmd.exe > powershell  

powershell commands are known as cmdlets (pronounced command-lets)  
Basic Syntax: Verb-Noun > like `Set-Location`  

`Get-Command`: To list all available cmdlets, functions, aliases, and scripts that can be executed in the current PowerShell session  
`Get-Command -CommandType "Function"` : if we want to display only the available commands of type “function”  
`Get-Help` : it provides detailed information about cmdlets > `Get-Help Get-Date`  
`‍Get-Alias` lists all aliases available. For example, `dir` is an alias for `Get-ChildItem`, and `cd` is an alias for `Set-Location`.  
`Get-ChildItem` lists the files and directories in a location specified with the `-Path`  like `ls` in cmd   
`Set-Location -Path ".\Documents"`  
`New-Item -Path ".\captain-cabin\captain-wardrobe" -ItemType "Directory"` maked directory or file  
`Remove-Item -Path ".\captain-cabin\captain-wardrobe\captain-boots.txt"`  
`Remove-Item -Path ".\captain-cabin\captain-wardrobe"`  removes directory  
`Copy-Item -Path .\captain-cabin\captain-hat.txt -Destination .\captain-cabin\captain-hat2.txt`  
`Get-Content -Path ".\captain-hat.txt"` like `cat` in linux  


piping: output of one command to be used as the input for another `Get-ChildItem | Sort-Object Length`  
pipe and filter: `Get-ChildItem | Where-Object -Property "Extension" -eq ".txt" `  : `-eq` means equal  
  - `-ne`: "not equal"  
  - `-gt`: "greater than"  
  - `-ge`: "greater than or equal to"  
  - `-lt`: "less than"
  - `-le`: "less than or equal to".  
  - `-like`: `Get-ChildItem | Where-Object -Property "Name" -like "ship*"`  
`Select-Object` : refining the output to show only the details one needs. `Get-ChildItem | Select-Object Name,Length`  
example :  `Get-ChildItem | Sort-Object Length -Descending | Select-Object -First 1` : gets biggest size file  
`Select-String` : searches for text patterns within files, similar to `grep` or `findstr` in Windows : `Select-String -Path ".\captain-hat.txt" -Pattern "hat"`  


`Find-Module -Name "PowerShell*"` finds modules onlne  (NEED INTERNET)  
`Install-Module -Name "PowerShellGet"` install it (NEED INTERNET)  
### task 6 : system and networking  
`Get-ComputerInfo`  
`Get-LocalUser`  
`ipconfig` and `Get-NetIPConfiguration`  
`Get-NetIPAddress`  specific details about the IP addresses assigned to the network interfaces  

### task7 real-time analysis
`Get-Process` provides a detailed view of all currently running processes  
`Get-Service` status of services  
`Get-NetTCPConnection` displays current TCP connections.  it can uncover hidden backdoors or established connections    
`Get-FileHash` as a useful cmdlet for generating file hashes, which is particularly valuable in incident response  

### task 8
`Invoke-Command` is essential for executing commands on remote systems, making it fundamental for system administrators, security engineers and penetration testers  
`Get-Help Invoke-Command -examples`  

## Linux Shell
`echo $SHELL` To see which shell you are using,  
`cat /etc/shells` ist down the available shells   
then type the name and it will open ...   
`chsh -s /usr/bin/zsh` :  makes this shell as the default shell for your terminal.  
### Bash
default in linux  
complete command with `tab`  
can see hystory by : `history`  
#### task 4
`nano first_script.sh`  
in first line : `#!/bin/bash`  
`#!/bin/bash`  
`echo "Hey, what’s your name?"`  
`read name` > for input
`echo "Welcome, $name"`  

`chmod +x first_script.sh` > make executable  
`./` for execute : `./first_script.sh`  

Loop:
```
for i in {1..10};
do
echo $i
done
```

```
if [ "$name" = "Stewart" ]; then
        echo "Welcome Stewart! Here is the secret: THM_Script"
else
        echo "Sorry! You are not authorized to access the secret."
fi
```

comment: `#`  

locker:
```
if [ "$username" = "John" ] && [ "$companyname" = "Tryhackme" ] && [ "$pin" = "7385" ]; then
        echo "Authentication Successful. You can now access your locker, John."
else
        echo "Authentication Denied!!"
fi
```

`sudo su` become root user  



