# Assurance Cases

### Assurance Case List

* #### [Home Assistant effectively stores and protects sensitive user information.](#assurance-case-1)

* #### [Home Assistant provides multiple Authentication Providers](#assurance-case-2)

* #### [Home Assistant minimizes the risk when  adding IoT devices](#assurance-case-3)

* #### [Home Assistant efficiently prevents users from installing malicious addons.](#assurance-case-4)

* #### [Home Assistant minimizes information disclosure during communication between remote networks and local instances](#assurance-case-5)

### Assurance Case 1
#### Home Assistant effectively stores and protects sensitive user information.

![Assurance Case 1 Diagram:](/images/Assurance_Case_1.PNG)

#### Evidence for Assurance Case 1
Home Assistant offers users the ability to edit the `configuration.yaml` file on the local network via a variety of different options. The `configuration.yaml` file is the base configuration file where users can add their [YAML]( https://yaml.org/) code to specify device settings. This gives users the ability to integrate devices that are not configurable through Home Assistants user interface. The `configuration.yaml` files is a plain-text file that is readable by anyone who has access to the file, as seen in rebuttal R1. The file contains API tokens, account usernames, and passwords. As seen in sub-claim C2, Home Assistant recommends users store their sensitive information in the [secrets.yaml]( https://www.home-assistant.io/docs/configuration/secrets/) file, which is a separate configuration file. `Secrets.yaml` allows users to replace sensitive information in the `configuration.yaml` file with `!secret`. `!secret` will tell the configuration file that the sensitive information is in `secrets.yaml`. However as seen in rebuttal R2, `secrets.yaml` still stores password information in plain test and resides in the same `config` folder as the `configuration.yaml` file. If the `config` folder is comprised, a malicious user will have access to sensitive account information and API keys. 

Sub-claim C3 and Evidence E1 and E2 help protect sensitive information by giving users different locations to store sensitive account information that is not in plain text. While `secrets.yaml` is mentioned in the Home Assistant setup documentation, they also mention [Keyrings]( https://www.home-assistant.io/docs/tools/keyring/) and [Credstash]( https://www.home-assistant.io/docs/tools/credstash/). E2 protects sensitive user data because there is no longer a `secrets.yaml` file in the base `config` folder. As seen in E1, sensitive data is replaced with `!secret` and will grab the sensitive data from Credstash or the Keyring. Credstash and Keyrings can still be compromised as seen in Undermine UM1. Sub-claims C4 focuses on Keyring and explains how sensitive information is stored on the Operating System and only accessible through password authentication (Evidence E3). Sub-claim C5 focuses on using Credstash which requires an Amazon Webservices (AWS) account set up and accounts must follow AWS password [guidelines]( https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_passwords_change-root.html) (Evidence E4). The passwords in E3 and E4 will protect sensitive user data from being compromised by a malicious user. Both Evidence E3 and E4 and their respective sub-claims allow more protection than what was offered in sub-claim C2. Now the standard user will not have to store a password in plaintext files that can be accessible by anyone on the local network.

Home Assistant resides on the local network and does not have any ports open to the internet when the device is initially set up, noted by Inference Rule IR1. Undercut UC1 undercuts IR1 because users can configure their device to allow SSH access by forwarding the appropriate ports on the device and their router. SSH does not come enabled by default and Home Assistant offers documentation on how to enable [SSH]( https://www.home-assistant.io/blog/2017/11/02/secure-shell-tunnel/). Sub-claim C6 claims that the user sets up SSH securely. Evidence E5 specifies that users should use SSH keys for authentication, it is also good practice to use SSH keys instead of passwords to prevent brute force password attempts. The documentation recommends authentication via SSH keys instead of passwords, but it does not inform the user to disable Password Authentication in the `sshd_config` file. As seen in Undermine UM2, if the user still has password authentication enabled the password can be brute forces. Sub-claim C7 says that if the user sets `PasswordAuthentication no` in the `sshd_config` file evidence E8 provides assurance that this is done by showing the setting in the `sshd_config` file.

Evidence E7 is directly stated in Home Assistants documentation. It prevents users from using SSH with their root account. They will need to create less privileged accounts to access Home Assistant over SSH, which is a good security practice, but their documentation does not specify how to create non-root accounts on a Linux based system, nor does it link to any sort of 3rd party documentation. This is a good security control and is standard practice amongst Cybersecurity professionals however Home Assistant documentation does not elaborate on this.

I would list sub-claim C7 and evidence E8 as a gap for Home Assistant configuration. While they do link to a [third party site]( https://docs.fedoraproject.org//en-US/Fedora/14/html/Deployment_Guide/s2-ssh-configuration-keypairs.html) with instructions on how to enable SSH keys, they should list in their configuration documentation that users should set `PasswordAuthentication no` similar to how they list `PermitRootLogin no` in evidence E7. Having ` PasswordAuthentication yes` and using SSH keys still allows malicious users the ability to brute force the password and with a user using an SSH key they will typically put less effort into creating a secure password.

Home Assistant should also list instructions on how to create non-root users so they can effectively secure their internet-facing machine with evidence E7. While evidence E7 will stop a malicious user from accessing the device as root if the user is unable to set up non-root users the control will fail. This is a gap in Home Assistants configuration documentation.

The final gap that I noticed was with evidence E6. [Fail2Ban]( https://pimylifeup.com/raspberry-pi-fail2ban/#:~:text=%20Installing%20and%20configuring%20Fail2ban%20%201%20Before,file%20called%20%E2%80%9C%20jail.conf%20%E2%80%9C..%20We...%20More%20) is a crucial piece of software used to secure Linux devices by blocking malicious connections. Fail2Ban works by scanning log files and looks for multiple unauthorized or failed login attempts and updates the device's firewall to block that IP address. It is a standard cybersecurity practice and it is recommended by cybersecurity professionals for users who open their SSH port up to the internet.

#### [Return to top](#assurance-case-list)

### Assurance Case 2
#### Home Assistant provides multiple Authentication Providers

![Assurance Case 2 Diagram:]("/images/Authenticaiton Case 2.jpeg")


#### Evidence for Assurance Case 2

Home Assistant offers the ability to customize your Home Assistant server to have different authentication methods. The ability to customize the security authentication for your server can be found in the `configuration.yaml` file that comes with Home Assistatant. Editing this file grants the user the ablility to choose between authenticating using Trusted Networks, Command Line Authentication, and Mulit Factor Authentication. As seen under R1, Subclaim 2 states that the `configuration.yaml` file which you use to configure the authentication providers is stored in plain text. This is true as it is a file that anyone who has access to the box can edit. Home Assistant recommends that credentials that are hardcoded into the `configuration.yaml` to be stored in a `secrets.yaml` which should be stored in a Keyring or Credstash instances as seen under E2. Home Assistant does state that any hard-coded usernames and password used in the `configuration.yaml` file is stored using a Hash and Salt as seen under E3.

Configuring your Home Assistant Server to use Trusted Networks is a fast and easy way for the user to make sure that there is secure authorization with the Home Assistant Server. The drawback with setting up internal Authentiction with Trusted networks can be seen under R1. R1 states that a flaw of using internal networks is if the advisary is already on the network, then the connection already "forms a trust". Since the only thing the Home Assisnt looks at within "Internal Networks" is what IP address the authenticaiton is comming from, this can lead to a securty flaw with the system. This Flaw is undermined though that if the malicious user is already on the network first authentication with the Home Assistant Server requires a manual login to preform the entire authentication, which can be seen within UM1 and E1. 

Another way Home Assistnat can be configured for authentication is using LDAP/RADIUS instances to manage user credentials as seen in R2. This is undermineded though that if the LDAP/RADIUS credential server is compromised then there is a security issue with to Home Assistant. This though is outside the realm of Home Assistant's policy as it does not manage external/third party Authentication Suites as seen in E4. 

Home Assistant also allows Multi-Factor Authentication to be configured for the Home Assistant server authentication. As seen in R4, if the Multi Factor Authentication is compromised an advisary can exploit this to gain access to the server. E6 though states that Multi Factor Authentication is solely third party (such as Google Authenticatior or Authy) which is not managaed by Home Assistant.

With Home assistant providing multiple ways for authentication it might provide multiple avenues for advisarys to attack the system as seen in R3. Home Assistant though by default only turns on the authentication prviders that you specify in then `configuration.yaml`. Any authentication providers that are not in said `configuration.yaml`, are truned off and no able to be used as seen in E5.

#### [Return to top](#assurance-case-list)

### Assurance Case 3
#### Home Assistant minimizes the risk when adding IoT devices

![Assurance Case 3 Diagram:](/images/IoT_Assurance_Case.png)

#### Evidence for Assurance Case 3

Home Assistant offers the ability to securely integrate various IoT devices in your home on a single platform. Home Assistant has community made integrations available for many devices, from light bulbs to cameras. Home Assistant rates the add-ons 1 – 6 based on the assigned Home Assistant API role. A rating of 1 means the user should trust this add-on source because it is likely to ask for elevated privileges. A rating of 6 means the integration is secure. Unless the device is not compatible with Home Assistant, as stated in R1. Then the user will have two options to add the device. The first is adding the device via Discovery. This tool will automatically discover and configure [compatible IoT devices](https://www.home-assistant.io/integrations/discovery/). If the device is not compatible with Discovery, the user will need to configure the configuration.yaml file, as stated in C4. The first evidence of the successful configurations is user should see the device in the Home Assistant user interface. The second is the user should be able to see the API data when pushed or polled. 

Unless the device is incompatible with Home Assistant but never integrated, the user will manually integrate the device with code, as stated In C3.  Unless the user interfaces the device directly, the device will interact with a third-party Python library created by the user. Once the library is published, the user will add the device to the integration manifest, as seen in E3. Home Assistant has a gap here because the third-party libraries are not verified for security vulnerabilities or malware by Home Assistant. The gap is left to be addressed by the user. They are to analyze the security rating and make a decision based on their knowledge of the source. Unless the library contains malicious code or add on and the community deems it safe. The IoT device's integration will later be scored again as follows: No Score, Silver, Gold, Platinum. No Score means the device will need to be manually configured and is using basic communication protocols. The silver rating means the integration will cope when things go wrong and not print exceptions or log retry attempts. The device will also provide basic statuses. Gold integrations will be able to survive poor conditions and can be easily configured via the user interface. Platinum integrations are the best. These integrations are easily configured via the user interface and fast because they are entirely async. 

Inference Rule 1 assumes that if the device is an IoT device, we can poll for data and possibly push instructions. Undercut 1 undercuts Inference Rule 1 because some manufacturers provide proprietary hardware for companies that offer a service. The company could demand the manufacturer lock the API with a password to avoid the device be used in another way other than originally intended. Otherwise, the IoT device should be able to be integrated. This claim will need to be further developed because the user will need to research if the device is already integrated with code and compatible with discovery. 


#### [Return to top](#assurance-case-list)

### Assurance Case 4
#### Home Assistant efficiently prevents users from installing malicious addons.

![Assurance Case 4 Diagram:](/images/Assurance_Case_4.png)

#### Evidence for Assurance Case 4
Home Assistant offers both officially supported add-ons as well as third-party add-ons to fully utilize the capabilities of home automation with Home Assistant. They encourage users to develop their own add-ons if there are not any officially supported or third-party add-ons that support devices that users want. They also encourage those who have created add-ons to contribute to the community by publishing them to the public. Home Assistant has even created a tutorial document for advanced users who want to begin [creating and publishing add-ons](https://developers.home-assistant.io/docs/add-ons). This feature is a major aspect of Home Assistant's usability and integration ability with home automation, but this also creates a major risk to the application security with the risk of malicious add-ons.

As you can see in Rebuttal R1, installing malicious add-ons are not the only security risk. With Home Assistant having to communicate with outside repositories when downloading add-ons and updates this adds a risk of a Man in The Middle attack. Home Assistant utilizes HTTPS encryption to try to prevent these attacks. Wireshark logs and update logs could also be implemented to watch any suspicious activity.

As for Rebuttal R2 with third-party add-ons, Home Assistant community-made third-party add-ons are all publicly published on [GitHub](https://github.com/hassio-addons), explained in sub-claim C2. To prevent any risk from installing any malicious third-party add-ons, Home Assistant warns users about the risk of installing add-ons multiple times shown on their [website](https://www.home-assistant.io/hassio/installing_third_party_addons/#:~:text=Installing%20third-party%20add-ons%20Home%20Assistant%20allows%20anyone%20to,you%20can%20use%20our%20example%20add-on%20repository%20at) and within the application. If the user still enables third-party add-ons such as said in Rebuttal R3, Home Assistant makes sure that it points to the official community add-on repo said in sub-claim C4. Evidence E5 states that Home Assistant provides quality ratings on all third-party add-ons within the community repository with 6 being very secure and 1 meaning that users should not install it unless they are 100% sure that they can trust the source. Evidence E4 supports this sub-claim as well by making sure that users provide a Github link that they can trust based on Evidence E5 as well as Evidence E6 which Home Assitant can utilize the [Github code scanner](https://github.blog/2020-09-30-code-scanning-is-now-available/) to find security vulnerabilities within the repositories. Though, if a user provides an unsupported/bad Github link stated in Undermine UM1, Sub-claim C5 states that Home Assistant runs all add-ons on separate self-contained docker containers to prevent any malicious add-on from taking over the system with Evidence E7 and E8 to support this claim from [Home Assistant add-on communication document](https://developers.home-assistant.io/docs/add-ons/communication) and [add-on configuration document](https://developers.home-assistant.io/docs/add-ons/configuration). Sub-claim C6 also states that all add-ons are run in protection enabled mode with Evidence E9 and E10 to support this claim from the [Add-on security document](https://developers.home-assistant.io/docs/add-ons/security) and the [Add-on configuration document](https://developers.home-assistant.io/docs/add-ons/configuration).

As for Home Assitant official add-ons, we presume that they are secure and if a vulnerability is found such as stated in Undercut UC1, Sub-claim C7 states that all officially supported add-ons are managed by the core team of Home Assistant and are frequently updated and monitored with logs stated in Evidence E11 and E12.

#### [Return to top](#assurance-case-list)

### Assurance Case 5
#### Home Assistant minimizes information disclosure during communication between remote networks and local instances.

![Assurance Case 1 Diagram:](/images/Assurance_Case_5.png)

#### Evidence for Assurance Case 5
Home Assistant offers users to have access to their Home Assistant integrations outside of the user's local network. This feature is developed by the founders of Home Assistant and serves Home Assistant Cloud (Otherwise known as [Nabu Casa](https://www.nabucasa.com/)) as an optional add-on on top of the traditional Home Assistant integration. The setup process for expanding your integration to allow remote access is rather seamless, with various amounts of [documentation supporting it](https://www.nabucasa.com/config/). To enable the remote access feature, while connected to your Home Assistant locally on a user's network, navigate to the options menu and toggle remote access, from their Home Assistant takes care of the rest. This feature allows users to enhance their Home Assistant integration with the ability to manage their home outside of their network. However, with the addition of this feature the risk of user's information being hijacked in transit from remote devices to an at home network increases.  

As discussed in R1, a concerning risk of any out of network communication is a Man in the Middle Attack. This is a type of attack in which a user stands between two communicating devices, and attempts to hijack data mid-transfer. However to combat this Home Assistant ensures that all traffic between the remote device and local network are encrypted, using [Let's Encrypt SSL certificates](https://www.nabucasa.com/config/remote/#how-it-works), ensuring that data can only be read by the local network. 

As for R2, we analyze the case in which an attacker obtains the secure certificate by other means. However, as explained in sub-claim C3 it is required that once a connection is established between two machines the local Home Assistant credentials are required in order to allow for [authorization](https://www.nabucasa.com/config/remote/#security). It's also a known feature, that Home Assistant allows tracking of all events done on both remote and local sessions allowing user [customized guard locks to be put in place](https://www.home-assistant.io/docs/authentication/). However, the storage of local credentials in Home Assistant is its own caveat that is covered in [Assurance Case 1](#assurance-case-1).

As discussed in R3, another possibility is that an attacker is able to generate their own key and attach it to your local Home Assistant instance. However as explained in sub-claim C4, connection certificates are only generated at setup time by Home Assistant or are manually configured on [network](https://www.nabucasa.com/config/remote/#remote-ui). This does bring one glaring worry, however, in the case of Home Assistant manually decrypting traffic while routing it from your remote device, to your Home Assistant integration. This vulnerability is publically announced by Home Assistant, and they verify that in no normal circumstance will they read the data in transit. The only situation in which they will decrypt user data is when being forced by a government body, as outline in Undermine UM2 and discussed in the official  [Home Assistant Documentation](https://www.nabucasa.com/config/remote/#security) 

#### [Return to top](#assurance-case-list)

## Reflection

This assignment went a lot smoother than the last one. The group adapted to the new format of cloning their own branch and merging it with the master branch once the Pull Request received two approvals. We worked together at the beginning of the assignment before the meeting with our professor to discuss the questions we had and to formulate a couple of assurance cases. Some of our assurance cases got a little carried away but we worked together to trim them down according to what we learned in class. Overall, we all agreed that the new process for our project board helped us work together and opened more channels of communication for the assignment. We will be sticking with the same format for the remainder of the class. 

## Planning and Contribution

To Project Board we utilized for this assignment can be viewed at [Assurance Cases Project Board](https://github.com/Chrs987/HomeAssistant/projects/3)


