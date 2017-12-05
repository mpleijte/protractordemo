# Four steps for running protractor test in within cygwin on Windows10 on docker. 

Instructions below include the 'winpty' command because I had dicciculties getting a pseude tty from within cygwin. 
You can install Winpty seperately from: https://github.com/rprichard/winpty



### Step 1: Git clone this repo

### Step 2: Run selenium-hub
````winpty docker run -d -P --name selenium-hub selenium/hub````


### Step 3: Run selenium-chrome and link it to selenium-hub docker
````winpty docker run -d -P --link selenium-hub:hub selenium/node-chrome-debug````


### Step 4: Run protractor container with a volume to root of current cloned repo directory (that's where the protractor test files are)
````export FILES="//c/<directory-path-to-mpleijte/protractordemo>/protractor-tests"````
````winpty docker run -it --rm --net="host" -v $FILES:/src felippenardi/yo````
````dockercontainer$ protractor conf.js````


### Step 5 (Optional) view running tests with VNC viewer
#### In cygwin do
````$ docker ps````
````
CONTAINER ID        IMAGE                        COMMAND                  CREATED             STATUS              PORTS                     NAMES
25cb813e65ef        selenium/node-chrome-debug   "/opt/bin/entry_po..."   36 minutes ago      Up 36 minutes       0.0.0.0:32774->5900/tcp   vibrant_shockley
0e09f866db5a        selenium/node-chrome-debug   "/opt/bin/entry_po..."   About an hour ago   Up About an hour    0.0.0.0:32773->5900/tcp   hopeful_goldberg
ec4d9e5d3430        selenium/hub                 "/opt/bin/entry_po..."   About an hour ago   Up About an hour    0.0.0.0:32772->4444/tcp   selenium-hub
````

### In windows op vnc viewer
#### VNC connection parameters
servername = ```127.0.0.1:32773```
password = ```secret```


