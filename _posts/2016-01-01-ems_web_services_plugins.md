---
layout: post
title: EMS Web Service Plugins
date:   2016-01-01 00:00:00 +0000
categories: jekyll update
permalink: ems_web_services_plugins
---

## Stream AutoRouting 

This web service automatically forwards a stream to another EMS via RTMP. When a new stream is brought into the EMS, either by issuing a pullStream or by pushing a stream into the EMS, this web service issues an API command to automatically forward that stream to another EMS.

The AutoRouting web service has two configuration values which can be set in the config.ini file.

1. **Token**. If the token is defined, and not empty, the AutoRouting web service will only forward streams that have the token as part of their localStreamName.
   
2. **Destination\_uri.** The address of the computer you wish to forward the streams to.
   
        [StreamAutoRouter] 
        token = forwardthese 
        destination_uri = 192.168.2.58


## Stream Recorder 

This web service tells the EMS to automatically records streams.

When a new stream is created, this web service issues an API command to automatically record the stream. The user can also set how long the stream would be recorded (in seconds).

The destination for the recorded file must be set in the config.ini file.

    [StreamRecorder] 
    file_location = C:\xampp\htdocs\evowebservices\media\ 
    period_time = 60;

The maximum period\_time is 86399 (24 hours).


## Stream Load Balancer 

The Load Balancer web service ensures that a group of EMS instances maintain the same collection of inbound (source) streams.

When a new stream is created on one EMS, this web service will tell all the other EMS instances to also to and get that stream.

The list of EMS instances the Load Balancer will maintain is defined in the config.ini file:

    [StreamLoadBalancer] 
    destination_uri[] = 192.168.2.39 
    destination_uri[] = 192.168.2.38 
    destination_uri[] = 192.168.2.58 


## Amazon S3 HDS Upload 

This web service automatically uploads an HDS stream to an Amazon S3 storage instance.

As the EMS writes HDS chunks to disk, this web service uploads those file chunks to your Amazon S3 instance.

Your Amazon S3 access and secret key must be set in the config.ini file.

    [AmazonHDSUpload] 
    aws_access_key = '' 
    aws_secret_key = '' 
    default_bucket = 'ems-files' 
    bootstrap = 'bootstrap'

Bootstrap is the bootstrap file which should be included with the HDS chunks. If you are unsure what this should be, it should be left as ‘bootstrap’.


## Amazon S3 Upload HLS Chunk Plugin 

This web service automatically uploads an HLS stream to an Amazon S3 storage instance.

As the EMS writes HLS chunks to disk, this web service uploads those file chunks to your Amazon S3 instance.

Your Amazon S3 access and secret key must be set in the config.ini file.

    [AmazonHLSUpload] 
    aws_access_key = '' 
    aws_secret_key = '' 
    default_bucket = 'ems-files'

