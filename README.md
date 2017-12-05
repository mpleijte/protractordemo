# Steps for running protractor test in within cygwin on Windows10 on docker. 

Note: I'm using the 'winpty' command because I had difficulties getting a pseudo tty from within cygwin. 
You can install winpty from: https://github.com/rprichard/winpty



* **Step 1: Git clone this repo**<br />
```git clone https://github.com/mpleijte/protractordemo.git```

* **Step 2: Run selenium-hub**<br />
```winpty docker run -d -P --name selenium-hub selenium/hub```


* **Step 3: Run selenium-chrome and link it to selenium-hub docker**<br />
```winpty docker run -d -P --link selenium-hub:hub selenium/node-chrome-debug```


* **Step 4: Run protractor container with a volume to local repo**<br />
Open cygwin and cd into cloned protractordemo directory
<br />
```export FILES="//c/<directory-path-to-mpleijte/protractordemo>/protractor-tests"```
<br />
```winpty docker run -it --rm --net="host" -v $FILES:/src felippenardi/yo```
<br /><br />
_You should now be inside running protractor container._ 
<br />**To run the test, execute the following command:** <br />
```protractor conf.js```
<br />
<br />
* **Step 5 (Optional) view running tests with VNC viewer**
<br /> In cygwin type
<br />
````$ docker ps````
```
CONTAINER ID        IMAGE                        COMMAND                  CREATED             STATUS              PORTS                     NAMES
25cb813e65ef        selenium/node-chrome-debug   "/opt/bin/entry_po..."   36 minutes ago      Up 36 minutes       0.0.0.0:32774->5900/tcp   vibrant_shockley
0e09f866db5a        selenium/node-chrome-debug   "/opt/bin/entry_po..."   About an hour ago   Up About an hour    0.0.0.0:32773->5900/tcp   hopeful_goldberg
ec4d9e5d3430        selenium/hub                 "/opt/bin/entry_po..."   About an hour ago   Up About an hour    0.0.0.0:32772->4444/tcp   selenium-hub
```

VNC connection parameters
servername = ```127.0.0.1:32773```
password = ```secret```


