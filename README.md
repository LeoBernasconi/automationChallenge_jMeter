# Automation challenge 2: Jmeter

Prepare a JMeter project to validate if the following endpoint support a throughput 5 request per second: 
https://api.stackexchange.com/docs/articles#order=desc&sort=activity&filter=default&site=stackoverflow&run=true

## Table of Contents

* [Introduction](#introduction)
* [Installation](#installation)
* [Usage](#usage)


## Introduction
The only non-functional requirement is to assert that the endpoint returns 5 valid responses per second. However, I've assumed that we need to iterate those calls during a certain period of time. 
To do so, and to make the test more flexible, two parameters have been defined. They allow the user to modify the number of request per seconds and the amount of time during those request should continue performing OK. Those parameters are: 
* rps (request per seconds): Set by default to 5 (as requested).
* totalTime: Number of seconds where the test will continue calling 5 rps. Set by default to 1.
*Both may be changed in the object "parameters" (indise the jmx file).*

## Installation

1. Verify that Java is installed in your computer, by opening the console/terminal and type "java --version".
2. If not, install Java: https://www.java.com/en/download/help/download_options.html.
3. Install Jmeter: https://jmeter.apache.org/download_jmeter.cgi
4. Download the file "getArticles.jmx" into some folder --> remember the place, it will be use when executing the test.

## Usage

How to execute the tests?
* From command line
  - Open the console/terminal and type [JmeterRootDirectory]\bin\jmeter -n -t [directory_where_the_jmx_file_is_downloaded]\getArticles.jmx -l [JmeterRootDirectory]/logFile0.log -e -o [JmeterRootDirectory]\results\
  - For example: C:\apache-jmeter-5.6.2\bin\jmeter -n -t C:\apache-jmeter-5.6.2\tests\getArticles.jmx -l C:\apache-jmeter-5.6.2\tests/logFile0.log -e -o C:\apache-jmeter-5.6.2\tests\results\
  - This will create a log file and a basic HTML report inside the directory "results" (both in [JmeterRootDirectory]) . You can open the html and check the results in [JmeterRootDirectory]/results/index.html
  - **If you need to execute the test more than once, you will need the delete the log file and the directory results (both in [JmeterRootDirectory]).**
* From the Jmeter UI
  - Open the console/terminal and go to [JmeterRootDirectory]/bin, type "jmeter" and ENTER (JmeterRootDirectory example: "C:\apache-jmeter-5.6.2\bin").
  - Verify that the listeners ("View Results Tree" and "Summary Report") are enable (by default they will be enabled, but for running the test it is highly recommended to disable themn because they consume memory and may affect the test results).
  - Click on "Start".
  - Click on a listener to see the results.
  - **Keep in mind that this execution is slower than the "command line" one.**
 * From server
   - This would be ***the ideal way for executing the tests*, because it will use server capabilities insteod of the local machine's ones.**
   - The steps are identical to the ones decribed on "From command line" option, but in the VM console/terminal.
