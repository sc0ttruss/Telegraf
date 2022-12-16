# Telegraph
A collection of log configuratoins for telegraph to import to influx, zinc etc.

Nginx log format for reading Chef infra nginx logs.  This example reads the logs with a given grok pattern and allows you to extract the http_x_ops_userid  (node_name from client.rb) and the https status code.  The output is currently into a file for future processing and in this example it is use to find all node_names where the status = 401(actually it outputs all status codes, but a simple cat outputfile.csv | grep "401" should pull out only the 401 status items).  Using this to track down particular node names which have issues authenticating to chef infra server. 

# installation 

Install the telegraph client in your host OS, instructions for such can be found from the [influx website](https://docs.influxdata.com/telegraf/v1.21/introduction/installation/)

## Pre-requisitess

some logs with the following format (if you have installed chef infra server you will have these already)

```
101.140.88.240 - - [2022-12-02T18:56:08+00:00]  \"GET /bookshelf/organization-e45g8her9t478hll82544je4b7774w7639/checksum-5ddfy7456674rf943h8793aevt27g1h4?AWSAccessKeyId=014tj94710vs6m8v7ff6ss9mwd7h3ks6n8369k22&Expires=1670041458&Signature=pepd9iwrlpPPS2kaMAOY%7NB6kkwpV%3D HTTP/1.1\" 200 \"0.000\" 2380 \"-\" \"Chef Client/16.11.7 (ruby-2.7.2-p137; ohai-16.10.7; x86_64-linux; +https://chef.io)\" \"-\" \"-\" \"-\" \"16.11.7\" \"algorithm=sha1;version=1.1;\" \"node_001_cloud.pri.va.te\" \"2022-12-02T18:56:08Z\" \"7rmr9y5ywppYvB/pElapJDD/Ptss=\" 1240 \"pscz2894-8365-0f5j-n4v6-02989628nnw3\"
```


# Testing

# usage for this example
copy the nginx.conf file into your config directory for telegraph in this case /etc/telegraf/telegraf.d/nginx.conf
now test if that file is operational

```
telegraf -config /etc/telegraf/telegraf.d/nginx.conf -test --debug
```

# Running
```
telegraf -config /etc/telegraf/telegraf.d/nginx.conf
```
