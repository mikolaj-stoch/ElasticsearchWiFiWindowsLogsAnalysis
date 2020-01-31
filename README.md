# Elasticsearch Windows Wi-Fi logs

Elastisearch project for Windows Wi-Fi logs analysis.

## Getting Started

### Prerequisites

What things you need to install:
* WinlogBeat
* ElasticSearch
* Kibana

### Installing

For ElasticSearch and Kibana just unzip archives.
For WinlogBeat follow: [installation guide](https://www.elastic.co/guide/en/beats/winlogbeat/current/winlogbeat-installation.html)


## Running

### WinlogBeat
1.Put winlogbeat.yml in winlogbeat folder
2. Make sure that winlogbeat deamon is running

### ElasticSearch and Kibana

Just run appropriate .bat files.


## Example dashboard made in Kibana


![alt text](https://raw.githubusercontent.com/username/projectname/branch/path/to/img.png)

## Example commands for Kibana DevTool

### Add new log to database ( using an existing log id will overwrite log )
```
PUT winlogbeat-7.5.1/_doc/2137
{
"@timestap" : "Jan 19, 2020 @ 21:37:00.995",
"winlog":{
"event_data":{
"SSID": "SiecWiFi"
}}}
```
### Update log info
```
POST winlogbeat-7.5.1/_update/2137
{
"doc" : {
"winlog":{
"event_data":{
"Adapter": "Watykanski Adapter"
}}}}
```
### Change all logs with specific SSID to other SSID value
```
POST winlogbeat-7.5.1/_update_by_query
{
"script": {
"source": """
ctx._source.winlog.event_data.SSID='Siec Watykanu'""",
"lang": "painless"
},
"query" : {
"term" : {"winlog.event_data.SSID" : "FunBox2-8415" }
}}
```
### Show 100 logs ( only ID value )
```
GET winlogbeat-7.5.1/_search
{
"from" : 0, "size" : 100,
"_source": ["_id"]
}
```
### Show 100 logs ( only SSID value )
```
GET winlogbeat-7.5.1/_search
{
"from" : 0, "size" : 100,
"_source": ["winlog.event_data.SSID"]
}
```
### Show logs with specific SSID value
```
GET winlogbeat-7.5.1/_search
{
"query" : {
"term" : {"winlog.event_data.SSID" : "TorysNET" }
}}
```
### Delete log
```
DELETE winlogbeat-7.5.1/_doc/2137
```
