# Automation challenge 2: Jmeter

Prepare an JMeter project to validate if the following endpoint support a throughput 5 request per second: 
https://api.stackexchange.com/docs/articles#order=desc&sort=activity&filter=default&site=stackoverflow&run=true

## Table of Contents

* [Introduction](#introduction)
* [Installation](#installation)
* [Usage](#usage)


## Introduction
The only non-functional requirement was to assert that the endpoint return 5 valid responses per second. However, I've assumed that we need to iterate those calls during a certain time. 
To do so, and to make the test more flexible, two parameters have been defined. They allow the user to modify the number of request per seconds and the amount of time during those request should contionue performing OK. Those parameters are: 
* rps (request per seconds): Set by default to 5.
* totalTime: Number of seconds where the test will continue calling 5 rps. Set by default to 60.
Both may be changed in the object "parameters" (indise the jmx file).

## Installation

1. Verify that Java is installed in your computer, by opening the console/terminal and type "java --version".
2. If not, install Java: https://www.java.com/en/download/help/download_options.html.
3. Install Jmeter: https://jmeter.apache.org/download_jmeter.cgi

## Usage

How do to execute the tests?
* From command line
  -TBC
* From the Jmeter UI
  - Open the console/terminal and go to [JmeterRootDirectory]/bin, type "jmeter" and ENTER (JmeterRootDirectory example: "C:\apache-jmeter-5.6.2\bin").
  - Verify that the listeners () are enable.
  - Click on "Start"
  - Click on a listener to see the results.
  - *Keep in mind that this execution is slower than the "command line" one.*
 * From server
   - This would be *the ideal way for executing the tests*, because it will use server capabilities insteod of the local machine's ones.
   - The steps are identical to the ones decribed on "From command line" option, but in the VM console/terminal.
