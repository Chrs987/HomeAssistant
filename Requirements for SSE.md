# Requirements for Software Security Engineering

## Essential Data Flows

### Case list

#### [Usecase 1](#use-case-1)

#### [Usecase 2](#use-case-2)

#### [Usecase 3](#use-case-3)

#### [Third-Party Add-ons Use Case](#use-case-4)

#### [Usecase 5](#use-case-5)

### Use Case 1

#### TODO: Insert Use Case Name

TODO: Insert use-case info

#### TODO: Misuse case Name

TODO: Insert info here

#### Prevention/Security Requirement

TODO: Assess alignment of security requirements derived from mis-use case analysis with advertised features of the open-source software. Review OSS project documentation and codebase to support your observations. Summarize your observations.

#### Diagram

TODO: Insert Diagram photo

 
#### [Return to top](#case-list)

### Use Case 2

#### TODO: Insert Use Case Name

TODO: Insert use-case info

#### TODO: Misuse case Name

TODO: Insert info here

#### Prevention/Security Requirement

TODO: Assess alignment of security requirements derived from mis-use case analysis with advertised features of the open-source software. Review OSS project documentation and codebase to support your observations. Summarize your observations.

#### Diagram

TODO: Insert Diagram photo


#### [Return to top](#case-list)

### Use Case 3

#### TODO: Insert Use Case Name

TODO: Insert use-case info

#### TODO: Misuse case Name

TODO: Insert info here

#### Prevention/Security Requirement

TODO: Assess alignment of security requirements derived from mis-use case analysis with advertised features of the open-source software. Review OSS project documentation and codebase to support your observations. Summarize your observations.

#### Diagram

TODO: Insert Diagram photo


#### [Return to top](#case-list)

### Use Case 4

#### Third-Party Add-ons Use Case

Jack wants to be able to integrate a new IoT device but has no official add-on support. Home Assistant's third-party add-on support is one of its main features, it pushes users to find or create a third-party add-on to use with their home automation set-ups. Home Assistant rates every third-party add-on from 6 to 1 and warns users that Home Assistant cannot guarantee the quality and security of third-party add-ons and to use at the users risk. Jack then searches the Home Assistant community add-ons to see if there is one that supports his new IoT device. He finds an add-on that supports his device but is rated as a 1. Jack does not notice this fact but is excited to integrate his new IoT device, so he copies the github link and home assistant does a git copy on the repo and installs it on Jack's system. The add-on asks for elevated system rights to be able to work with his new IoT device. Jack disables add-on protection to allow the add-on with elevated rights without a second thought. Jack is able to integrate his new IoT device within his Home Automation set-up.

#### Third-Party Add-ons Misuse Case

Joel is a hacker who likes to mess with others networks and devices. Joel creates a Home Assistant add-on that supports a very specific IoT device that has no official Home Assistant add-on support. He creates the add-on to run on the hosts network and require elevated system rights to run properly. He also adds a backdoor to the add-on code for him to gain control of the network and devices of users who download his add-on. Home Assistant limits add-ons with rights to run on the host network to be able to directly communicate with all other add-ons by name. This allows Joel to mess with Jack's network and connected IoT devices he has set up with Home Automation.

#### Prevention/Security Requirement

Risks of installing third-party add-ons is difficult for Home Assistant to control. Though they provide many warnings to the user that they cannot guarantee the quality or security of third-party add-ons. Home Assistant also rates third-party add-ons for users to be able to distinguish which third-party add-ons they recommend and don't recommend using with Home Assistant. All add-ons added to Home Assistant initially run on protection enabled mode which prevents add-ons from getting rights on the system, but Home Assistant allows users to disable this if add-ons require more rights but warns users that this could destroy their system. Home Assistant also uses an internal network that allows communication between add-ons by using names or alias so they are able to defend against outside threats. Home Assistant Community repository requires contributors to contact owners to discuss any contributions before adding an add-on to the repository, and requires two other developers to approve before the change is merged into the repository.

#### Diagram

TODO: Insert Diagram photo

#### [Return to top](#case-list)

### Use Case 5

#### TODO: Insert Use Case Name

TODO: Insert use-case info

#### TODO: Misuse case Name

TODO: Insert info here

#### Prevention/Security Requirement

TODO: Assess alignment of security requirements derived from mis-use case analysis with advertised features of the open-source software. Review OSS project documentation and codebase to support your observations. Summarize your observations.

#### Diagram

TODO: Insert Diagram photo


#### [Return to top](#case-list)

## Observation of Security-Related Configuration and Installation Issues


#### [Return to top](#case-list)

## Planning and Contribution

TODO: Insert repository, project board, and reflection
Include a link to your team GitHub repository that shows your internal project task assignments and collaborations to finish this task. 
Include a reflection of your teamwork for this assignment. What issues occurred? How did you resolve them? What did you plan to change moving forward? 

## Documentation Sources

TODO: Insert documents referenced above (if any)

#### [Return to top](#requirements-for-software-security-engineering)
