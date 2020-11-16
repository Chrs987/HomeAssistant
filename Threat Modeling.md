# Design for Software Security Engineering


## Edit Configuration.Yaml Threat Model 1

![level1](/images/EditConfig.YamlFile.PNG)

TODO: Insert HTML Report

## Threat Model 2


### Threat Model 2 Level 1

TODO: Insert HTML Report


## Threat Model 3


### Threat Model 3 Level 1

![level1](/images/IoT.png)

[IoT Report](/reports/IoT_Report.pdf)


## Update Addon Threat Model 4

![level1](/images/Update_Addon.png)

[Update Addon Report](/reports/Update_Addon_Report.pdf)


## Threat Model 5


### Threat Model 5 Level 1

TODO: Insert HTML Report

## Summary of Observations

TODO: Insert General Overall Summary Here

## Repudation

Home Assistant gives users the ability to view the system logs in several ways. The user can view it from the Lovelace Interface (the web GUI) or on the actual device itself in the `home-assistant.log` and `system_log_event` files on the host machine. Logging is done via [System Log](https://www.home-assistant.io/integrations/system_log/) which keeps track of all logged errors and warnings for the IoT devices the hub manages. Errors and warnings are posted as the event in the `system_log_event` file while more detailed logging is stored in the `home-assistant.log` file. 

--------------------------

### Spoofing
Home Assistant is relatively secure because users usually access the server on a local network. As a result, an attacker would need access to the local network before attempting to circumvent security. However, Home Assistant has experienced spoofing vulnerabilities in the past. It has been possible to use the ["X-Forwarded-For” option to spoof the IP address](https://github.com/home-assistant/core/issues/14345#issuecomment-401324487) to one that is on the trusted list. This vulnerability allowed attackers to bypass authentication once on the network and change the IP address once one is banned in SSH brute force attempts.  The vulnerability was mainly an issue for users using a reverse proxy and trusted network simultaneously in their set up. Home Assistant specified the dangers of using these settings together, but users did not read the warning in some cases. [Changes have been made](https://github.com/home-assistant/core/pull/15204) to the code to address these issues. When running Home Assistant, it is crucial to ensure the local network is secured and only trusted users have access. Securing the local network will help prevent spoofing.



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
