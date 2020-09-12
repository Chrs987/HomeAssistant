# Home-Assistant Project Proposal

## Operational Environment
The operational environment this project focuses on is the home environment. The software is used for personal use. 
  ### Systems Engineering View Diagram
TODO: Provide a diagram that identifies the systems engineering view (https://robinagandhi.github.io/swa/slides/lecture-1/systems-security-engineering.html#13) of the software in the hypothetical environment. 
  ### Security Needs
- Secure Addons
  - Addons should be regularly updated and not contain malicious content.
- Secure Communication
  - Home-Assistant acts as a hub for IoT devices. 
TODO: What are the threats perceived by users of the software in its intended operational environment? (If there are none or very few, then re-evaluate your project selection.)
  ### Security Features
TODO: Develop a list of security features in the software (Again, if there are none or very few, then re-evaluate your choice).

## Team motivation for selecting this project.

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
TODO: Discuss License, procedures for making contributions, and contributor agreements (https://opensource.guide/how-to-contribute/#orienting-yourself-to-a-new-project)
  https://github.com/home-assistant/core/blob/dev/LICENSE.md

## Security-Related History for Home-Assistant
Home Assistant has a large attack surface because it interacts and accepts commands and messages from many IoT devices. Considering IoT manufactures are continually releasing devices, many are still very vulnerable. Many devices still use default administrator credentials, which means bad actors can circumvent authentication, leading to accessing the network, and the opportunity to circumvent more vital security features within the software. With continuous updates to the software, the CVE reports are limited. There are two CVE reports, one Cross-Site scripting attack, and a sensitive information leak via an unauthenticated link in the API. The API issue was present for about 175 releases before being patched by adding authentication to the API endpoint. The second CVE report focused on the cross-site scripting vulnerability. The vulnerability was a result of the markdown output was not sanitized. When working on the issue, the developer saw that a method call was missing, which caused the polymer template to not exist, correcting this fixed the vulnerability. The developer recommends that the project should take a closer look at what persistent notification markdown supports and possibly limit this to links and paragraphs only. Bugzilla had some installation bugs, but no vulnerability reports. The Development of Home Assistant primarily focuses on adding new features and fixing bugs. There are a few security updates, like adding VPN integration. 

## Planning and Contribution
TODO: Link to your team GitHub repository that shows your internal project task assignments and collaborations to finish this task. 
Github Project Boards (Links to an external site.)
TODO: Include a reflection of your teamwork for this assignment. What issues occurred? How did you resolve them? What did you plan to change moving forward? 
  - Our team has primarily been in contact over Discord and we decided to work on Home-Assistant for our OSS project. As a team, we each contributed information to the project proposal and commits can be viewed on Github in our repository [Home-Assistant](https://github.com/Chrs987/HomeAssistant/issues). We will be 

## Documentation Sources
 - [GitHub](https://github.com/home-assistant/core/blob/dev/README.rst)
 - Home-Assistant [Wiki](https://www.home-assistant.io/docs/)
 - Home-Assistant [Homepage](https://www.home-assistant.io/)
