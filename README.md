# headlesschrome


This repository contains necessary docker images to run selenium based 
tests in an automated envrionment using headless chrome.


## Contents


### /headlesschrome

This folder contains the base image used to run the tests. It's built on
ubuntu 16.04 and prepares an image with selenium, chrome and chromedriver.
It also provides a couple tools, such as curl, pip etc.


This image is a base one, meaning that you shouldn't necessarily
change it to add in your tests. Building this container takes a long time
and if you're not going to add this to hub, you will want to prevent this
fro being built over and over again.

You'll need to build this one first before moving to test suites. You may 
simply use the shell script in the folder.

### /robot

This is a sample test suite. The test suit in there is built with 
robot-framework and python. I recommend adding as much folders as you need
in the root folder, working with the variety of the tools you need. 
This allows you to have a central point to run all your tests even if
they're built with different technologies.


The /robot folder shows how to set your test suite folder and docker image.


Basically, building on top of "headlesschrome", you should decide on two
directories, one for hosting the files and the second for outputs.


In this example, I chose

1. **/app** -> to keep the source files in.
2. **/output** -> to transfer the output files to.


Using ADD command, add your source files into the image.  
Using WORKDIR, specify your output folder so any generated source 
will be added under it.  
Run your tests using the absolute paths, or ideally using another script
to run all your scripts.  
Remember that headless chrome setup should be added to your source folder,
for more information, see test.robot.  


To build the test suite image, use this command

	docker build . -t bar


To run your tests and get the output folder, you'll need to run the container
in a specific way.
On unix-like systems:

	docker run -tiv ~/path/to/output/:/output bar


On windows, I recommend using cmd instead of bash.

	docker run -tiv C:\path\to\output:/output bar
Or with bash

	winpty docker run -tiv C:\path\to\output:/output bar



