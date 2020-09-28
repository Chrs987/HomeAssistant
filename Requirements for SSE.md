# Requirements for Software Security Engineering

## Essential Data Flows

### Case list

#### [IoT Device Risk](#use-case-1)

#### [Updating Configuration.yaml](#use-case-2)

#### [Usecase 3](#use-case-3)

#### [Third-Party Add-ons Use Case](#use-case-4)

#### [Usecase 5](#use-case-5)

### Use Case 1

#### IoT Device Risk Use Case

Bob, a Home Assistant software user, recently purchased a Tesla and wants to know if it is possible to control and monitor his Tesla through Home Assistant. He notices that it is possible to lock your car, control climate, track sensor data, and track location. Home Assistant relies on Tesla’s API to access this information, which requires Bob’s Tesla account username and password. This feature can be configured via the GUI or manually. Bob chooses to manually configure the add-on since he is implementing some additional security features and enabling SSH root access for convinience. Bob will be using a secrets.yaml file and the keyring, as recommended by the software documentation. 

#### IoT Device Risk Misuse Case

Bob has to a get-together, Joe a friend of a friend attends. After Bob shows a party trick of being able to control and view his car from his home automation system, Joe notices that Bob uses Home Assistant. Joe has some cybersecurity knowledge and has used Home Assistant before. He knows that the software interfaces with a third-party API to gain the appropriate information, and the credentials are usually saved in the configuration file or a secrets.yaml file in plain text. As the night goes on, Joe scans the network and sees Bob has an SSH port forwarded and takes note of the WAN IP. Joe uses the tcpdump app on his rooted Android phone to log packets on the network. He later looks over the logs and can see multiple API calls in http and makes note of the credentials. After going through the logs, Joe brute forces the simple password with a dictionary attack and gains complete access to Home Assistant because Bob enabled root access via SSH for convinience. Joe looks over the documentation for the Tesla add-on and sees that it reports location. Before he goes any further and risk detection, he comes up with a plan to burglarize the home with some friends while Bob is at work. Joe wants to use the location services via a home assistant or gain access to the Tesla credentials to monitor Bob’s location without his knowledge. 

#### Prevention/Security Requirement

Home Assistant recommends not allowing root access via SSH if forwarded to the public and is set up this way be default. The documentation also recommends the user create a secrets.yaml file to separate the configurations from the username and passwords. The documentation also recommends the use of a keyring to avoid storing passwords in plain text. Lastly, it is essential to secure SSH with a key rather than a password when exposing the device to the public to help prevent a compromise. 

#### Diagram

![Use-Case 1:](/images/Use-Case1.png)

 
#### [Return to top](#case-list)

### Use Case 2

#### Updating Configuration.yaml Use Case

