# Code Analysis for Software Security Engineering

## Code Review Strategy

Home Assistant is primarily written in Python but has a few .json and .yaml files inside different subfolders of the repository. Inside the [core](https://github.com/home-assistant/core) repository there are several folders including `docs`, `homeassistant`, `machine`, `rootfs`, `scripts`, `tests`, and several stand alone .txt/.yml/md files. Since our semester project focused on the actual software Home Assistant we chose to only look at the `homeassistant` folder inside the core repository. The `homeassistant` folder contained several subfolders and a few .py files with over 300,000 lines of code. We came together as a group and discussed the best way to analyze the codebase in a time efficient manner. Jose suggested we use the `Bandit` automated code review tool to scan the entire `homeassistant` repository to see what the results and based on the results we would de-scope non-applicable files/folder. We also decided collectively as a group to inspect some of the .py files that were directly related to the software assurance cases and misuse/use-cases we looked at over the course of the semester. We were particularly concerned with the `auth`, `util`, and `components` folders since after a quick manual review it was noted that these were most related to the work we have been doing over the course of the semester.

## Manual Code Review

<TODO> Insert Findings from manual code review of critical security functions identified in misuse cases, assurance cases, and threat models.

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
  * Total lines of code: 328174
  * Total lines skipped (#nosec): 2
- Run metrics:
   * Total issues (by severity):
       * Undefined: 0.0
       * Low: 201.0
       * Medium: 4.0
       * High: 16.0
   * Total issues (by confidence):
       * Undefined: 0.0
       * Low: 0.0
       * Medium: 3.0
       * High: 218.0
- Files skipped (0):

#### Key Findings

Bandit discovered 221 issues in total with 18 being rated High and 7 being rated Medium with each issue having their own `test_id`. We broke the `test_id` down into unique categories and attempted to map them to CVE's. A full list of vulnerabilities can be seen in the attached report.
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

### B102 Use of exec detected

### B301	Pickle and modules that wrap it can be unsafe when used to deserialize untrusted data, possible security issue.

### B303	Use of insecure MD2, MD4, MD5, or SHA1 hash function.

### B312	Telnet-related functions are being called. Telnet is considered insecure. Use SSH or some other encrypted protocol.

### B321	FTP-related functions are being called. FTP is considered insecure. Use SSH/SFTP/SCP or some other encrypted protocol.

### B401	A telnet-related module is being imported.  Telnet is considered insecure. Use SSH or some other encrypted protocol.

### B402	A FTP-related module is being imported.  FTP is considered insecure. Use SSH/SFTP/SCP or some other encrypted protocol.

### B506 Unsafe yaml.load Operation
Bandit discovered issue [B506](https://bandit.readthedocs.io/en/latest/plugins/b506_yaml_load.html) which was rated as a MEDIUM issue in the `homeassistant\util\yaml` folder for the `loader.py` [file](https://github.com/home-assistant/core/blob/dev/homeassistant/util/yaml/loader.py). The Bandit documentation recommended that `yaml.safe_load()` be used in this instance becuase it could potentially allow the instantiation of arbitrary objects.

### B605	Starting a process with a shell, possible injection detected, security issue.

<TODO> Insert summary of key findings from manual and/or automated scanning. This summary should include mappings to CWEs to describe categories of major findings.

## Contributions to Open-Source Project

### B506 Unsafe Yaml.load Operation Issue and Pull Request
We created [Issue 43918](https://github.com/home-assistant/core/issues/43918) in the Home Assistant `core` repository and created [Pull Request 43919](https://github.com/home-assistant/core/pull/43919) which fixed the issue. The proposed fix was to change `yaml.load(conf_file, Loader=SafeLineLoader) or OrderedDict()` to `yaml.load_safe(conf_file, Loader=SafeLineLoader) or OrderedDict()`. One of the contributors responded with "The yaml being loaded here is configured by the Home Assistant administrator as is expected to have full access to the system.". More information can be seen in the pull request. 

### Other Issues Here

## Team Reflection

This assignment, like the last one was kind of difficult to collaborate on remotely. We used the same project with two review style as last time, but the hardest part was trying to break up the work so each team member can contribute equally. We decided that we would break up some of the issues found by Bandit and map CWE's to the ones that we deemed "high risk" or "needed further investigation". Over the course of the semester our group has worked rather well together, and our group members were always willing to assist others and people responded to each other in a timely manner. Using the Discord server helped us collab and have group meetings with the ability to share the screen which came in handy as we reviewed the results from Bandit.  

## GitHub Project Board
[GitHub Repository](https://github.com/Chrs987/HomeAssistant/projects/7)
