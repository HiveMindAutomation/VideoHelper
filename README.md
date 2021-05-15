# VideoHelper

Python Script to help YouTubers quickly create Folder Structures and Script Outlines for Video projects with Templated Intro's and Outtro's in MS Word.

Featuring Atlassian JIRA integration

## Table of Contents
- [VideoHelper](#videohelper)
  - [Table of Contents](#table-of-contents)
  - [Video Walkthrough of this Project available on YouTube](#video-walkthrough-of-this-project-available-on-youtube)
  - [Requirements](#requirements)
    - [Required for creating DOCX files](#required-for-creating-docx-files)
    - [Optional - `imports` can be commented out if not utilising JIRA integration](#optional---imports-can-be-commented-out-if-not-utilising-jira-integration)
  - [Usage](#usage)
    - [Fill out `auth_template.py`](#fill-out-auth_templatepy)
    - [Update `rootPath` variable](#update-rootpath-variable)
    - [Update path conditional logic for your use case](#update-path-conditional-logic-for-your-use-case)
    - [if not using JIRA integration](#if-not-using-jira-integration)
  - [Run the script](#run-the-script)

> [!IMPORTANT]
> Only tested in Python 3.8.2 and Python 3.9.4 on macOS
> OS functions may require modification in Linux or Windows

## Video Walkthrough of this Project available on YouTube


## Requirements

### Required for creating DOCX files  
[Python DOCX Library] (https://python-docx.readthedocs.io/en/latest/)  
Can be installed using:  
`pip3 install python-docx`  

### Optional - `imports` can be commented out if not utilising JIRA integration

[Python Requests Library](https://pypi.org/project/requests/)  
Can be installed by running:  
`pip3 install requests`

[Python JSON Library](https://docs.python.org/3/library/json.html)  
Can be installed by running:  
`pip3 install json`

## Usage

### Fill out `auth_template.py`
Inside `auth_template.py` are important variables
You COULD explicitly define these within `generate.py`, however, I feel like it's better to define them externally for..... security, especially if you commit anything to GitHub.  
The only potentially sensitive detail in here is the `headers` for JIRA.  
These are required for Authentication. I plan to fix this authentication in a future release, but for now it works. I got my Authentication headers by using Postman to explore the JIRA API and copied the Authentication headers from there.

Once you've filled out auth_template.py, save the file as auth.py in the same folder.

### Update `rootPath` variable

You'll need to change this path based on YOUR configuration. Mine points to a mounted SMB share which is on my Server. You might just want to point this to Local Storage
```python
rootPath = "/Volumes/HiveMind/Videos"
```
### Update path conditional logic for your use case

The conditionals from Line 74 suit my use cases, however, you should update this to suit your own use case.
For Example, changing `Getting Started Series` to `Tutorials` or however you want to structure your folders.

```python
# Set Path based on inputs
if projectType == 1:
    path = f"{rootPath}/Getting Started Series/{project}-{projectID} - {jobTitle}"
elif projectType == 2:
    path = f"{rootPath}/Product Reviews/{project}-{projectID} - {jobTitle}"
elif projectType == 3:
    path = f"{rootPath}/Quick Tips/{project}-{projectID} - {jobTitle}"
elif projectType == 4:
    path = f"{rootPath}/Code Review/{project}-{projectID} - {jobTitle}"
else:
    projectType = int(input(typePrompt))
```

### if not using JIRA integration
If you aren't using the JIRA integration, modify the "JIRA" variable on Line 15 to 
```python
JIRA = False
```
## Run the script
Run the script by opening a Terminal in the same location as the generate.py script and running `python3 ./generate.py`.

