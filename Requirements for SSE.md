# Requirements for Software Security Engineering

## Essential Data Flows

### Case list

#### [Usecase 1](#use-case-3)

#### [Updating Configuration.yaml](#use-case-2)

#### [Usecase 3](#use-case-3)

#### [Usecase 4](#use-case-4)

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

TODO: Insert repository, project board, and reflection
Include a link to your team GitHub repository that shows your internal project task assignments and collaborations to finish this task. 
Include a reflection of your teamwork for this assignment. What issues occurred? How did you resolve them? What did you plan to change moving forward? 

## Documentation Sources

TODO: Insert documents referenced above (if any)

#### [Return to top](#requirements-for-software-security-engineering)
