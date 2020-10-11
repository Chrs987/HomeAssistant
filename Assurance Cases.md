# Assurance Cases

### Assurance Case List

* #### [Home Assistant efecttively stores and protects sensitive user information.](#assurance-case-1)

* #### [INSERT NAME HERE](#assurance-case-2)

* #### [Home Assistant minimizes the risk when  adding IoT devices](#assurance-case-3)

* #### [Home Assistant efficiently prevents users from installing malicious addons.](#assurance-case-4)

* #### [INSERT NAME HERE](#assurance-case-5)

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
#### .red[TODO] Insert Assurance Case 2 Name

![Assurance Case 2 Diagram:](/images/)
.red[TODO] Insert Assuracne Case 2 Image

#### Evidence for Assurance Case 2

.red[TODO] Insert Evidence 2

#### [Return to top](#assurance-case-list)

### Assurance Case 3
#### .red[TODO] Insert Assurance Case 3 Name

![Assurance Case 3 Diagram:](/images/IoT_Assurance_Case.png)

#### Evidence for Assurance Case 3

.red[TODO] Insert Evidence 3

#### [Return to top](#assurance-case-list)

### Assurance Case 4
#### .red[TODO] Insert Assurance Case 4 Name

![Assurance Case 4 Diagram:](/images/Assurance_Case_4.PNG)
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


