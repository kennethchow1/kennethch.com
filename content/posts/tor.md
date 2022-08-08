---
title: "Tor"
date: 2022-07-08T12:23:02-07:00
draft: false
comments: false
images:
tags: 
  - tutorial
  - privacy
---
## Introduction
Tor, or known as the The Onion Router is a free and open source project with a goal to offer users around the world to surf the web anonymously. It is accomplished by relaying traffic and encrypted multiple times as it passes through multiple volunteer-run relays. 
Tor has become a vital tool for anyone looking to be truly anonymous and looking to bypass any government censorship or protect from any government surveillance. Tor is run by individuals who fully believe that everyone should be able to access the internet with complete privacy.
The best way to contribute to Tor and further their mission of providing individuals with privacy on the internet is to run a relay or a bridge.

###  What is a Bridge?
A Bridge is important to the Tor network because it serves as a private entrypoint that connects users to the Tor Network. Due to the IP address of both Guard/Middle and Exit relay being public. It can be easily blocked by any institution or government to block and prevent anyone from utilizing the Tor network. 

### What is a Relay?
There are two types of relays, Guard/Middle Relays and Exit Relays, Guard or Middle Relays are known to be the easiest and most common relay that is setup because there are minimal maintenance and bandwidth requirements.

Exit relay will always be at the end of the relay circuit. Therefore, any service or website that is being accessed by Tor users will see the exit relay IP address. Any abuse or complaints that is associated with the Exit Relay IP address will be passed onto the server owner and hosting provider. These relays are least common due to the inherent risks. Due to the inherent risks, these relays are the most valuable type of relay.

## Hosting a Tor Bridge
Hosting a bridge is the simpliest and easiest to host because it is easy, low-risk and low bandwidth which makes it perfect to be hosted from a home network.

*Note: It is important if you are hosting a Tor Bridge to not use an IP that has been used as a Tor Relay.* 


Prerequisites
Through testing, I have found that running a Tor Bridge using Docker and Debian is the easiest. 

### **Install Docker**
  In order to install Docker, you need to setup the official Docker Repository.

  1. Update the `apt` package repository:
  ```
  sudo apt update
  ```
  2. Install packages toe allow `apt` to use a repository over HTTPS:
  ```
  sudo apt install \
    ca-certificates \
    curl \
    gnupg \
    lsb-release
  ```
  3. Add Docker's GPG key:
  ```
  curl -fsSL https://download.docker.com/linux/debian/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
  ```
  4. Add the stable repository:
  ```
  echo \
    "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/debian \
    $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
  ```
  5. Update the `apt` repository:
  ```
  sudo apt update
  ```
  6. Install the *latest* Docker packages:
  ```
  sudo apt install docker-ce docker-ce-cli containerd.io
  ```
  7. Install the `wget` package:
  ```
  sudo apt install wget 
  ```
  8. Download the Docker Compose file:
  ``` 
  wget https://gitlab.torproject.org/torproject/anti-censorship/docker-obfs4-bridge/raw/main/docker-compose.yml 
  ```
  9. Create .env file:
   ```
  # Your bridge's Tor port.
  OR_PORT=X
  # Your bridge's obfs4 port.
  PT_PORT=Y
  # Your email address.
  EMAIL=Z
  ```
  *If you don't have an IPv6 Address* 
  - Add the following to the .env file
    ```  
    OBFS4_ENABLE_ADDITIONAL_VARIABLES=1
    OBFS4V_AddressDisableIPv6=1
    ```

  10. Deploy Docker Container: 
  ```
  docker-compose up -d obfs4-bridge
  ```


  - Monitor the Tor Bridge

    1. View all Docker Container List 
    ```
    sudo docker ps -a
    ```
    - Look for Container ID

    2. View Tor Bridge Logs
    ```
    sudo docker logs `CONTAINER ID`
    ```






