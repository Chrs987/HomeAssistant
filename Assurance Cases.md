# Assurance Cases

### Assurance Case List

* #### [Home Assistant efecttively stores and protects sensitive user information.](#assurance-case-1)

* #### [INSERT NAME HERE](#assurance-case-2)

* #### [INSERT NAME HERE](#assurance-case-3)

* #### [INSERT NAME HERE](#assurance-case-4)

* #### [INSERT NAME HERE](#assurance-case-5)

### Assurance Case 1
#### Home Assistant effectively stores and protects sensitive user information.

![Assurance Case 1 Diagram:](/images/Assurance_Case_1.PNG)

#### Evidence for Assurance Case 1
Home Assistant offers users the ability to edit the `configuration.yaml` file on the local network via a variety of different options. The `configuration.yaml` file is the base configuration file where users can add their [YAML]( https://yaml.org/) code to specify device settings. This gives users the ability to integrate devices that are not configurable through Home Assistants user interface. The `configuration.yaml` files is a plain-text file that is readable by anyone who has access to the file, as seen in rebuttal R1. The file contains API tokens, account usernames, and passwords. As seen in sub-claim C2, Home Assistant recommends users store their sensitive information in the [secrets.yaml]( https://www.home-assistant.io/docs/configuration/secrets/) file, which is a separate configuration file. `Secrets.yaml` allows users to replace sensitive information in the `configuration.yaml` file with `!secret`. `!secret` will tell the configuration file that the sensitive information is in `secrets.yaml`. However as seen in rebuttal R2, `secrets.yaml` still stores password information in plain test and resides in the same `config` folder as the `configuration.yaml` file. If the `config` folder is comprised, a malicious user will have access to sensitive account information and API keys. 

#### [Return to top](#assurance-case-list)

### Assurance Case 2
#### .red[TODO] Insert Assurance Case 2 Name

![Assurance Case 2 Diagram:](/images/)
.red[TODO] Insert Assuracne Case 2 Image

#### Evidence for Assurance Case 2

.red[TODO] Insert Evidence 2

#### [Return to top](#assurance-case-list)

### Assurance Case 3
#### .red[TODO] Insert Assurance Case 3 Name

![Assurance Case 3 Diagram:](/images/)
.red[TODO] Insert Assuracne Case 3 Image

#### Evidence for Assurance Case 3

.red[TODO] Insert Evidence 3

#### [Return to top](#assurance-case-list)

### Assurance Case 4
#### .red[TODO] Insert Assurance Case 4 Name

![Assurance Case 4 Diagram:](/images/)
.red[TODO] Insert Assuracne Case 4 Image

#### Evidence for Assurance Case 4

.red[TODO] Insert Evidence 4

#### [Return to top](#assurance-case-list)

### Assurance Case 5
#### .red[TODO] Insert Assurance Case 5 Name

![Assurance Case 5 Diagram:](/images/)
.red[TODO] Insert Assuracne Case 5 Image

#### Evidence for Assurance Case 5

.red[TODO] Insert Evidence 5

#### [Return to top](#assurance-case-list)

## Reflection

.red[TODO] Insert Reflection

## Planning and Contribution

To Project Board we utilized for this assignment can be viewed at [Assurance Cases Project Board](https://github.com/Chrs987/HomeAssistant/projects/3)


