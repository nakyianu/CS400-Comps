# Development Plan

#### Group Members: Aadi Akyianu, Essy Ingram, Lazuli Kleinhans

## Project Description
We plan to implement a version of LinPEAS that scans for vulnerabilities and takes advantage of those vulnerabilities to escalate its privileges.


## Learning Goals
###### What do you want to end up understanding that you don't understand yet?
* Building a coding architecture that allows us to add or remove vulnerabilities easily.
* How to add vulnerabilities to a machine (for the purposes of understanding what not to do to secure a machine)
* Learn how to categorize different vulnerabilities.


## Development Goals 
###### What features do you want your software to have by the end of the project?
* Run a vulnerability scan on a machine
* Implement code to attack a vulnerability
* Implement more vulnerabilities 
* Add users with multiple groups and try to run horizontal and vertical privilege escalation (stretch goal)
* Create a backdoor for an external user (stretch goal)


## Testing and Benchmarking our Tool
* Use a vulnerable machine to practice
* Start from non-priveleged users and try to gain root access
* Create unit tests for each module

## Rough Development Schedule
###### What steps will you take, and what will be your deadlines? 
* Decide between using a virtual machine or a local machine (week 2)
* Read through LinPEAS source code to get an idea of how vulnerability scanning works (week 3)
* Modularize code and develop overarching code structure (week 4)
* Create a vulnerability in the machine (week 5)
* Develop code to scan for that vulnerability (week 5)
* Implement code to exploit that vulnerability (week 6)
* Add another vulnerabilities to the machine (week 7)
* Develop code to scan for and exploit that new vulnerability (week 7)
* Develop other scans and exploitations (week 9)

#### Link to repo
https://github.com/nakyianu/linPEVES 
