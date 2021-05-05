#### first we login into IRIS and do ^zrxxx   
~~~
C:\GitHub\zrccx>docker-compose exec iris iris session iris -U "%SYS"  
Node: 32842aedd3c5, Instance: IRIS   
%SYS>   
%SYS>do ^zrccx   
start Run Container Command eXecution   
server = localhost,  port = 6666  
Enter bash command [.=exit, *** = stop executor & exit]   
??> :   
~~~
#### next we run some listing   
~~~
??> :    
??> :ls -la /   
~~~ 
```
  total 1572
  drwxr-xr-x   5 irisowner irisowner    4096 Oct 22  2020 LIC
  drwxr-xr-x   1 root      root         4096 Feb  3  2020 bin
  drwxr-xr-x   2 root      root         4096 Apr 24  2018 boot
  drwxr-xr-x   5 root      root          340 May  5 15:36 dev
  drwxr-xr-x   1 root      root         4096 May  5 15:36 etc
  drwxr-xr-x   1 root      root         4096 Feb  3  2020 home
  -rwxr-xr-x   1 root      root      1491216 Oct 22  2020 iris-main
  -rwxr-xr-x   1 root      root          382 Oct 22  2020 irisHealth.sh
  drwxr-xr-x   3 root      root         4096 May  5 15:36 irisrun
  drwxr-xr-x   1 root      root         4096 May 23  2017 lib
  - - - - - - - 
  -rwxr-xr-x   1 root      root           41 Apr 26 10:11 rccx.sh

>>drwx------   1 root      root         4096 Oct 22  2020 root <<

  drwxr-xr-x   1 root      root         4096 Jan 16  2020 run
  drwxr-xr-x   1 root      root         4096 Feb  3  2020 sbin
  drwxr-xr-x   2 root      root         4096 Jan 12  2020 srv
  dr-xr-xr-x  11 root      root            0 May  5 15:36 sys
  drwxrwxrwt   1 root      root         4096 May  5 15:35 tmp
  drwxr-xr-x   1 root      root         4096 Oct 22  2020 usr
  drwxr-xr-x   1 root      root         4096 Jan 12  2020 var
```
#### what is there in a rootless container?
~~~
??> :
??> :ls -la /root ; whoami
~~~
```
  ls: cannot open directory '/root': Permission denied
  irisowner
```
#### $ in postion 1 changes the view
~~~
??> :
??> :$ls -la /root ; whoami
~~~   
``` 
  total 24
  drwx------ 1 root root 4096 Oct 22  2020 .
  drwxr-xr-x 1 root root 4096 May  5 15:36 ..
  -rw-r--r-- 1 root root 3106 Apr  9  2018 .bashrc
  -rw-r--r-- 1 root root  148 Aug 17  2015 .profile
  -rw-r--r-- 1 root root  176 Feb  3  2020 .wget-hsts
  -rw-r--r-- 1 root root  199 Oct 22  2020 waitISC.log
  root
```
Q.A.D.
