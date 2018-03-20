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
