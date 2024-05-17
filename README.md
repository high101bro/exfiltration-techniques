# exfiltration-techniques

Did you know you can append early any text to the end of nearly any file in Linux, and the modified file will still work? You don't have to base64 encode the data like I have before, but I'm include as POC to obfuscate the contents. You could use encryption instead of encoding to further hide it. 

```
# Copying /bin/ls to my local directory
┌──(kali㉿ZenBook)-[~]
└─$ cp /bin/ls .

# Testing that ./ls works locally
┌──(kali㉿ZenBook)-[~]
└─$ ./ls
Android  Desktop  docker-commands.txt  Documents  Downloads  kali  ls  Music  Pictures  Public  Templates  test  thinclient_drives  update-kali.sh  Videos

# Viewing what the last 250 characters ./ls 
┌──(kali㉿ZenBook)-[~]
└─$ tail -c 250 ./ls
�U�E� �EI ,F4`F/

# Appending a newline so the data to exfiltrate is on the last line
┌──(kali㉿ZenBook)-[~]
└─$ echo -e "\n" >> ./ls

# Appending the contents of /bin/echo as base64 into ./ls
┌──(kali㉿ZenBook)-[~]
└─$ cat /bin/echo | base64 -w 0 >> ./ls

# Testing that ./ls is still functional locally
┌──(kali㉿ZenBook)-[~]
└─$ ./ls
Android  Desktop  docker-commands.txt  Documents  Downloads  kali  ls  Music  Pictures  Public  Templates  test  thinclient_drives  update-kali.sh  Videos

# Viewing that the last 250 characters ./ls include the base64 encoded data to exfiltrate 
┌──(kali㉿ZenBook)-[~]
└─$ tail -c 250 ./ls
AAAAAAAAAAAAAAAAAAAAAAAADgoQAAAAAAAEkAAAAAAAAAAAAAAAAAAAABAAAAAAAAAAAAAAAAAAAAIAEAAAEAAAAAAAAAAAAAAAAAAAAAAAAALKIAAAAAAAA0AAAAAAAAAAAAAAAAAAAABAAAAAAAAAAAAAAAAAAAAAEAAAADAAAAAAAAAAAAAAAAAAAAAAAAAGCiAAAAAAAALwEAAAAAAAAAAAAAAAAAAAEAAAAAAAAAAAAAAAAAAAA=

# Extracting and decoding the base64 code within ./ls to a local ./echo
┌──(kali㉿ZenBook)-[~]
└─$ tail -n 1 ./ls | base64 -d > ./echo

# Setting the execute bin so that he ./echo command will function
┌──(kali㉿ZenBook)-[~]
└─$ sudo chmod +x ./echo
[sudo] password for kali: 

# Testing that the local ./echo is fully funcational after being encoded and decoded/extracted
┌──(kali㉿ZenBook)-[~]
└─$ ./echo "Bazinga! Both ./ls and ./echo function flawlessly! ./ls with the appended base64, and ./echo after being encoded and decoded/extracted!"
Bazinga! Both ./ls and ./echo function flawlessly! ./ls with the appended base64, and ./echo after being encoded and decoded/extracted!
```

Screenshot Proof of Concept

![image](https://github.com/high101bro/exfiltration-techniques/assets/13679268/ef832d08-6a76-48d1-b695-23f8eb246279)

