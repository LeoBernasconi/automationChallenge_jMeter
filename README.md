# Automation challenge 2: Jmeter

Prepare a JMeter project to validate if the following endpoint support a throughput 5 request per second: 
https://api.stackexchange.com/docs/articles#order=desc&sort=activity&filter=default&site=stackoverflow&run=true

## Table of Contents

* [Introduction](#introduction)
* [Installation](#installation)
* [Usage](#usage)
* [Conclusions](#conclusions)


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
  - The first action will be to identify the [JmeterRootDirectory] (the place where jmeter has been installed). It will be used in the further steps.
  - Open the console/terminal and type [JmeterRootDirectory]\bin\jmeter -n -t [directory_where_the_jmx_file_is_downloaded]\getArticles.jmx -l [JmeterRootDirectory]/logFile0.log -e -o [JmeterRootDirectory]\results\
  - For example: C:\apache-jmeter-5.6.2\bin\jmeter -n -t C:\apache-jmeter-5.6.2\tests\getArticles.jmx -l C:\apache-jmeter-5.6.2\tests/logFile0.log -e -o C:\apache-jmeter-5.6.2\tests\results\
  - This will create a log file and a basic HTML report inside the directory "results" (both in [JmeterRootDirectory]/tests) . You can open the html and check the results in [JmeterRootDirectory]/results/index.html
  - **If you need to execute the test more than once, you will need the delete the log file and the directory results (both in [JmeterRootDirectory]).**
* From the Jmeter UI
  - Open the console/terminal and go to [JmeterRootDirectory]/bin, type "jmeter" and ENTER (JmeterRootDirectory example: "C:\apache-jmeter-5.6.2\bin").
  - Open the file getArticles.jmx.
  - Verify that the listeners ("View Results Tree" and "Summary Report") are enable (by default they will be enabled, but for running the test it is highly recommended to disable themn because they consume memory and may affect the test results).
  - Click on "Start" (the green arrow in the top menu).
  - Click on a listener to see the results.
  - **Keep in mind that this execution is slower than the "command line" one.**
 * From server
   - This would be ***the ideal way for executing the tests*, because it will use server capabilities insteod of the local machine's ones.**
   - The steps are identical to the ones decribed on "From command line" option, but in the VM console/terminal.

How to read the reports?
* Download them to a local directory.
* Go to directory \results and click on "index.html".
* A Jmeter report will be shown with different tabs (see left menu).

## Conclusions
* The first conclusion is that the API is protected from being overloaded. After some debugging (with some 200 response code), I started to receive 502 response code with the following body: {"error_id":502,"error_message":"too many requests from this IP, more requests available in 84268 seconds","error_name":"throttle_violation"}. That means that after little traffic the server activates some security process and block the suspicious IP for 24 hours.
* Once those 24 hours has passed, I could generate two reports:
  1. Calling the API 5 times during 1 seconds
     - All request return 200 status code with an average of 548.40 milliseconds
     - Summarizing all request, 4.44 request were worked per second
  2. Calling the API 5 times during 1 minute (60 seconds)
     - 300 request were calling during one minute. The average time response was 120.31 milliseconds.
     - 48.33% of the request shown 400 errors (145 out of 300)
     - Summarizing all request, 4.48 request were worked per second (almost the same as the previous execution)
* After that, I've started to received "throttle violation" errors again. So I was not able to go ahead with more tests.
