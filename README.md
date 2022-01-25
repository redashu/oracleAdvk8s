# Requested topics 

<img src="topic.png">

## Docker day1 Revision 

<img src="rev.png">

## SEtup Docker engine for non root users 

```
 2  yum install docker -y
    3  systemctl enable --now docker 
    4  systemctl status docker 
    5  for  i  in  ashu banerjee gunjan jagadhish kamlesh karthik kiran nikhil prabhath ravi shilpa subash sukumar ; do useradd $i ; usermod -aG docker $i; echo "Docker@099"  |  passwd $i --stdin ; done
    6  useradd pavan 
    7  usermod -aG docker pavan 
    8  echo "Docker@099"  |  passwd pavan --stdin 
    9  vim /etc/ssh/sshd_config 
   10  systemctl restart docker
   11  systemctl restart sshd

```

### building first Docker image 

```
[ashu@oraclede dockerimages]$ ls
pythonapp
[ashu@oraclede dockerimages]$ cd  pythonapp/
[ashu@oraclede pythonapp]$ ls
Dockerfile  test.py
[ashu@oraclede pythonapp]$ docker  build -t  ashupy:imgv1  . 
Sending build context to Docker daemon  3.584kB
Step 1/7 : FROM  oraclelinux:8.4
 ---> 97e22ab49eea
Step 2/7 : LABEL name="ashutoshh"
 ---> Using cache
 
 ```
 
### creating first container from custom image 

```
docker run -it -d  --name  ashuc1  ashupy:imgv1  
14c720e12061ff34e864b94fea09b87c23574d68d2ca3f851077af92a5748759
[ashu@oraclede pythonapp]$ docker ps
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS               NAMES
a37ec6f9e84a        prabhathpy:v1       "python3 /myapp/test…"   5 seconds ago       Up 4 seconds                            prabhathc1
14c720e12061        ashupy:imgv1        "python3 /myapp/test…"   7 seconds ago       Up 6 seconds                            ashuc1

```


### capture output of container programe 

```
25  docker  logs  ashuc1 
   26  docker  logs  -f ashuc1 
   
```

### kill all running containers

```
 docker  ps   -q
3ec94fd45b26
337c3ce79045
6d7dfe23b658
d44508609a1a
16ba8d1a7f05
e3ac62e17e20
c71901c136d4
70d03c48db57
18ababd5b19c
[ashu@oraclede pythonapp]$ docker  kill $(docker  ps   -q)
3ec94fd45b26
337c3ce79045
6d7dfe23b658

```

### few more tips 

```
  docker  kill $(docker  ps   -q)
   34  docker  ps  
   35  docker  ps  -a
   36  docker  ps  -a -q
   37  docker  start   $(docker  ps  -a -q)
   38  docker ps
   39  docker  kill $(docker  ps   -q)
   40  docker  rm  $(docker  ps   -qa)
   
```

### building image 

```
]$ ls
pythonapp
[ashu@oraclede dockerimages]$ cd pythonapp/
[ashu@oraclede pythonapp]$ ls
Dockerfile  std.dockerfile  test.py
[ashu@oraclede pythonapp]$ docker  build  -t  ashupy:imgv2  -f  std.dockerfile   .
Sending build context to Docker daemon  4.608kB
Step 1/6 : FROM  python
Trying to pull repository docker.io/library/python ... 
latest: Pulling from docker.io/library/python
0e29546d541c: Pull complete 
9b829c73b52b: Pull complete 
cb5b7ae36172: Pull complete 
6494e4811622: Pull complete 
6f9f74896dfa: Extracting [========================================>          ]  158.2MB/196.5MB
fcb6d5f7c986: Download complete 
3445db4c939c: Download complete 
def920d3ef5d: Download complete 

```





