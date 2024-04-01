# Automation
Voer deze stappen uit op iedere linux server, die als ansible managed node zal dienen.
```/bin/bash
sudo useradd ansible -G root -m
sudo mkdir -p /home/ansible/.ssh
sudo chown -R ansible /home/ansible/.ssh
sudo nano /home/ansible/.ssh/authorized_keys
```

ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQC8OW+jZvvF5+2JJTegfZZzogkmZftB9U4Ls8C61W3EBTArIElApKeiT8Jh4dLTzw7+7533YWmF+CS3j+uru8IRTAUn+kvaie5ba7vlPzVY1gzr4GZ9f+bnOLhepmzRTdcsqpooxYf1mKG1y4WWIcqPdMy0IpTxIKUuSnRxr+XBzRPDcVOMLh+rExEUVbckzAYdTViOj0s3AW2aSgcZHoOAPwm8An+m3B+x/yzC1k/l0UJXlUPmrMC+XxjactdpZKf4CYCwZ4VyggEKuy/vNJt/9TCzWUKBgbxPCa9Z2fO0V/Iyd0bktRSXPFv95Z+DeQLSDxQ+RE/030WYuYyTBZtsEJqS2qMHPFokW5AmyM0Hrk+HWntn7+T0PlN5aLcN6ld60lG10I9P9qHRqVAC9Nkw2H4zsfibibgHUJnXYhW/9IA5XPeikiTgw746/xiNFbmPOJWpH+QUOq+ierAo9mANjlBKtpuGnQB+uq20CjeNkgKyrLX8Nfo8p9AIKfMJM2c= ansible@truman

```.ssh/config
Host aed
  Hostname aed.ad.eendjesshop.be
  PreferredAuthentications publickey
  User ansible
  IdentityFile ~/.ssh/automation_key

```


https://docs.ansible.com/ansible/latest/os_guide/windows_setup.html

https://www.google.com/search?channel=fs&client=ubuntu-sn&q=managing+windows+hosts+with+ansible#fpstate=ive&vld=cid:13aa7fd0,vid:-vPXS8UuJoI,st:0

Upgrade Powershell & .Net
```powershell
[Net.ServicePointManager]::SecurityProtocol = [Net.SecurityProtocolType]::Tls12
$url = "https://raw.githubusercontent.com/jborean93/ansible-windows/master/scripts/Upgrade-PowerShell.ps1"
$file = "$env:temp\Upgrade-PowerShell.ps1"
$username = "Administrator"
$password = "Password"

(New-Object -TypeName System.Net.WebClient).DownloadFile($url, $file)
Set-ExecutionPolicy -ExecutionPolicy Unrestricted -Force

&$file -Version 5.1 -Username $username -Password $password -Verbose
```

Setup Winrm listeners

```powershell
[Net.ServicePointManager]::SecurityProtocol = [Net.SecurityProtocolType]::Tls12
$url = "https://raw.githubusercontent.com/ansible/ansible-documentation/ae8772176a5c645655c91328e93196bcf741732d/examples/scripts/ConfigureRemotingForAnsible.ps1"
$file = "$env:temp\ConfigureRemotingForAnsible.ps1"
(New-Object -TypeName System.Net.WebClient).DownloadFile($url, $file)
powershell.exe -ExecutionPolicy ByPass -File $file
```