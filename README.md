# exfiltration-techniques

Did you know you can append early any text to the end of nearly any file in Linux, and the modified file will still work? You don't have to base64 encode the data like I have before, but I'm include as POC to obfuscate the contents. You could use encryption instead of encoding to further hide it. 

```bash
┌──(kali㉿ZenBook)-[~]
└─$ cp /bin/ls .

┌──(kali㉿ZenBook)-[~]
└─$ echo "\n" >> ./ls

┌──(kali㉿ZenBook)-[~]
└─$ tail -n 1 ./ls
 ��M�=��O���O�`S`C�    �U�E� �EI ,F4`F/\n

┌──(kali㉿ZenBook)-[~]
└─$ echo -e "\n" >> ./ls                                                                                                                                                                                                                                                                                                                                                                                                          

┌──(kali㉿ZenBook)-[~]
└─$ tail -n 1 ./ls                                                                                                                                                                                                                                                                                                                                                                                                                 


┌──(kali㉿ZenBook)-[~]
└─$ cp /bin/ls .

┌──(kali㉿ZenBook)-[~]
└─$ echo -e "\n" >> ./ls                                                                                                                                                                                                                                                                                                                                                                                                                 

┌──(kali㉿ZenBook)-[~]
└─$ cat /bin/echo | base64 -w 0 >> ./ls

┌──(kali㉿ZenBook)-[~]
└─$ tail -c 25 ./ls
AAAEAAAAAAAAAAAAAAAAAAAA=
┌──(kali㉿ZenBook)-[~]
└─$ ./ls                                                                                                                                                                                                                                                                                                                                                                                                                                 
Android  Desktop  docker-commands.txt  Documents  Downloads  echo  kali  ls  Music  Pictures  Public  Templates  test  thinclient_drives  update-kali.sh  Videos

┌──(kali㉿ZenBook)-[~]
└─$ tail -n 1 ./ls | base64 -d >> ./echo                                                                                                                                                                                                                                                                                                                                                                          

┌──(kali㉿ZenBook)-[~]
└─$ ./echo "This works flawlessly!"
bash: ./echo: Permission denied

┌──(kali㉿ZenBook)-[~]
└─$ chmod +x ./echo                                                                                                                                                                                                                                                                                                                                                                                                                      

┌──(kali㉿ZenBook)-[~]
└─$ ./echo "Okay... this works flawlessly!"                                                                                                                                                                                                                                                                                                                                                                                            
Okay... this works flawlessly!
```

![image](https://github.com/high101bro/exfiltration-techniques/assets/13679268/c99b10f5-468a-41c6-bb9d-0c9dc2c902e0)
