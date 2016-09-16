---
layout: post
title: Installation
date:   2016-01-01 00:00:00 +0000
categories: jekyll update
permalink: installation
---

## Using PHP

### **Pre-requisites:**

- Web Server (EWS, Apache, Nginx)
- EMS (events enabled)



### **Getting evowebservices:**

The default evowebservices in EMS package is the one that runs on PHP. To be able to install the EMS with evowebservices, please see the installation guide [here](http://docs.evostream.com/ems_user_guide/installation). 

After installation, the evowebservices will be found here: `..\evo-webroot\evowebservices`



#### Distribution Content:

``` 
/evowebservices
├── config
│ 	├── config.ini
│ 	└── config.php
├── core_modules
│ 	└── evoapi-core.php
│   ├── ini-parser.php
│ 	└── s3-core.php
├── plugins
│ 	├── amazonhdsupload.php
│ 	├── amazonhlsupload.php
│ 	├── basehdsplugin.php
│ 	├── basehlsplugin.php
│ 	├── baseplugin.php
│ 	├── plugins.php
│ 	├── streamautorouter.php
│ 	├── streamloadbalancer.php
│ 	├── streamrecorder.php
│ 	└── transcoderesetter.php
├── evostream_copyright.txt
├── evowebservices.log
├── evowebservices.php
├── LICENSE.md
└── README.txt
```



### Starting evowebservices:

1. Enable the services to be used by configuring the `config.ini` file
2. Start the web server to be used, if EWS will be used, it is automatically started when EMS starts
3. Run EMS
4. The Event Notification System would now be receiving data from EMS and trigger the all enabled plugins





## Using Node.js

### **Pre-requisites:**

- Node.js
- npm
- EMS (events enabled)



### **Getting evowebservices:**

#### A. Windows

1. **Download** the evowebservices Windows batch file installer from our Github
   
   Link: <https://github.com/EvoStream/evowebservices-archives/tree/master/installers>
   
2. Double click on the .bat file to **install** evowebservices
   
   ``` 
   evowebservices-0.0.1-win-x64.bat
   ```
   
3. If the installation is successful, evowebservices will start automatically
   
   ``` 
   starting evowebservices using npm....
   
   > evowebservices@0.0.0 start C:\node_evowebservices\node_modules\evowebservices
   > node ./bin/www
   
   STARTED: evowebservices:server Listening on port 4000
   info: STARTED: evowebservices:server Listening on port 4000
   info: Get enabled Plugins
   ```



####  B. Linux Installation

1.  **Download** the evowebservices Bash Script file installer from our Github.
   
   Link: <https://github.com/EvoStream/evowebservices-archives/tree/master/installers>
   
2. Locate the installer file, **install** the script by typing this in terminal:
   
   ``` 
   ./evowebservices-0.0.1-linux-x64.sh
   ```
   
3. If the installation is successful, evowebservices will start automatically
   
   ``` 
   Starting EVOWEBSERVICES...
   
   > evowebservices@0.0.0 start /home/user/Desktop/node_modules/evowebservices
   > node ./bin/www
   
   STARTED: evowebservices:server Listening on port 4000 
   info: STARTED: evowebservices:server Listening on port 4000 
   info: Get enabled Plugins
   ```



### Starting evowebservices:

1. Run the evowebservices before starting EMS. Make sure the plugins in evowebservices is configured as well as the event notification system in the config.lua of the EMS.
2. Open your node command prompt and go to your evowebservices directory. Start the evowebservices by executing command:

``` 
npm start
```



![]({{site.baseurl}}/assets/npm_start.jpg)



**Note:** You may check the node console terminal and evowebservice log for errors. The evowebservices log is located on the evowebservices/logs directory