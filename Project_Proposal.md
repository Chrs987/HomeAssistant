# Home-Assistant Project Proposal

## Operational Environment
The operational environment this project focuses on is the home environment. The software is used for personal use. 
  ### Systems Engineering View Diagrams
  #### Home Automation Overview
![Home Automation Overview](/images/home_automation_landscape.svg)
  #### Home Automation Core Architecture
![Home Automation Core Architecture](/images/ha_architecture.svg)
  #### Home Automation Component Architecture
![Home Automation Component Architecture](/images/component_interaction.png)
  #### Home Automation Full Architecture
![Home Automation Full Architecture](/images/ha_full_architecture.png)
  ### Security Needs
- Secure Addons
  - Addons should be regularly updated and not contain malicious content.
- Secure Communication
  - Home-Assistant acts as a hub for IoT devices.
  ### Security Features
- [Add-on security](https://developers.home-assistant.io/docs/add-ons/security) is implemented with add-on security rating from 1(worst)-6(best)
- [Integrated even logging](https://www.home-assistant.io/integrations/logger/)
- Home-Assistant does not ask for personal information unless needed -> [Privacy Policy](https://www.home-assistant.io/privacy/)
- Home-Assistant provides user [authentication](https://www.home-assistant.io/docs/authentication/)
  - Allows multi-factor authentication
- Home-Assistant runs locally, not dependant on cloud services
- Home-Assitant provides a [checklist](https://www.home-assistant.io/docs/configuration/securing/) for securing user Home-Assistant system.

## Team motivation for selecting this project.
Now more than ever Internet Of Things (IOT) devices are a staple of a modern home in 2020. Manufacturers from all corners of the globe are getting into the IOT market. With the variety of manufacturers and products, bringing them together and working within a single ecosystem makes the user experience alot better. Home Assistant helps bridge the gap between these differnt manufactures and enables users to use a variety of IOT /Smart Devices within their home/enviroment. 

As a team we all have IOT/Smart Devices  devices in our homes. Each one of us used differnt IOT devices from differnt manufacturers (Phillips, Amazon, Google, Apple to name some of them). Together, after researching topics reguarding IOT/Smart Device, we stumbled upon Home Assistant which helps blend all the ecosystems together.

## Open-Source Project Description of Home-Assistant 
- Home Assistant is a python based open source home automation system that allows users the ability to put local control and privacy first. It tracks the state of all the devices in the users home uniting them under a single mobile-friendly interface. Home Assistant takes control of all devices without storing any data in the cloud and lets the user set up advanced rules to control devices. 
- Activity
  - Contributors - 2,000+
  - Commits - 29,000+
  - Last Commit - 9/9/2020
  - Open Pull Request - 184
  - Closed Pull Request - 23,000+
  - Most Recent Pull Request - 9/9/2020
  - Open Issues - 998
  - Closed Issues - 15,000+
  - Most Recent Issue Opened - 9/9/2020
- Popularity
  - Information on how many downloads or active Home-Assistant users was unavailable, but Home-Assistant is talked about in present time on different technical magazines and journal sites such as [Linux Magazine](https://www.linux-magazine.com/Issues/2017/203/Home-Assistant), [ProductHunt](https://www.producthunt.com/posts/home-assistant), [Linux.com](https://www.linux.com/news/home-assistant-python-approach-home-automation-video/), and [OpenSource.com](https://opensource.com/article/17/7/home-automation-primer)
- Languages Used: Python (100.0%)
- Platform(s)
  - Available on different operation systems and hardware platforms. Home-Assistant is officially supported on Raspberry Pi and Docker but can be isntalled on Linux, Android, MacOS, and Windows.
    
 ## How to Contribute
  - Coding
    - Write code for a device, notification service, sensor or IoT thing
      - Fork the repository
      - Write Code
      - Ensure the tests work
      - Create Pull Request against dev branch
    - Improve the [Frontend](https://developers.home-assistant.io/docs/frontend/) of HomeAssistant
  - Helping Home-Assistant
    - Respond to issues with soluitons
    - Respond to questions in the [forums](https://community.home-assistant.io/)
    - Join the HomeAssistant Community on different social media platforms
      - [Discord](https://discord.com/invite/c5DvZ4e)
      - [Twitter](https://twitter.com/home_assistant)
      - [Facebook](https://www.facebook.com/homeassistantio)
      - [Reddit](https://www.reddit.com/r/homeassistant)
    - Be supportive and helpful to new users
  - Help improve [General Documentation](https://developers.home-assistant.io/docs/documenting/standards)
  - [Translation](https://developers.home-assistant.io/docs/translations)
    - Help translate HomeAssistant into other languages
  - Add a New [Intergration](https://developers.home-assistant.io/docs/development_index/)
    - GitHub is used for tracking issues not Feature Request. New features (intergrations) are tracked via their [Community Forum](https://community.home-assistant.io/c/feature-requests)
  - Documentation
    - Help write new documents or edit current documents on [Home-Assistant.io](https://www.home-assistant.io/)
    
 ## Contributor Agreement
- https://github.com/home-assistant/core/blob/dev/CODE_OF_CONDUCT.md
- https://github.com/home-assistant/core/blob/dev/CLA.md

 ## License 
The license used by Home Assistant is the Apache license 2.0, last revised in 2004. This license grants the developer a perpetual, worldwide, non-exclusive, no-charge, royalty-free, irrevocable copyright, and patent license. However, if the developer/distributor of the new software starts litigation against an entity for this work, the patent license specified is terminated on the date of filing the litigation. The Apache license also allows for redistribution of the source with or without modifications. If modifications occur, the developer must provide a notice that this work is a derivative of the original. The developer may also add their copyright statement, including license materials from other software. Any contributions made to the software will also be included under the same license unless specified. The license does not give the developer the rights to trade names, trademarks, service marks, or product names from the licensor. The license also specifies that the software provided is as-is and does not include any warranties. The document also specifies that the developer assumes the risk of using the files. Also, under no legal theories shall any contributor be liable for any damages or inability to work due to the software provided. Lastly, when redistributing, the developer is allowed to offer warranties or support for the work or derivative of this work. The support and warranty are the sole responsibility of the entity providing the service. 
When contributing to Home Assistant there is a [check list](https://developers.home-assistant.io/docs/development_checklist) to follow. All communication to external devices/services must be wrapped in an external Python library hosted on pipy. When adding new dependencies, they should be in the file “requirements_all.txt.” The file “.coveragerc” should be updated to exclude the platform is there is no test available or is the code uses a third-party library for communicating to devices/services. All submissions should also go through the [Black formatting tool](https://developers.home-assistant.io/blog/2019/07/31/black/) using the command Black –fast homeassistant tests. The [requirements for adding components](https://developers.home-assistant.io/docs/creating_component_code_review) are stricter than simple contributions. For example, existing constants should be from the const.py file, and widely used constants should also be in the file. Otherwise, it should be at the component level. Also, new requirements should be added to the manifest.json file and uploaded to PyPI. The developer should use the Voluptuous library to create a data validation schema. This schema stores the default settings parameters. Next, data can be shared on the platform using a hass.data[domain] call. It also recommended that home assistant only interact with objects and not make direct calls to the API. Pull requests should be as small as possible. Lastly, the event names should have a prefix of the domain name, and the documentation recommends that the component include tests to avoid further setbacks. 


## Security-Related History for Home-Assistant
Home Assistant has a large attack surface because it interacts and accepts commands and messages from many IoT devices. Considering IoT manufactures are continually releasing devices, many are still very vulnerable. Many devices still use default administrator credentials, which means bad actors can circumvent authentication, leading to accessing the network and the opportunity to circumvent more vital security features within the software. With continuous updates to the software, the CVE reports are limited. There are two CVE reports, one [Cross-Site scripting attack](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2017-16782), and a [sensitive information leak via an unauthenticated link in the API](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2018-21019). The API issue was present for about 175 releases before being patched by adding authentication to the API endpoint. The second CVE report focused on the cross-site scripting vulnerability. The vulnerability was a result of the markdown output was not sanitized. When working on the issue, the developer saw that a method call was missing, which caused the polymer template not to exist, correcting this fixed the vulnerability. The developer recommends that the project should take a closer look at what persistent notification markdown supports and possibly limit this to links and paragraphs only. Bugzilla had some installation bugs, but no vulnerability reports. The Development of Home Assistant primarily focuses on adding new features and fixing bugs. There are a few security updates, like the [implementation of Bandit](https://github.com/home-assistant/core/pull/28341) a known python vulnerability scanner, in order to catch [XML parsing vulnerabilities](https://github.com/home-assistant/core/pull/28302). 

## Planning and Contribution
TODO: Link to your team GitHub repository that shows your internal project task assignments and collaborations to finish this task. 
Github Project Boards (Links to an external site.)
TODO: Include a reflection of your teamwork for this assignment. What issues occurred? How did you resolve them? What did you plan to change moving forward? 
  - Our team has primarily been in contact over Discord and we decided to work on Home-Assistant for our OSS project. As a team, we each contributed information to the project proposal and commits can be viewed on Github in our repository [Home-Assistant](https://github.com/Chrs987/HomeAssistant/issues). We will be 

## Documentation Sources
 - [GitHub](https://github.com/home-assistant/core/blob/dev/README.rst)
 - Home-Assistant [Wiki](https://www.home-assistant.io/docs/)
 - Home-Assistant [Homepage](https://www.home-assistant.io/)
 - Home-Assistant [Developer Documentation](https://developers.home-assistant.io/)
