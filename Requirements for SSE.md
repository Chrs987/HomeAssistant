# Requirements for Software Security Engineering

## Essential Data Flows

### Case list

#### [Usecase 1](#use-case-3)

#### [Updating Configuration.yaml](#use-case-2)

#### [Usecase 3](#use-case-3)

#### [Usecase 4](#use-case-4)

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

#### Updating Configuration.yaml Use Case

Bob was a user of a popular application called [IFTTT](https://ifttt.com/) and automated many of his IoT devices until they began their "Pro" subscription service which limited the number of integrations he could use unless he paid IFTTT's monthly subscription fee. Bob recently talked with his neighbor who shared a blog post about [HomeAssistant](https://blog.briancmoses.com/2020/09/ditching-ifttt-for-home-assistant.html) that discussed the advantages of bringing all IoT devices under a single hub. Being a not so savvy tech user Bob began researching, setting up HomeAssistant, and integrating all his IoT devices and hubs. Once Bob has all his IoT devices managed by HomeAssistant he begins creating his own automations similar to what he did on IFTTT. HomeAssistant handles all its automations inside the [Configuration.yaml](https://www.home-assistant.io/docs/configuration/) file which is editable via several official HomeAssistant add-ons: File Editor, Samba, and SSH. Bob enables Samba so he can input all his device information in the Configuration.yaml including his username, API tokens, and password information for his Ring Security System, Blink Camera System, and other IoT device accounts and sets up his automations similar to how he had it in IFTTT. 

#### Updating Configuration.yaml Misuse Case

Bobs neighbor, Kyle, comes over to Bobs house for a weekend BBQ with family and friends. Bob, being the not so tech savvy user, gives out his WiFi password to the party goers so they can use their mobile devices. While Kyle helped Bob get started on HomeAssistant, Kyle is experienced in IT and HomeAssistant and knows the ins and outs of the software. He connects to Bob's WiFi network, saving the password on his phone. When Kyle gets home, he gets on his laptop and connects to Bob's WiFi from his computer. Kyle knows that Bob just set up his HomeAssistant so he begins to try and connect to the device and see Bob's Configuration.yaml file. First Kyle tried connecting to localhost:8123 but noticed that it required a username and password preventing him from viewing the Configuration.yaml with the File Editor addon. Kyle then begins to see if Bob enabled his device to allow editing via Samba. Sure enough Bob enabled Samba and Kyle sees the Configuration.yaml file under his Network tab in file explorer. Kyle attempts to open the Configuration.yaml file and notices that all of Bob's passwords are listed as !secrets <AccountName>. 

#### Prevention/Security Requirement

To prevent the mis-use case, HomeAssisnt imploys several safety measures. To prevent an attacker from gaining access to the Configurations.yaml file, the web interface is protected by a password and multi-factor authentication to prevent bruteforce attacks. In the event that a user will enable the Samba addon, Samba requires password authentication and the attacking machine to be on the same local network. In the event that a malicious actor does gain access to the Configuration.yaml, HomeAssistant documentation suggests that users input sensitive data in a separate yaml file known as the secrets.yaml file. This fill will allow the user to input !secrets <AccountName> in place of the sensitive data and the Configuration.yaml file will pull the associated information based on the <Accountname>. HomeAssistant also gives the user the ability to store sensitive data in the systems Environmental Variables, storing passwords in an Amazon Web Services (AWS) server via [Credstash](https://github.com/fugue/credstash) or on a [keyring](https://github.com/jaraco/keyring) stored on the Operating System(OS). 

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

#### TODO: Insert Use Case Name

TODO: Insert use-case info

#### TODO: Misuse case Name

TODO: Insert info here

#### Prevention/Security Requirement

TODO: Assess alignment of security requirements derived from mis-use case analysis with advertised features of the open-source software. Review OSS project documentation and codebase to support your observations. Summarize your observations.

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

Each team member was assigned an issue related to 1 of the 5 use/misuse cases. We also used GitHub's [Project Board](https://github.com/Chrs987/HomeAssistant/projects/2) feature and added an "In Review" column so we could track issues that are currently in review. We created separate branches for each team-member and required them to submit a pull-request to the master branch instead of editing the master branch. Each team members pull request required 2 other team members to approve it before it was merged with the master branch. This allowed us to collaborate in the comment section and discuss different ideas on how to approach the assigned use/misuse case. We all met on Monday September 21st via Discord Voice Chat and discussed the potential use cases for the assignment. Mr. Schmitt utilized the screenshare function to give a brief demo of his HomeAssistant setup and overview of the software. The group engaged in a brief discussion and we hypothesized several use cases in preparation for the Tuesday meeting with the professor. We liked the ability to review each other’s changes before pushing it to master and having our own branch. We may change to having each of us "fork" the repository for future assignments, but all agreed that this method worked for now. 

## Documentation Sources

TODO: Insert documents referenced above (if any)

#### [Return to top](#requirements-for-software-security-engineering)
