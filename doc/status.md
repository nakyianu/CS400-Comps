## Monday, October 14

### What’s Already Working

* Created three working vulnerability scans  
  * The first scan, “cron-scan.sh,” checks to see if there are writable cron jobs run by root on the system. In our case, these scans are functional on our personal systems.
  * Our next scan, path-scan.sh, checks if there are any writable directories in the PATH variable. If there are, it adds them to a list called writable-dirs for later exploitation.  
  * Our final scan, pkexec-scan.sh, scans for the pkexec binary on a machine. If it finds it, it checks if the current user has sudo access. If so it sets the PKEXEC flag to 1 to notify the program that it can use pkexec for further exploits.  
* A “main.sh” file that runs each scan successfully.  
* Created an Ubuntu VM on AWS where the scans live and have run successfully.  
* Added the user to sudoers to the sudoers group as part of the crontab exploit.

### What We’re Working on Now

* Deciding on a goal for our exploits that each scan/exploit brings us closer to achieving.  
  * For instance, pkexec works best with a specific exploit in mind.

### Other Thoughts

* We could abandon pkexec, or just have the scan exist without an exploit.  
  * It requires having two terminal sessions active which might be a challenge.  
  * We’re looking it creating a child process that runs concurrently with the parent

