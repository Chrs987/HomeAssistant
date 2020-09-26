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

Bobs neighbor, Kyle, comes over to Bobs house for a weekend BBQ with family and friends. Bob, being the not so tech savvy user, gives out his WiFi password to the party goers so they can use their mobile devices. While Kyle helped Bob get started on HomeAssistant, Kyle is experienced in IT and HomeAssistant and knows the ins and outs of the software. He connects to Bob's WiFi network, saving the password on his phone. When Kyle gets home, he gets on his laptop and connects to Bob's WiFi from his computer. Kyle knows that Bob just set up his HomeAssistant so he begins to try and connect to the device and see Bob's Configuration.yaml file. First Kyle tried connecting to localhost:8123 but noticed that it required a username and password preventing him from viewing the Configuration.yaml with the File Editor addon. Kyle then begins to see if Bob enabled his device to allow editing via Samba. Sure enough Bob enabled Samba and Kyle sees the Configuration.yaml file under his Network tab in file explorer. Kyle attempts to open the Configuration.yaml file and notices that all of Bob's passwords are listed as !secrets <AccountName>. Kyle then looks at the secrets.yaml file which is in the same folder as the Configuration.yaml file and retrieves all of Bob's sensitive information. 

#### Prevention/Security Requirement

To prevent the mis-use case, HomeAssisnt employs several safety measures. To prevent an attacker from gaining access to the Configurations.yaml file, the web interface is protected by a password and multi-factor authentication to prevent bruteforce attacks. In the event that a user will enable the Samba addon, Samba requires password authentication and the attacking machine to be on the same local network. In the event that a malicious actor does gain access to the Configuration.yaml, HomeAssistant documentation provides users the ability to input sensitive data in a separate yaml file known as the secrets.yaml file. This will allow the user to input !secrets <AccountName> in place of the sensitive data and the Configuration.yaml file will pull the associated information based on the <Accountname>. However the secrets.yamls file still stores information in plain text. HomeAssistant also gives the user the ability to store sensitive data in the systems Environmental Variables, storing passwords in an Amazon Web Services (AWS) server via [Credstash](https://github.com/fugue/credstash) or on a [keyring](https://github.com/jaraco/keyring) stored on the Operating System(OS). 

#### Diagram

![Use-Case 2:](/images/Use-Case2.PNG)

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
With service like IFTTT starting to charge monthly fees for simple automations, users have been looking for free alternatives when it comes to automating their houses. HomeAssistant, while not as user friendly as IFTTT, is an Open Source Software that allows users to integrate their Internet of Things (IoT) devices and centrally manage them under HA's web interface. There is a slight learning curve, especially for users who have never written in yaml or experimented with a Raspberry Pi, when it comes to setting up HA but the installation process is very well documented on the HomeAssistant official [website](https://www.home-assistant.io/docs/). They also provide several [Youtube](https://www.youtube.com/results?search_query=home+assistant) tutorials that help users integrate different devices and walk them through the initial setup process.

The installation of HA can be tricky for newcomers to the IT world but the creators of the software document and explain each step thoroughly on their [Getting Started](https://www.home-assistant.io/getting-started/) wiki page. Users are required to obtain a Raspberry Pi and SD card and flash the HomeAssistant image to the SD card before inserting it into the Pi. Once the Pi is powered on the device will connect to the internet and begin downloading the latest version of HomeAssistant and enable the Web User Interface (UI) on http://homeassistant.local:8123. Once the installation is complete and the user can access the Web UI the [onboarding](https://www.home-assistant.io/getting-started/onboarding/) process beings.

When the user first goes to the Web UI, they are prompted to create the HA administrator account that has the ability to change everything. They will enter a 'Name' 'Username' and 'Password' that is used every time the user accesses HA. HA then asks for the devices primary location and states that this information is not shared outside of the users network. Next the user will begin onboarding (adding) IoT devices that can be discovered on their network. Not all devices will show up, some require the user to manually add once the initial setup is complete. Once the devices are discovered and added the user will be brought to the [Lovelace User Interface](https://www.home-assistant.io/lovelace/) showing all the connected devices and settings. The Lovelace interface allows users the ability to create new integrations, group devices based on area, add new devices, edit configuration settings, install addons, and manage their HA administrator account. 

Lovelace offers users an [automation editor](https://www.home-assistant.io/getting-started/automation/) which gives users a clean and easy way to build their own automation. Here users can enable [Multi-factor authentication](https://www.home-assistant.io/docs/authentication/multi-factor-auth/) and ad an extra level of security to their account. The automation editor converts the users newly created automation to yaml and saves it to the Configuration.yaml file. To give users a more robust editing experience HA offers several ways to directly edit the configuration.yaml file. In their [advanced configuration](https://www.home-assistant.io/getting-started/configuration/) page they list several ways to edit the configuration file by installing addons. 

The Samba and File Editor (both officially supported addons) allow users to access the Configuration.yaml file and add devices, api keys, account information, and other device information. For HA to communicate with some IoT devices, users are required to input their account information in the Configuration.yaml file so the HA can communicate with the API. When looking in Samba of File editor the user will notice that this information is stored in plain text. If the device is compromised as seen in [Use Case 2](#Use Case 2) a user can lose all of their account information. Since HA is only accessible on the local network and requires password authentication the risk of a users information being compromised is low. However, they do offer several features that will help protect sensitive data. The first being a separate file called the [secrets.yaml file](https://www.home-assistant.io/docs/configuration/secrets/). This file allows users to input the work `!Secret <AccountName>` in place of sensitive data, similar to the `.gitignore` file in GitHub. However both the secrets.yaml and configuration.yaml store passwords in plain text and reside in the same `config` folder. HA offers several more secure ways to store sensitive account information:
 - [Credstash](https://www.home-assistant.io/docs/tools/credstash/) - communicates with an AWS server hosting the secrets file.
 - [keyring](https://www.home-assistant.io/docs/tools/keyring/) - stores information in a password protected keyring on the OS.
 - [Enviornment Variables](https://www.home-assistant.io/docs/configuration/yaml/#using-environment-variables) - stores information in an environment variable on the OS.

The Configuration.yaml files is one of the main features that the software has to offer. Users will often share their Configuration.yaml file on GitHub so storing sensitive information outside of the Configuration.yaml. The ability to edit and share the Configuration.yaml gives more functionality to HA and allows users to manually add devices that were not discovered during setup. Often users find it easier to edit the Configuration.yaml file directly with Samba, FileEditor, or SSH instead of using the Lovelace GUI. 

Community built addons are what drives HA and gives it most of its functionality. HA official supports several addons and allows community users the ability to create their own addons. HA encourages their userbase to create addon repositories (usually hosted on GitHub) and share it with other users for stuff that is not currently supported on HA. While these addons help improve the functionality of HA, it does open the device up for different misuse cases as seen in [Use Case 4](#Use Case 4). Without addons and community support HA will not be able to offer users a robust experience setting HA apart for the other competitors.  

#### [Return to top](#case-list)

## Planning and Contribution

Each team member was assigned an issue related to 1 of the 5 use/misuse cases. We also used GitHub's [Project Board](https://github.com/Chrs987/HomeAssistant/projects/2) feature and added an "In Review" column so we could track issues that are currently in review. We created separate branches for each team-member and required them to submit a pull-request to the master branch instead of editing the master branch. Each team members pull request required 2 other team members to approve it before it was merged with the master branch. This allowed us to collaborate in the comment section and discuss different ideas on how to approach the assigned use/misuse case. We all met on Monday September 21st via Discord Voice Chat and discussed the potential use cases for the assignment. Mr. Schmitt utilized the screenshare function to give a brief demo of his HomeAssistant setup and overview of the software. The group engaged in a brief discussion and we hypothesized several use cases in preparation for the Tuesday meeting with the professor. We liked the ability to review each other’s changes before pushing it to master and having our own branch. We may change to having each of us "fork" the repository for future assignments, but all agreed that this method worked for now. One of the difficult parts about working on our own branch was parts that we collaborated on like the Planning and Contribution and Observation of Security-Related Configuration and Installation Issues sections. We worked together on these but only created one issue for each part. We plan on brainstorming a better idea for issues that require multiple group members to work on for our next assignment. 

## Documentation Sources
* [HA Add-on Communication] (https://developers.home-assistant.io/docs/add-ons/communication)
* [HA Add-on Security] (https://developers.home-assistant.io/docs/add-ons/security/)
* [HA Community Contribution Guidelines] (https://github.com/hassio-addons/repository/blob/master/CONTRIBUTING.md)
* [IFTTT](https://ifttt.com/)
* [Ditching IFTTT For HA](https://blog.briancmoses.com/2020/09/ditching-ifttt-for-home-assistant.html)
* [HA Configuration.yaml](https://www.home-assistant.io/docs/configuration/)
* [HA Documentation](https://www.home-assistant.io/docs/)
* [HA Getting Started](https://www.home-assistant.io/getting-started/)
* [HA Onboarding](https://www.home-assistant.io/getting-started/onboarding/)
* [HA Forums](https://community.home-assistant.io/)
* [HA Credstash](https://www.home-assistant.io/docs/tools/credstash/)
* [HA Keyring](https://www.home-assistant.io/docs/tools/keyring/)
* [HA Enviornment Variables](https://www.home-assistant.io/docs/configuration/yaml/#using-environment-variables)
* [HA Multi-factor authentication](https://www.home-assistant.io/docs/authentication/multi-factor-auth/)
* [Lovelace User Interface](https://www.home-assistant.io/lovelace/)
* [Automation Editor](https://www.home-assistant.io/getting-started/automation/)
* [Youtube Tutorials](https://www.youtube.com/results?search_query=home+assistant)
* [secrets.yaml file](https://www.home-assistant.io/docs/configuration/secrets/)

#### [Return to top](#requirements-for-software-security-engineering)
