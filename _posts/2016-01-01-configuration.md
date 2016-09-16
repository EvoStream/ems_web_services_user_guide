---
layout: post
title: Configuration
date:   2016-01-01 00:00:00 +0000
categories: jekyll update
permalink: configuration
---

## Configuring EMS Event Notifications

EMS Event Notifications must be configured to communicate with the EMS Web Services. The EMS configuration file must be modified as follows. Please view the [EMS User’s Guide](http://docs.evostream.com/ems_user_guide/table_of_contents) for more detailed information on configuring Event Notifications.

**config.lua:**

``` 
eventLogger= 
{
  sinks=
  { 
    {
      type="RPC", 
      url="http://192.168.2.39/evowebservices/evowebservices.php",    -- for php
      url="http://localhost:4000/evowebservices/",                    -- for node       
      serializerType="JSON",
      -- serializerType="XML" 
      -- serializerType="XMLRPC"
      enabledEvents= 
      { 
		"inStreamCreated",
		"inStreamClosed",
		"outStreamCreated",
		"timerCreated",
		"timerTriggered",
		"timerClosed",						
		"hlsMasterPlaylistUpdated",
		"hlsChildPlaylistUpdated",
		"hlsChunkClosed",
		"hdsMasterPlaylistUpdated",
		"hdsChildPlaylistUpdated",
		"hdsChunkClosed",
		"dashChunkClosed",
		"dashPlaylistUpdated"	
      }, 
    }, 
  }, 
```



The **`enabledEvents`** parameter is optional and allows you to specify only the events which you wish to receive. **If the enabledEvents section is not specified, all events will be generated.** The list of all possible events can be found above, and more detail on each event can be found in the EMS API Definition document.

The evowebservices rely on EMS Events being generated as follows:

1. **RPC – Remote Procedure Calls**
   
   Event details are transmitted to a remote host via HTTP POST. The EMS will ignore any response from the remote host.
   
   RPC sink configuration:
   
   ``` 
   type="RPC",
   url="http://localhost/evowebservices/evowebservices.php",       -- for php
   url="http://localhost:4000/evowebservices/",                    -- for node     
   serializerType="JSON" 
   ```
   
   The url field specifies the destination which will be accepting the HTTP POST event notifications. In this example, the web services are installed on the same computer that the EMS is running on (“localhost”). This value can be changed to the IP address of the computer running the web services.
   
   ​
   
2. **serializerType**
   
   Format for the event logs. The serializerType can in the format of JSON, XML or XMLRPC. 
   
   Sample format of JSON:
   
   ``` 
   {"payload":{"creationTimestamp":1349335053486.4370,"name":"","queryTimestamp":1349335053487.4370,"type":"NR","uniqueId":1,"upTime":1.0000},"type":"streamCreated"}
   ```





## Configuring the EMS Web Service Plugins

Every EMS Web Service is contained within a “**plugin**". Each plugin can be enabled or disabled, effectively turning on and off each web service. The EMS Web Service system allows many Web Service Plugins to be active at one time, allowing users to create an entire suite of features.

### A. Configuration file (config.ini/plugins.json)

The EMS Web Services has a primary configuration file for the plugins.

**For php:**  evowebservices > config > config.ini

**For node:** evowebservices > config > plugins.json

Turn on a plugin by changing the **disabled** to **enabled**. By default all plugins are disabled.

Plugin Configuration:

``` 
StreamLoadBalancer = disabled 
StreamAutoRouter = disabled
StreamRecorder = disabled
AmazonHDSUpload = disabled
AmazonHLSUpload = disabled 
```

See [EMS Web Service Plugins](http://docs.evostream.com/ems_web_services_user_guide/ems_web_services_plugins) for the detailed information of plugins.



### B. Logging (logging.json)

Available only on node. This is the configuration for the evowebservices log files and the log console. Go to **evowebservices > config > logging.json** for configuration.

Configuration options for logging:

``` 
{
  "options": {
    "level": "silly",    
    "handleExceptions": true,
    "json": false,
    "maxsize": 5242880
  }
```

- level - the logging level for logs
  
  There are 6 default levels in winston: 
  
  ``` 
  level 0 = silly (lowest)
  level 1 = debug
  level 2 = verbose
  level 3 = info
  level 4 = warn
  level 5 = error (highest)
  ```
  
- handleExceptions - Handling Uncaught Exceptions with winston
  
- json - log files are in json format otherwise log files are saved as string format
  
- maxsize - maximum size of the log file in KB