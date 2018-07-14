FROM ubuntu:16.04


RUN apt-get update
RUN apt-get install -y curl

COPY . /app
WORKDIR /app


# Install dependencies.
RUN apt-get install -y unzip openjdk-8-jre-headless xvfb libxi6 libgconf-2-4

# Install Chrome.
RUN curl -sS -o - https://dl-ssl.google.com/linux/linux_signing_key.pub | apt-key add
RUN echo "deb http://dl.google.com/linux/chrome/deb/ stable main" >> /etc/apt/sources.list.d/google-chrome.list
RUN apt-get -y update
RUN apt-get -y install google-chrome-stable

# Install ChromeDriver.
RUN wget -N http://chromedriver.storage.googleapis.com/2.40/chromedriver_linux64.zip -P ~/
RUN unzip ~/chromedriver_linux64.zip -d ~/
RUN mv -f ~/chromedriver /usr/local/bin/chromedriver
RUN chown root:root /usr/local/bin/chromedriver
RUN chmod 0755 /usr/local/bin/chromedriver

# Install Selenium.
RUN wget -N http://selenium-release.storage.googleapis.com/3.13/selenium-server-standalone-3.13.0.jar -P ~/
RUN mv -f ~/selenium-server-standalone-3.13.0.jar /usr/local/bin/selenium-server-standalone.jar
RUN chown root:root /usr/local/bin/selenium-server-standalone.jar
RUN chmod 0755 /usr/local/bin/selenium-server-standalone.jar


# Install pip
RUN apt-get install -y python-pip
