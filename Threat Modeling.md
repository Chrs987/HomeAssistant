# Design for Software Security Engineering


## Edit Configuration.Yaml Threat Model 1

![level1](/images/EditConfig.YamlFile.PNG)

TODO: Insert HTML Report

## Threat Model 2


### Threat Model 2 Level 1

TODO: Insert HTML Report


## Threat Model 3


### Threat Model 3 Level 1

TODO: Insert HTML Report


## Update Addon Threat Model 4

![level1](/images/Update_Addon.png)

[Update Addon Report](/reports/Update_Addon_Report.pdf)


## Guest User Authentication Threat Model 5

![level1](/images/GuestAuth.png)

[Guest User Authentication](/reports/Guest_Auth_Report.htm)
## Summary of Observations

TODO: Insert General Overall Summary Here

## Repudation

Home Assistant gives users the ability to view the system logs in several ways. The user can view it from the Lovelace Interface (the web GUI) or on the actual device itself in the `home-assistant.log` and `system_log_event` files on the host machine. Logging is done via [System Log](https://www.home-assistant.io/integrations/system_log/) which keeps track of all logged errors and warnings for the IoT devices the hub manages. Errors and warnings are posted as the event in the `system_log_event` file while more detailed logging is stored in the `home-assistant.log` file. 

--------------------------

### Spoofing



### Tampering


### Repudiation


### Information Disclosure

Home Assistant does not require confidential user information however for some of the integration the user’s username and password must be stored on the device or a third-party service (i.e. Credstash, GitHub). While not specifically stated, communication between these third-party entities is done over HTTPS and in for Credstash, authentication is required while GitHub performs validation of checksums. We were unable to find documentation of this on the WiKi page, but we were able to verify this with the logs mentioned in the [Repudiation](#Repudiation) section. In the `home-assistant.log` file we can see how the device communicates with some of the external reactors in the DFD's created above and we can see that communication to external websites is done over [HTTPS](https://web.dev/why-https-matters/).  Home Assistant does not store any information in the cloud, so the only way for any personal information to be disclosed is if the device itself is compromised. As seen in their [WiKi](https://www.home-assistant.io/docs/authentication/) documentation, account credentials are stored on the device that host the Home Assistant software in the `.storage/` folder. If GitHub, Credstash, or any other third-party has a breach, that is out of scope of Home Assistants control and is not addressed by this review.

### Denial of Service


### Elevation of Privilege

--------------------------

### Link to Repo

[GitHub Repo Link](https://github.com/Chrs987/HomeAssistant/projects/4)

### Reflection

TODO: Insert Reflection Here