Bob was a user of a popular application called [IFTTT](https://ifttt.com/) and automated many of his IoT devices. IFTTT began their "Pro" subscription service which limited the number of integrations he could use unless he paid IFTTT's monthly subscription fee. Bob recently spoke with his neighbor who shared a blog post about [HomeAssistant](https://blog.briancmoses.com/2020/09/ditching-ifttt-for-home-assistant.html) that discussed the advantages of bringing all IoT devices under a single hub. Being a not so savvy tech user Bob began researching, setting up HomeAssistant, and integrating all his IoT devices and hubs. Once Bob has all his IoT devices managed by HomeAssistant he begins creating his own automations similar to what he did on IFTTT. HomeAssistant handles all its automations inside the [Configuration.yaml](https://www.home-assistant.io/docs/configuration/) file which is editable via several official HomeAssistant add-ons: File Editor, Samba, and SSH. Bob enables Samba so he can input all his device information in the Configuration.yaml including his username, API tokens, and password information for his Ring Security System, Blink Camera System, and other IoT device accounts and sets up his automations similar to how he had it in IFTTT. 

#### Updating Configuration.yaml Misuse Case

Bobs neighbor, Kyle, comes over to Bobs house for a weekend BBQ with family and friends. Bob, being the not so tech savvy user, gives out his WiFi password to the party goers so they can use their mobile devices. While Kyle helped Bob get started on HomeAssistant, Kyle is experienced in IT and HomeAssistant and knows the ins and outs of the software. He connects to Bob's WiFi network, saving the password on his phone. When Kyle gets home, he gets on his laptop and connects to Bob's WiFi from his computer. Kyle knows that Bob just set up his HomeAssistant so he begins to try and connect to the device and see Bob's Configuration.yaml file. First Kyle tried connecting to localhost:8123 but noticed that it required a username and password preventing him from viewing the Configuration.yaml with the File Editor addon. Kyle then begins to see if Bob enabled his device to allow editing via Samba. Sure enough Bob enabled Samba and Kyle sees the Configuration.yaml file under his Network tab in file explorer. Kyle attempts to open the Configuration.yaml file and notices that all of Bob's passwords are listed as !secrets <AccountName>. Kyle then looks at the secrets.yaml file which is in the same folder as the Configuration.yaml file and retrieves all of Bob's sensitive information. 

#### Prevention/Security Requirement

To prevent the mis-use case, HomeAssisnt employs several safety measures. To prevent an attacker from gaining access to the Configurations.yaml file, the web interface is protected by a password and multi-factor authentication to prevent bruteforce attacks. In the event that a user will enable the Samba addon, Samba requires password authentication and the attacking machine to be on the same local network. In the event that a malicious actor does gain access to the Configuration.yaml, HomeAssistant documentation provides users the ability to input sensitive data in a separate yaml file known as the secrets.yaml file. This will allow the user to input !secrets <AccountName> in place of the sensitive data and the Configuration.yaml file will pull the associated information based on the <Accountname>. However the secrets.yamls file still stores information in plain text. HomeAssistant also gives the user the ability to store sensitive data in the systems Environmental Variables, storing passwords in an Amazon Web Services (AWS) server via [Credstash](https://github.com/fugue/credstash) or on a [keyring](https://github.com/jaraco/keyring) stored on the Operating System(OS). 

#### Diagram

![Use-Case 2:](/images/Use-Case2.PNG)

#### [Return to top](#case-list)

### Use Case 3

#### Home Assistant Cloud Use Case

Bob, a Home Assistant software user, recently stumbled upon the Home Assistant Cloud module built into Home Assistant. This module allows administrators of home assistant to interact with their “home IOT devices” from anywhere in the world. Bob is very interested in configuring his Home Assistant so that he can check on his house from anywhere and anytime. 

#### Home Assistant Cloud Risk Misuse Case

Bob must travel for his work, so he spends a lot of time in the airport terminals of numerous airports. Because Bob spends a lot of time in airports, he connects to multiple Wi-Fi networks across the world. Upon landing at his layover terminal Bob forgot to see if his garage door is shut. He attempts to connect to a Wi-Fi signal named “FREE AIRPORT WIFI” to check on the status of his garage door. Bob unknowingly connects to a compromised network which an advisory is listening to all the traffic going through the network.  

#### Prevention/Security Requirement

Nabu Casa has partnered with Home Assistant to offer users the ability to manage their Home Assistant instance remotely. When setting up cloud remote access, the Home Assistant local instance, connects to Nabu Casa’s entities and forms a trusted relationship between the boxes. From here the user connects to the Nabu Casa trusted Proxy to interact with the Home Assistant. One other step of security is that once the user connects to Nabu Casa’s proxy and then connects to the Home Assistant local instance, the user must log into the instance with their credentials as well.  Nabu Casa explains in its security section that their main weakness are possible Man in the Middle Attacks (MITM), but they can help spot them by looking at the certificate fingerprints that the local instance and the “waiting to authenticate” use provides, and their use of Lets Encrypt Certificate Transparency technologies which uses a list of public logs that record all certificates issued which allows the Home Assistant local instance spot if the certificate is being impersonated. 

#### Diagram

TODO: Insert Diagram photo


#### [Return to top](#case-list)

### Use Case 4

#### Third-Party Add-ons Use Case

Jack wants to be able to integrate a new IoT device but has no official add-on support. Home Assistant's third-party add-on support is one of its main features, it pushes users to find or create a third-party add-on to use with their home automation set-ups. Home Assistant rates every third-party add-on from 6 to 1 and warns users that Home Assistant cannot guarantee the quality and security of third-party add-ons and to use at the users risk. Jack then searches the Home Assistant community add-ons to see if there is one that supports his new IoT device. He finds an add-on that supports his device but is rated as a 1. Jack does not notice this fact but is excited to integrate his new IoT device, so he copies the github link and home assistant does a git copy on the repo and installs it on Jack's system. The add-on asks for elevated system rights to be able to work with his new IoT device. Jack disables add-on protection to allow the add-on with elevated rights without a second thought. Jack is able to integrate his new IoT device within his Home Automation set-up.

#### Third-Party Add-ons Misuse Case

Joel is a hacker who likes to mess with others networks and devices. Joel creates a Home Assistant add-on that supports a very specific IoT device that has no official Home Assistant add-on support. He creates the add-on to run on the hosts network and require elevated system rights to run properly. He also adds a backdoor to the add-on code for him to gain control of the network and devices of users who download his add-on. Home Assistant limits add-ons with rights to run on the host network to be able to directly communicate with all other add-ons by name. This allows Joel to mess with Jack's network and connected IoT devices he has set up with Home Automation.

#### Prevention/Security Requirement

Risks of installing third-party add-ons is difficult for Home Assistant to control. Though they provide many warnings to the user that they cannot guarantee the quality or security of third-party add-ons. Home Assistant also rates third-party add-ons for users to be able to distinguish which third-party add-ons they recommend and don't recommend using with Home Assistant. This prevents Jack/Users from installing third-party add-ons or at least cautions them. All add-ons added to Home Assistant initially run on protection enabled mode which prevents add-ons from getting rights on the system, but Home Assistant allows users to disable this if add-ons require more rights but also warns users that this could destroy their system. This built-in security feature prevents Joel's add-on from getting elevated system rights unless the user allows it. Home Assistant third-party add-ons are all designed for hass.io and this environment runs all add-ons as seperate docker containers and these containers communicate to the hassio_supervisor container and then interracts with homeassistant. All add-on containers are ran within an internal network to defend against outside threats. This prevents Joel from accessing the add-on backdoor he added to his add-on to attempt in gaining control of Jack's network and devices. A feature that Home Assistant could implement is a code analyzer when it pulls in the repository from github. This would allow them to scan the code for commonly used malware and trojans which would prevent Joel from using those commonly used malware and trojans.

#### Diagram

![Third-party Add-ons Use Case / Misuse Case Diagram](/images/Third-party_add-ons.png)

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

Lovelace offers users an [automation editor](https://www.home-assistant.io/getting-started/automation/) which gives users a clean and easy way to build their own automation. Here users can enable [Multi-factor authentication](https://www.home-assistant.io/docs/authentication/multi-factor-auth/) to add an extra level of security to their account. The automation editor converts the users newly created automation to yaml and saves it to the Configuration.yaml file. To give users a more robust editing experience HA offers several ways to directly edit the configuration.yaml file. In their [advanced configuration](https://www.home-assistant.io/getting-started/configuration/) page they list several ways to edit the configuration file by installing addons. 

The Samba and File Editor (both officially supported addons) allow users to access the Configuration.yaml file and add devices, api keys, account information, and other device information. For HA to communicate with some IoT devices, users are required to input their account information in the Configuration.yaml file so the HA can communicate with the API. When looking in Samba of File editor the user will notice that this information is stored in plain text. If the device is compromised as seen in [Use Case 2](#Use Case 2) a user can lose all of their account information. Since HA is only accessible on the local network and requires password authentication the risk of a users information being compromised is low. However, they do offer several features that will help protect sensitive data. The first being a separate file called the [secrets.yaml file](https://www.home-assistant.io/docs/configuration/secrets/). This file allows users to input the work `!Secret <AccountName>` in place of sensitive data, similar to the `.gitignore` file in GitHub. However both the secrets.yaml and configuration.yaml store passwords in plain text and reside in the same `config` folder. HA offers several more secure ways to store sensitive account information:
 - [Credstash](https://www.home-assistant.io/docs/tools/credstash/) - communicates with an AWS server hosting the secrets file.
 - [keyring](https://www.home-assistant.io/docs/tools/keyring/) - stores information in a password protected keyring on the OS.
 - [Enviornment Variables](https://www.home-assistant.io/docs/configuration/yaml/#using-environment-variables) - stores information in an environment variable on the OS.

The Configuration.yaml files is one of the main features that the software has to offer. Users will often share their Configuration.yaml file on GitHub so storing sensitive information outside of the Configuration.yaml. The ability to edit and share the Configuration.yaml gives more functionality to HA and allows users to manually add devices that were not discovered during setup. Often users find it easier to edit the Configuration.yaml file directly with Samba, FileEditor, or SSH instead of using the Lovelace GUI. 

Community built addons are what drives HA and give it most of its functionality. HA official supports several addons and allows community users the ability to create their own addons. HA encourages their userbase to create addon repositories (usually hosted on GitHub) and share it with other users for stuff that is not currently supported on HA. While these addons help improve the functionality of HA, it does open the device up for different misuse cases as seen in [Use Case 4](#Use Case 4). Without addons and community support HA will not be able to offer users a robust experience setting HA apart for the other competitors. Throughout the installation process and while our team brainstormed the use and misuse cases, we noticed that HA offers several security features that require the user to enable them. Several of the security features relied on the developer enabling them in their addon.

#### [Return to top](#case-list)

## Planning and Contribution

Each team member was assigned an issue related to 1 of the 5 use/misuse cases. We also used GitHub's [Project Board](https://github.com/Chrs987/HomeAssistant/projects/2) feature and added an "In Review" column so we could track issues that are currently in review. We created separate branches for each team-member and required them to submit a pull-request to the master branch instead of editing the master branch. Each team members pull request required 2 other team members to approve it before it was merged with the master branch. This allowed us to collaborate in the comment section and discuss different ideas on how to approach the assigned use/misuse case. We all met on Monday September 21st via Discord Voice Chat and discussed the potential use cases for the assignment. Mr. Schmitt utilized the screenshare function to give a brief demo of his HomeAssistant setup and overview of the software. The group engaged in a brief discussion and we hypothesized several use cases in preparation for the Tuesday meeting with the professor. We liked the ability to review each other’s changes before pushing it to master and having our own branch. We may change to having each of us "fork" the repository for future assignments, but all agreed that this method worked for now. One of the difficult parts about working on our own branch was parts that we collaborated on like the Planning and Contribution and Observation of Security-Related Configuration and Installation Issues sections. We worked together on these but only created one issue for each part. We plan on brainstorming a better idea for issues that require multiple group members to work on for our next assignment. 

## Documentation Sources
* [HA Add-on Communication](https://developers.home-assistant.io/docs/add-ons/communication)
* [HA Add-on Security](https://developers.home-assistant.io/docs/add-ons/security/)
* [HA Community Contribution Guidelines](https://github.com/hassio-addons/repository/blob/master/CONTRIBUTING.md)
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
