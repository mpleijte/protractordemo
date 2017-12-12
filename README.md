# Steps for running protractor test in within git bash on Windows10 on docker. 

Note 1: I'm using the 'winpty' as prefix for all docker run commands because I had difficulties getting a pseudo tty from git bash or cygwin. You can install winpty from: https://github.com/rprichard/winpty

* **Step 1: Git clone this repo**<br />
```git clone https://github.com/mpleijte/protractordemo.git```

* **Step 2: Run selenium and chrome containers**<br />
```docker-compose up```

* **Step 3: Run protractor container with a volume to your local repo**<br />
Open git bash and cd into cloned protractordemo directory<br />
```
docker run -it --rm --net="host" -v /`realpath .`:/src felippenardi/yo
```
<br /><br />
_You should now be inside running protractor container._ 
<br />**To run the test, execute the following command:** <br />
```protractor conf.js```
<br />
<br />
* **Step 4 (Optional) view running tests with VNC viewer**
<br /> In git bash type<br />
```$ docker ps```
````
CONTAINER ID        IMAGE                        COMMAND                  CREATED             STATUS              PORTS                     NAMES
25cb813e65ef        selenium/node-chrome-debug   "/opt/bin/entry_po..."   36 minutes ago      Up 36 minutes       0.0.0.0:32774->5900/tcp   vibrant_shockley
0e09f866db5a        selenium/node-chrome-debug   "/opt/bin/entry_po..."   About an hour ago   Up About an hour    0.0.0.0:32773->5900/tcp   hopeful_goldberg
ec4d9e5d3430        selenium/hub                 "/opt/bin/entry_po..."   About an hour ago   Up About an hour    0.0.0.0:32772->4444/tcp   selenium-hub
````
VNC connection parameters
servername = ```127.0.0.1:33378```
password = ```secret```


