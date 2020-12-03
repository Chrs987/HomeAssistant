# Code Analysis for Software Security Engineering

## Code Review Strategy

Home Assistant is primarily written in Python but has a few .json and .yaml files inside different subfolders of the repository. Inside the [core](https://github.com/home-assistant/core) repository there are several folders including `docs`, `homeassistant`, `machine`, `rootfs`, `scripts`, `tests`, and several stand alone .txt/.yml/md files. Since our semester project focused on the actual software Home Assistant we chose to only look at the `homeassistant` folder inside the core repository. The `homeassistant` folder contained several subfolders and a few .py files with over 300,000 lines of code. We came together as a group and discussed the best way to analyze the codebase in a time efficient manner. Jose suggested we use the `Bandit` automated code review tool to scan the entire `homeassistant` repository to see what the results and based on the results we would de-scope non-applicable files/folder. We also decided collectively as a group to inspect some of the .py files that were directly related to the software assurance cases and mis-use/use-cases we looked at over the course of the semester. We were particularly concerned with the `auth`, `util`, and `components` folders since after a quick manual review it was noted that these were most related to the work we have been doing over the course of the semester.

## Manual Code Review

<TODO> Insert Findings from manual code review of critical security functions identified in misuse cases, assurance cases, and threat models.

## Automated Tool Findings

### Bandit

#### Overview

[Bandit](https://pypi.org/project/bandit) is a Python based tool designed to find common security issues in Python code. To do this it will process each file, build an AST from it, and run appropriate plugins against the AST nodes. Once bandit is done scanning the files it will generate a .csv report.

<TODO> Insert metrics of findings (i.e. code scaned/metrics)
#### Key Findings

<TODO> Insert Key Findings from automated code scanning (if available). Include links to full reports. (Also check for CWEs)

## Summary of Key Findings

<TODO> Insert summary of key findings from manual and/or automated scanning. This summary should include mappings to CWEs to describe categories of major findings.

## Contributions to Open-Source Project
<NOTE>If applicable
<TODO> Planned or ongoing contributions to the upstream open-source project (documentation, design changes, code changes, communications, etc.) These can be based on any of the prior assignments in the class.

## Team Reflection

<TODO> Insert Reflection

## Github Project Board
[GitHub Repository](https://github.com/Chrs987/HomeAssistant/projects/7)
