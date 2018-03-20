---
layout: post
title: EMS Web Service Plugins
date:   2016-01-01 00:00:00 +0000
categories: jekyll update
permalink: ems_web_services_plugins
---

## Stream AutoRouting

This web service automatically forwards a stream to another EMS via RTMP. When a new stream is brought into the EMS, either by issuing a `pullStream` or by pushing a stream into the EMS host, this web service issues an API command to automatically forward that stream to another EMS.

The AutoRouting web service has two configuration values which can be set in the config.ini file.

1. **token**. If the token is defined, and not empty, the AutoRouting web service will only forward streams to the destination that have the "token" as part of their localStreamName.
   
2. **destination\_uri.** The address of the computer you wish to forward the streams to.
   
   ``` 
[StreamAutoRouter]
token = stream
destination_uri = 192.168.2.3
   ```

In this configuration, all the localstreamnames with "**stream**" in the host EMS will forward the stream to the destination URI which is the *192.168.2.3*.

To verify, do `listStreams` on the destination server. You should see all the streams pushed to the destination.





## Stream Recorder

This web service tells the EMS to automatically records streams.

When a new stream is created, this web service issues an API command to automatically records the stream to an mp4 format. The user can also set how long the stream would be recorded in seconds.

The destination for the recorded file must be set in the config.ini file.

1. **file_location**. The destination location where the recorded file is saved
   
   **Notes:** 
   
   - Use an absolute pathing
   - Use double slash for folder separation if using Windows OS
   
2. **period_time**.  The period of time between pulses expressed in seconds between 1 and 86399. The maximum period\_time is 86399 (24 hours).
   
   ```   
[StreamRecorder]
file_location = "C:\\EvoStream\\media"
period_time = 60;    
   ```

In this configuration, all the streams pulled by EMS will automatically be recorded in the file location indicated with a period time of 60 minutes each file as long as the plugin and or the stream is running.





## Stream Load Balancer

The Load Balancer web service ensures that a group of EMS instances maintain the same collection of inbound (source) streams.

When a new stream is created on one EMS, this web service will tell all the other EMS instances to also to and get that stream.

The list of EMS instances the Load Balancer will maintain is defined in the config.ini file:

1. **destination_uri**.  The array of ip address where the inbound streams would be replicated to
   
   ``` 
[StreamLoadBalancer]
destination_uri[] = 192.168.2.3
destination_uri[] = 192.168.2.4
destination_uri[] = 192.168.2.5
   ```

In this configuration, all the server IPs listed *(192.168.2.3, 192.168.2.4, 192.168.2.5)* will have the same pulled streams as the host EMS.

To verify, do `listconfig` in all destination IPs. All pulled streams from the host EMS should also be pulled by the destination servers.





## Amazon S3 HDS Upload

This web service automatically uploads an HDS stream to an Amazon S3 storage instance.

As the EMS writes HDS chunks to disk, this web service uploads those file chunks to your Amazon S3 instance.

Your Amazon S3 access and secret key must be set in the config.ini file.

1. **aws_access_key**. The amazon aws s3 access key
   
2. **aws_secret_key**. The amazon aws s3 secret key
   
3. **default_bucket**. The bucket in amazon aws s3 where files will be uploaded
   
4. **bootstrap**. The bootstrap file included with the fragments
   
   **Note:** Bootstrap is the bootstrap file which should be included with the HDS chunks. If you are unsure what this should be, it should be left as ‘**bootstrap**’.
   
   ``` 
[AmazonHDSUpload]
aws_access_key = '1234567890'
aws_secret_key = 'ABCDEFGHIJ1234567890'
default_bucket = 'HDS_files'
bootstrap = 'bootstrap'    
   ```

In this configuration, all the HDS files to be created will automatically be uploaded on the Amazon S3 bucket inside *HDS_files*.

**Note:** All files created when the service is not running will not be included in upload



## Amazon S3 HLS Upload

This web service automatically uploads an HLS stream to an Amazon S3 storage instance.

As the EMS writes HLS chunks to disk, this web service uploads those file chunks to your Amazon S3 instance.

Your Amazon S3 access and secret key must be set in the config.ini file.

1. **aws_access_key**. The amazon aws s3 access key
   
2. **aws_secret_key**. The amazon aws s3 secret key
   
3. **default_bucket**. The bucket in amazon aws s3 where files will be uploaded
   
   ``` 
[AmazonHLSUpload]
aws_access_key = '1234567890'
aws_secret_key = 'ABCDEFGHIJ1234567890'
default_bucket = 'HLS_files'
   ```

In this configuration, all the HLS files to be created will automatically be uploaded on the Amazon S3 bucket inside *HLS_files*.

**Note:** All files created when the service is not running will not be included in upload

