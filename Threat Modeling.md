# Design for Software Security Engineering


## Threat Model 1

### Threat Model 1 Level 1

TODO: Insert HTML Report


## Threat Model 2


### Threat Model 2 Level 1

TODO: Insert HTML Report


## Threat Model 3


### Threat Model 3 Level 1

![level1](/images/IoT.png)

[IoT Report](/reports/IoT_Report.pdf)


## Threat Model 4


### Threat Model 4 Level 1

TODO: Insert HTML Report


## Threat Model 5


### Threat Model 5 Level 1

TODO: Insert HTML Report

## Summary of Observations

TODO: Insert General Overall Summary Here

--------------------------

### Spoofing
Home Assistant is relatively secure because users usually access the server on a local network. As a result, an attacker would need access to the local network before attempting to circumvent security. However, Home Assistant has experienced spoofing vulnerabilities in the past. It has been possible to use the ["X-Forwarded-For” option to spoof the IP address](https://github.com/home-assistant/core/issues/14345#issuecomment-401324487) to one that is on the trusted list. This vulnerability allowed attackers to bypass authentication once on the network and change the IP address once one is banned in SSH brute force attempts.  The vulnerability was mainly an issue for users using a reverse proxy and trusted network simultaneously in their set up. Home Assistant specified the dangers of using these settings together, but users did not read the warning in some cases. [Changes have been made](https://github.com/home-assistant/core/pull/15204) to the code to address these issues. When running home Assistant, it is crucial to ensure the local network is secured and only trusted users have access. Securing the local network will help prevent spoofing.



### Tampering


### Repudiation


### Information Disclosure


### Denial of Service


### Elevation of Privilege

--------------------------

### Link to Repo

[GitHub Repo Link](https://github.com/Chrs987/HomeAssistant/projects/4)

### Reflection

TODO: Insert Reflection Here
