# Code Analysis for Software Security Engineering

## Code Review Strategy

Home Assistant is primarily written in Python but has a few .json and .yaml files inside different subfolders of the repository. Inside the [core](https://github.com/home-assistant/core) repository there are several folders including `docs`, `homeassistant`, `machine`, `rootfs`, `scripts`, `tests`, and several stand alone .txt/.yml/md files. Since our semester project focused on the actual software Home Assistant we chose to only look at the `homeassistant` folder inside the core repository. The `homeassistant` folder contained several subfolders and a few .py files with over 300,000 lines of code. We came together as a group and discussed the best way to analyze the codebase in a time efficient manner. Jose suggested we use the `Bandit` automated code review tool to scan the entire `homeassistant` repository to see what the results and based on the results we would de-scope non-applicable files/folder. For issues that `Bandit` found, we each manually inspected the specific file that was identified. We also decided collectively as a group to inspect some of the .py files that were directly related to the software assurance cases and misuse/use-cases we looked at over the course of the semester. We were particularly concerned with the `auth`, `util`, and `components` folders since after a quick manual review it was noted that these were most related to the work we have been doing over the course of the semester.

## Manual Code Review

Code that was reviewed 

 * [util/logging.py](https://github.com/home-assistant/core/blob/dev/homeassistant/util/logging.py)

[util/logging.py](https://github.com/home-assistant/core/blob/dev/homeassistant/util/logging.py)
Logging is an important part of all operating systems and applications [CWE-778: Insufficient Logging](https://cwe.mitre.org/data/definitions/778.html) recommends that detailed logging should be used so users/administrators can get an understanding of what is going on in the underlying system. Home Assistant offers different types of logs that can be enabled. Due to the importance of log reviews and CWE-778 and [CWE-532: Insertion of Sensitive Information into Log File](https://cwe.mitre.org/data/definitions/532.html) we chose this file as a part of our manual code review and because it was not flagged by bandit. Upon inspection of the code we see at line 15 that all sensitive data is filtered in logging messages and we also noted that issues [24982](https://github.com/home-assistant/core/issues/24982) was fixed to protect the stack frame from missing information. We concluded that CWE-778 is not applicable due to sufficient logging being taken and CWE-532 being not applicable due to the logger scrubbing all sensitive information.

 * [util/ssl.py](https://github.com/home-assistant/core/blob/dev/homeassistant/util/ssl.py)

SSL encryption is a vital piece of data transmission. According to [CWE-319](https://cwe.mitre.org/data/definitions/319.html), transmitting data in clear text is a weakness that will allow unauthorized actors to sniff and analyze network traffic. Home Assistant implements the use of TLS, which in some cases could be vulnerable. However, the Home Assistant team has followed [Mozilla corporation's best practices](https://wiki.mozilla.org/Security/Server_Side_TLS) to implementing TLS in a secure and modern way. Mozilla's modern recommendation supports TLS 1.3 and is not backward compatible, thus providing an extremely high level of security. 

The following are some of the technical details of Mozilla's Modern compatibility TLS best practices:
- Cipher suites (TLS 1.3): TLS_AES_128_GCM_SHA256:TLS_AES_256_GCM_SHA384:TLS_CHACHA20_POLY1305_SHA256
- Cipher suites (TLS 1.2): (none)
- Protocols: TLS 1.3
- Certificate type: ECDSA (P-256)
- TLS curves: X25519, prime256v1, secp384r1
- HSTS: max-age=63072000 (two years)
- Certificate lifespan: 90 days
- Cipher preference: client chooses

The rational behind the decisions are the following:
- All ciphers are forward sercret and authenticating.
- All cipher suites are strongs, allowing the client to choose will provide the best cipher supported.
- ECDSA certificates using P-256 is recomended because the benefit from using P-384 is negligible. 

* [util/yaml/loader.py](https://github.com/home-assistant/core/blob/dev/homeassistant/util/yaml/loader.py)

[util/yaml/loader.py](https://github.com/home-assistant/core/blob/dev/homeassistant/util/yaml/loader.py)
The loader.py file in the `util/yaml` folder is a customer loader written by the developers of Home Assistant and is responsible for loading the `!secrets` (sensitive information, passwords, API Passkeys, etc) from a source (CredStash, Env Variables, Keyring) to use in the `Configuration.yaml` file that allows Home Assistant to integrate with other devices. Because of the `!secrets` and loader.py [CWE-312](https://cwe.mitre.org/data/definitions/312.html) is not applicable. [CWE-20: Improper Input Validation](https://cwe.mitre.org/data/definitions/20) discusses the importance of insuring that input validation is used. We analyzed the code and noted that [yaml.SafeLoader](https://pyyaml.docsforge.com/master/api/yaml/safe_load/) for all sensitive information. One thing to note is that on like 324, Home Assistant will notify users that CredStash will be deprecated and removed in March 2021 which help prevents [CWE-477](https://cwe.mitre.org/data/definitions/477.html). We also noted that sufficient logging was enabled throughout the different functions in `loader.py`. After analyzing the rest of the code we noted no other CWEs or possible vulnerabilities.

## Automated Tool Findings

### Bandit

#### Overview

[Bandit](https://pypi.org/project/bandit) is a Python based tool designed to find common security issues in Python code. To do this it will process each file, build an AST from it, and run appropriate plugins against the AST nodes. Once bandit is done scanning the files it will generate a .csv report.

Bandit scans code based on Plugin ID Groupings and will flag issues in the code according to the table below:
 * ID	Description
 * B1xx	misc tests
 * B2xx	application/framework misconfiguration
 * B3xx	blacklists (calls)
 * B4xx	blacklists (imports)
 * B5xx	cryptography
 * B6xx	injection
 * B7xx	XSS

We had all the plugins enabled for our report.

#### Bandit [report](reports/Bandit-results.csv) for `homeassistant` folder:
- Code scanned:
   * Total lines of code: 410574
    * Total lines skipped (#nosec): 8
- Run metrics:
    * Total issues (by severity):
        * Undefined: 0.0
        * Low: 223.0
        * Medium: 7.0
        * High: 18.0
    * Total issues (by confidence):
        * Undefined: 0.0
        * Low: 0.0
        * Medium: 3.0
        * High: 245.0
- Files skipped (0):

#### Key Findings

Bandit discovered 248 issues in total with 18 being rated High and 7 being rated Medium with each issue having their own `test_id`. A full list of issues can be seen in the attached report. We manually inspected the files and code for each of the Bandit issues below and mapped them to an appropriate CWE. 
 - Test_ID
   * (1) B102 - [Use of exec detected](https://bandit.readthedocs.io/en/latest/plugins/b102_exec_used.html)
   * (1) B301 - [Pickle and modules that wrap it can be unsafe when used to deserialize untrusted data, possible security issue](https://bandit.readthedocs.io/en/latest/blacklists/blacklist_calls.html#b301-pickle)
   * (4) B303 -	[Use of insecure MD2, MD4, MD5, or SHA1 hash function](https://bandit.readthedocs.io/en/latest/blacklists/blacklist_calls.html#b303-md5)
   * (8) B312 -	[Telnet-related functions are being called. Telnet is considered insecure](https://bandit.readthedocs.io/en/latest/blacklists/blacklist_calls.html#b312-telnetlib)
   * (1) B321 -	[FTP-related functions are being called. FTP is considered insecure](https://bandit.readthedocs.io/en/latest/blacklists/blacklist_calls.html#b321-ftplib)
   * (6) B401 -	[A telnet-related module is being imported. Telnet is considered insecure](https://bandit.readthedocs.io/en/latest/blacklists/blacklist_imports.html#b401-import-telnetlib)
   * (1) B402 -	[A FTP-related module is being imported. FTP is considered insecure](https://bandit.readthedocs.io/en/latest/blacklists/blacklist_imports.html#b402-import-ftplib)
   * (1) B506	- [Use of unsafe yaml load. Allows instantiation of arbitrary objects](https://bandit.readthedocs.io/en/latest/plugins/b506_yaml_load.html)
   * (2) B605	- [Starting a process with a shell, possible injection detected](https://bandit.readthedocs.io/en/latest/plugins/b605_start_process_with_a_shell.html)

## Summary of Key Findings

A majority of the issues we found in Home Assistant came from the `components` folder. The [components](https://developers.home-assistant.io/docs/creating_integration_file_structure/#where-home-assistant-looks-for-integrations) folder is responsible for all the built-in integrations and is the location that Home Assistant looks at for integrations. Bandit did not map these findings to CWE’s, so we had to manually do so. To do so we created a section for each issue that was found by Bandit and assigned them to a different member of our group. Some issues required us to create a pull request or open an issue (see Contributions to Open-Source Project section below) for the respected vulnerability. Bandit did have links for each `test_id` that discussed in detail why Bandit flagged that specific `test_id` as an issue and proposed general fixes that could be done. We used this documentation to assess the `test_id` listed below for the specific file it was flagged in. 

### B102 Use of exec detected [CWE-78](https://cwe.mitre.org/data/definitions/78)
Bandit discovered the use of `exec()` in [components/python_script/__init__.py](https://github.com/home-assistant/core/blob/dev/homeassistant/components/python_script/__init__.py). CWE-78 discusses the dangers of using OS commands in code since an attacker could execute unexpected or dangerous commands directly on the operating system. The use of `exec()` was used on line 217 and was `exec(compiled.code, restricted_globals)`. Typically the risk here comes from when an unsanitized string is passed into the `exec` function, however we see in this case that [exec()](https://docs.python.org/3/library/functions.html#exec) takes in a code object instead of a string and a defined list of `globals` which is defined on line 200 named `restricted_globals`. We do not take issue to this and will not be creating a pull request.

### B301 Pickle and modules that wrap it can be unsafe when used to deserialize untrusted data, possible security issue [CWE-502](https://cwe.mitre.org/data/definitions/502)
According to Bandit documentation Pickle and modules that it wraps can be unsafe when used to deserialize untrusted data which can result in a possible security issue similar to what is described in CWE-502. Data that is deserialized should be fully trusted and sufficiently verified that it is valid to ensure that it has not been maliciously altered. Python typically uses the [Pickle](https://docs.python.org/3/library/pickle.html) function to perform serialization and deserialization. The file that was flagged [`__init__.py`](https://github.com/home-assistant/core/blob/dev/homeassistant/components/feedreader/__init__.py) in folder `components/feedreader` is used to support RSS/Atom feeds in Home Assistant. [Feedreader](https://www.home-assistant.io/integrations/feedreader) is a Home Assistant component that will poll feeds every hour and send entries into the event bus. While we did not see any evidence that the Feedreader component validates the serialized/deserialized data, we did note that Feedreader supports rather verbose logging that can be enabled. We also noted that the pickle function is only used to store and retrieve the RSS feeds once they have been retrieved (see `class StoreData` line 181) so we did not raise any issues since the data is stored locally on the device.

### B303	Use of insecure MD2, MD4, MD5, or SHA1 hash function. [CWE-916](https://cwe.mitre.org/data/definitions/916.html)
According to Bandit, there are some insecure implementation of hash functions in the following files:
- [components/demo/mailbox.py](https://github.com/home-assistant/core/blob/dev/homeassistant/components/demo/mailbox.py)
- [components/device_tracker/legacy.py](https://github.com/home-assistant/core/blob/dev/homeassistant/components/device_tracker/legacy.py)
- [components/emulated_hue/hue_api.py](https://github.com/home-assistant/core/blob/dev/homeassistant/components/emulated_hue/hue_api.py)
- [components/tts/__init__.py](https://github.com/home-assistant/core/blob/dev/homeassistant/components/tts/__init__.py)

According to the [CWE-916](https://cwe.mitre.org/data/definitions/916.html), the encryption scheme's weakness is not providing a sufficient computational level effort that would make the password cracking attack infeasible or expensive. After manually reviewing the files, it would not be beneficial to add salt to the encryption because the hashes are used to output data in a certain format expected by other program functions. [Mailbox.py](https://github.com/home-assistant/core/blob/dev/homeassistant/components/demo/mailbox.py) creates a mailbox intended to be a demo. The message being hashed is not relevant so this does not pose a security threat. For the file [legacy.py](https://github.com/home-assistant/core/blob/dev/homeassistant/components/device_tracker/legacy.py), the MD5 hash helps re-create the generation of the .jpg filename for an end user's Gravatar avatar picture using Gravatar's technique. This process does not have any security implications because it does not include any sensitive information being provided or produced. The [hue_api.py](https://github.com/home-assistant/core/blob/dev/homeassistant/components/emulated_hue/hue_api.py) file uses the MD5 hash to create the `unique_id` variable, which is added to a dictionary of data needed to change the status of a bulb. The `unique_id` is generated by taking the `entity_id` and running it through an MD5 hash. The `entity_id` is retrieved by using the function `create_list_of_entities`. After the entities are found, some error checking is done in the `get()` function on line 280. Due to the error checking and the `entity_id` being a way to identify an entity, there are no security implications. Regarding the [__init__.py](https://github.com/home-assistant/core/blob/dev/homeassistant/components/tts/__init__.py) file in the `tts` (Text-to-Speech) directory, the function generates the variable `msg_hash` using SHA1. The `msg_hash` is later combined and formated with other data to create the variable `key` on line 328. Next, the `key` is used to check if the TTS file is already present in memory or cached. If it is not, `async_get_tts_audio` on line 347 is called to create the TTS file, and the `key` is used to name the file. The variable `msg_hash` is only used to create a filename for a status message converted to speech. There are no security implications. For the various reasons listed above, the team decided not to submit a pull request on these results. 

### B312	Telnet-related functions are being called. Telnet is considered insecure. Use SSH or some other encrypted protocol.
Telnet is a communication protocol running on port 23 that transmits and receives data in plain text. [CWE-311](https://cwe.mitre.org/data/definitions/311.html) explains that the weakness is due to the software not encrypting sensitive or critical data. This gives actors the ability to eavesdrop. The file [sensor.py](https://github.com/home-assistant/core/blob/dev/homeassistant/components/hddtemp/sensor.py) uses telnet to run the command HDDTemp as a daemon to gain temperature information of the disk specified in the JSON file (line 120). Considering the vast array of devices and possible configurations, Home Assistant transmits this non-sensitive data through telnet. Although risky, the Home Assistant team's assumption that the local network is safe and the data transmitted is non-sensitive, we decided not to submit a pull request.

<<<<<<< HEAD
### B401	A telnet-related module is being imported.  Telnet is considered insecure. Use SSH or some other encrypted protocol.
Telnet is an outdated form of communication that does not use authentication to access a shell. [CWE-311](https://cwe.mitre.org/data/definitions/311.html) explains the weakness being; the software does not encrypt sensitive or critical information before storage or transmission. The lack of encryption could mean breaches of confidentiality, integrity, and accountability. The file [device_tracker.py](https://github.com/home-assistant/core/blob/dev/homeassistant/components/actiontec/device_tracker.py) uses telnet to get data for an Actiontec MI424WR (Verizon FIOS) router starting on line 93. After further research, the Actiontec MI424WR (Verizon FIOS) routers are outdated and do not support SSH. The only [work around](https://forums.verizon.com/t5/Fios-Internet/Remotely-restart-FIOS-MI424WR-Router/td-p/546593) found for safe remote access is to use an SSH device on the network to access the router. However, this solution is not feasible for Home Assistant, and the router is so outdated, there are likely little to none in use. For these reasons, so we decided not to submit a pull request. 

### B321	A FTP-related module is being called. FTP is considered insecure. Use SSH/SFTP/SCP or some other encrypted protocol.
FTP (File Transfer Protocol) is a standard networking protocol used for the transfer of files between a server and client across a network. [CWE-220](https://cwe.mitre.org/data/definitions/220) explains that the usage of an FTP server itself is a weakness, as the server stores sensitive data underneath the root directory that is accessible to the server's users. This grants files accessible to unauthorized actors in the system. The file [xiaomi/camera.py](https://github.com/home-assistant/core/blob/dev/homeassistant/components/xiaomi/camera.py) uses FTP to retrieve the latest video file from the Xiaomi FTP server starting on line 95. Upon [further reasearch](https://www.home-assistant.io/integrations/xiaomi/), this usage of FTP is intentional, as in order to maintain the ability to use the Xiaomi mobile app to view the live camera feed as well as the Home Assistant Integration. Usage of newer more secure technologies such as RTSP like most of the Home Assistant integrations would block the ability to use the Xiaomi mobile app features.
=======
### B321	FTP-related functions are being called. FTP is considered insecure. Use SSH/SFTP/SCP or some other encrypted protocol.

### B401	A telnet-related module is being imported.  Telnet is considered insecure. Use SSH or some other encrypted protocol.
Telnet is an outdated form of communication that does not use authentication to access a shell. [CWE-311](https://cwe.mitre.org/data/definitions/311.html) explains the weakness being; the software does not encrypt sensitive or critical information before storage or transmission. The lack of encryption could mean breaches of confidentiality, integrity, and accountability. The file [device_tracker.py](https://github.com/home-assistant/core/blob/dev/homeassistant/components/actiontec/device_tracker.py) uses telnet to get data for an Actiontec MI424WR (Verizon FIOS) router starting on line 93. After further research, the Actiontec MI424WR (Verizon FIOS) routers are outdated and do not support SSH. The only [work around](https://forums.verizon.com/t5/Fios-Internet/Remotely-restart-FIOS-MI424WR-Router/td-p/546593) found for safe remote access is to use an SSH device on the network to access the router. However, this solution is not feasible for Home Assistant, and the router is so outdated, there are likely little to none in use. For these reasons, so we decided not to submit a pull request. 

### B402	A FTP-related module is being imported.  FTP is considered insecure. Use SSH/SFTP/SCP or some other encrypted protocol.
>>>>>>> 5434afdc975f860483ac75291840b1fce350e411

### B506 Unsafe yaml.load Operation [CWE-20](https://cwe.mitre.org/data/definitions/20)
Bandit discovered issue [B506](https://bandit.readthedocs.io/en/latest/plugins/b506_yaml_load.html) which was rated as a MEDIUM issue in the `homeassistant\util\yaml` folder for the `loader.py` [file](https://github.com/home-assistant/core/blob/dev/homeassistant/util/yaml/loader.py) and mapped it to issue to CWE-20: Improper Input Validation. The Bandit documentation recommended that `yaml.safe_load()` be used in this instance becuase it could potentially allow the instantiation of arbitrary objects. 

### B605	Starting a process with a shell, possible injection detected, security issue [CWE-78](https://cwe.mitre.org/data/definitions/78)
Bandit discovered this issue for 2 individual commands in the same file [`scripts/macos/__init__.py`](https://github.com/home-assistant/core/blob/dev/homeassistant/scripts/macos/__init__.py). This particular file is used for installing/uninstalling Home Assistant on a users Mac computer, the first command can be found on line 33 `os.popen(f"launchctl load -w -F {path}")` to help install and line 44 `os.popen(f"launchctl unload {path}")` for uninstalling Home Assistant. CWE-78 discusses how an attacker could possibly exploit this issue and execute unexpected, dangerous commands directly on the operating system. The `[os.popen](https://docs.python.org/3/library/os.html#os.popen)` command is used to open a pipe to or from `cmd`. Since these 2 commands are used only for uninstalling and re-installing Home Assistant on the MacOS we did not deem this a vulnerability or exploit. 

## Contributions to Open-Source Project

### B506 Unsafe Yaml.load Operation Issue and Pull Request
We created [Issue 43918](https://github.com/home-assistant/core/issues/43918) in the Home Assistant `core` repository and created [Pull Request 43919](https://github.com/home-assistant/core/pull/43919) which fixed the issue. The proposed fix was to change `yaml.load(conf_file, Loader=SafeLineLoader) or OrderedDict()` to `yaml.load_safe(conf_file, Loader=SafeLineLoader) or OrderedDict()`. One of the contributors responded with "The yaml being loaded here is configured by the Home Assistant administrator as is expected to have full access to the system.". More information can be seen in the pull request. 


## Team Reflection

This assignment, like the last one was kind of difficult to collaborate on remotely. We used the same project with two review style as last time, but the hardest part was trying to break up the work so each team member can contribute equally. We decided that we would break up some of the issues found by Bandit and map CWE's to the ones that we deemed "high risk" or "needed further investigation". Over the course of the semester our group has worked rather well together, and our group members were always willing to assist others and people responded to each other in a timely manner. Using the Discord server helped us collab and have group meetings with the ability to share the screen which came in handy as we reviewed the results from Bandit.  

## GitHub Project Board
[GitHub Repository](https://github.com/Chrs987/HomeAssistant/projects/7)
