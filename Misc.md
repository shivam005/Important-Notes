# Important-Notes
Message Enpoints:  

Adapters: to connect another system  

Filter: to remove  

Transformer: to convert contect or structure  

Enricher: add content  

Service Activator: Invoke service operations

Gateway: connect your channel without SI coupling
There are 2 types of message channel: Pollable and subscribable 

JpaRepository>PagingAndSortingRepository>CrudRepository>Repository 

Program to an interface not an implementation

Favor object composition over inheritance

Steps followed by computer when it starts::
The CPU starts and fetches instructions into RAM from the BIOS, which is stored in the ROM.
The BIOS starts the monitor and keyboard, and does some basic checks to make sure the computer is working properly. For example, it will look for the RAM.
The BIOS then starts the boot sequence. It will look for the operating system.
If you don’t change any of the settings, the BIOS will fetch the operating system from the hard drive and load it into the RAM.
The BIOS then transfers control to the operating system.

Spring Security:: https://github.com/eazybytes/springsecurity6

Eight falacies of distributed computing, describing false assumptions that programmers new to distributed applications invariably make.
https://en.wikipedia.org/wiki/Fallacies_of_distributed_computing

## To Find IP of System
ifconfig | grep "inet " | grep -Fv 127.0.0.1 | awk '{print $2}'

## Script to read csv 
```
import requests
import json
import uuid
import csv
from time import sleep
from datetime import datetime, timedelta

# API endpoint
whiteListedQ = ["somedata"]
with open('/filePath/', 'r') as file:
    reader = csv.reader(file)
    index = 0
    start_row = 0
    for row in reader:
        if index == 0:
            index += 1
            continue
        if index < start_row:
            index += 1
            continue
        try:
            zeroData = row[0]
            firstData = row[1]
            tid = str(uuid.uuid4())
            secondData = json.loads(json.loads(row[3]))
            thirdData = json.loads(json.loads(row[4]))

        try:
                if response.status_code == 200:
                    print(
                        "success")
                else:
                    print(
                        f"Failed to send row {index + 1}: HTTP status {response.status_code}, Response text: {response.text}")
            else:
                print(f"skipping row={index + 1}")
        except json.JSONDecodeError as e:
            print(f"Error decoding JSON from row {index + 1}: {str(e)}")

        except Exception as e:
            print(f"An error occurred with row {index + 1}: {str(e)}")
        index += 1

```
