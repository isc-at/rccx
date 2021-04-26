### Why SSH ?
If you do not have direct access to the server that runs your IRIS Docker container   
you still may require access to the container outside "iris session" or "WebTerminal".   
With ans SSH terminal (PuTTY, KiTTY,.. ) you get access inside Docker, and then, depending    
on your needs you run "iris session iris" or display/manipulate files directly.

##### Note:
This is not meant to be the default access for the average application user  
but the emergency backdoor for System Management, Support and Development. 

This project is based on templates for InterSystems ObjectScript Github repository.  
There a few siginifcant extensions:  
- docker-compose.yaml exposes port 22 for SSH   
- Dockerfile installs SSH server and prepares Server start. You may observe    
  a significant bunch up updates as the underlying Ubuntu is not very fresh    
- to login into your container user **irisrsowner** got a password visible to you   
  that is required for login over SSH. User root is not allowed for login.   
 
The rest is pretty default for InterSystems IRIS Community Edition in a docker container.
### Prerequisites  
Make sure you have [git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git) and [Docker desktop](https://www.docker.com/products/docker-desktop) installed.
### Installation   
Clone/git pull the repo into any local directory  
```
$ git clone https://github.com/rcemper/SSH-for-IRIS-container.git   
```
Open the terminal in this directory and run:
```
$ docker-compose build
```
Run the IRIS container with
```
$ docker-compose up -d
```
### How to Test it:
If you didn't assign a fixed port to projected container port 22 you may run
```
$ docker ps
e37392a1c7c3   ssh-for-iris-container   "/bin/sh -c '/iris-m…"   2 hours ago   Up 2 hours (unhealthy)   
2188/tcp, 54773/tcp,    
0.0.0.0:41022->22/tcp, 0.0.0.0:41773->1972/tcp, 0.0.0.0:42773->52773/tcp, 0.0.0.0:49716->53773/tcp   
```
and see the assigned_port for port 22 in container (here it's 41022).  
Next, you connect with PuTTY over SSH to server:assigned_port   
Log in as **irisowner** + the PW of your choice and you are in your container.   

This is similar as with **docker-compose exec iris sh**  in a local docker instance.   

### Example:
```
login as: irisowner
irisowner@localhost's password:
Welcome to Ubuntu 18.04.4 LTS (GNU/Linux 5.4.72-microsoft-standard-WSL2 x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

This system has been minimized by removing packages and content that are
not required on a system that users do not log into.

To restore this content, you can run the 'unminimize' command.
Last login: Sat Apr 17 11:10:56 2021 from 172.18.0.1
$
$ iris view

Instance 'IRIS'   (default)
        directory:    /usr/irissys
        versionid:    2020.4.0.524.0com
        datadir:      /usr/irissys
        conf file:    iris.cpf  (SuperServer port = 1972, WebServer = 52773)
        status:       running, since Sat Apr 17 09:12:38 2021
        state:        ok
        product:      InterSystems IRIS

$ iris session iris -U "%SYS"
Node: e37392a1c7c3, Instance: IRIS
%SYS>zpm
zpm:%SYS>list
language-extender 0.0.1
webterminal 4.9.2
zpm 0.2.14
zpm:%SYS>q

%SYS>h
$
```

[Article in DC](https://community.intersystems.com/post/simplified-objectscript-source-folder-structure-package-manager)
