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


## Threat Model 5


### Threat Model 5 Level 1

TODO: Insert HTML Report

## Summary of Observations

TODO: Insert Summary Here

## Repudation

Home Assistant gives users the ability to view the system logs in several ways. The user can view it from the Lovelace Interface (the web GUI) or on the actual device itself in the `home-assistant.log` and `system_log_event` files on the host machine. Logging is done via [System Log](https://www.home-assistant.io/integrations/system_log/) which keeps track of all logged errors and warnings for the IoT devices the hub manages. Errors and warnings are posted as the event in the `system_log_event` file while more detailed logging is stored in the `home-assistant.log` file. 

--------------------------

TODO: Insert Analysis of Mitigated/Relevant Threat Models Here per HA WiKi

--------------------------

### Link to Repo

[GitHub Repo Link](https://github.com/Chrs987/HomeAssistant/projects/4)

### Reflection

TODO: Insert Reflection Here
