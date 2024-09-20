### Level 0:
- ssh bandit0@bandit.labs.overthewire.org -p 2220
- basically understanding how ssh works

### Level 0 -> Level 1:
- open the readme to get password
- ssh into bandit1 using that password
- bandit1 password: ZjLjTmM6FvvyRnrb2rfNWOZOTa6ip5If

### Level 1 -> Level 2:
- "cat < -" to open a dashed filename
- teaches you about stdin redirection
- bandit2 password: 263JGJPfgU6LtdEvgfWU1XP5yac29mFx

### Level 2 -> Level 3:
- "\ " for spaces in filenames
- command: cat spaces\ in\ this\ filename
- or... use tab to complete and it adds the \ for you 
- bandit3 password: MNk8KNH3Usiio41PRUEoDFPqfxLPlSmx

### Level 3 -> Level 4:
- ls -a: find hidden files
- -a: all files
- bandit4 password: 2WmrDFRmJIq3IPxneAaMGhap0pFhF3NJ

### Level 4 -> Level 5:
- they definitely want you to use file here but I found that grep also works
   - grep -v -R * inhere/:
   - -R: recursively searches the files in the inhere/ directory
   - -v: should only print lines that don't match but it seems to be working differently in this case
   - basically it prints the contents of inhere/-file07 which has the password.
   - why it works, I'm still not completely sure
- otherwise:
   - cd inhere
   - file ./* : searches all the files in the directory and returns info about them (e.g. whether they are binary files or not) 
- file is located: inhere/-file07
- bandit5 password: 4oQYVPkxZOOEOO5pTW81FB8j8lxXGUQw

### Level 5 -> Level 6:
- find -size 1033c ! -executable | xargs grep -L ?: gives you the directory where the password is hidden
- find -size 1033c ! -executable: it finds a file that is exactly 1033 bytes and is not executable. 
- xargs grep -L ?: takes the files from find and inputs them into grep then -L finds the files that don't match.
- bandit6 password: HWasnPhtq9AVKe0dmk45nxy20cvUa6EG

### Level 6 -> Level 7:
- find -size 33c -user bandit7 -group bandit6 -readable | xargs  ls -als: only one file has permission and that's ./var/lib/dpkg/info/bandit7.password
- bandit7 password: morbNTDkSW6jIlUc0ymOdMaLnOlFVAaj

### Level 7 -> Level 8:
- grep millionth data.txt
- bandit8 password: dfwvzFQi4mU0wfNbFOe9RoWskMLg7eEc

### Level 8 -> Level 9:
- sort data.txt | uniq -u: sorts the text which makes it easier to find duplicate lines
- bandit9 password: 4CKMh1JI91bUIZZPXDqGanal4xvAg0JM

### Level 9 -> Level 10:
- strings -e s data.txt | grep ^"=": prints the strings that use ascii characters and are preceded by an equal sign. Adding a \+ in the "" would mean the equal sign shows up 1 or more times.
- bandit10 password: FGUW5ilLVJrxX9kMYMmlN4MgbpfMiqey

### Level 10 -> Level 11:
- base64 -d data.txt: decodes the base64 data in the file into UTF-8
- bandit11 password: dtR173fZKb0RRsDFSGsg2RWnpNVj3qRr

### Level 11 -> Level 12:
- cat data.txt | tr 'NOPQRSTUVWXYZABCDEFGHIJKLMnopqrstuvwxyzabcdefghijklm' 'ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz' : replaces the letters and unscrambles the ROT13 code
- bandit12 password: 7x16WNeHIi5YkIhWsfFIqoognUTyj9Q4

### Level 12 -> Level 13:
- /tmp/tmp.xWGm5cxfjv
- copy the data file over into a temporary directory
	- cd /tmp
	- mktemp -d : makes a temporary directory with a random name
- reverse the hexdump so that you can determine what kind of zip it was
	- xxd -r [filename] > [output file]: reverse hex and output to file
	- file [output file]: to figure out what type of zip
- change the extension and unzip
- use file to check what new compression has been applied
- repeat the last two steps until file outputs ASCII
- bandit13 password: FO5dwFsc0cbaIiH0h8J2eUks2vdTDwAn


### Level 13 -> 14:
- ssh -i ~/sshkey.private bandit14@bandit.labs.overthewire.org: setup an ssh connecion using the key stored in sshkey.private to make the connection
- bandit14 password: MU4VWeTyJk8ROof1qqmcBPaLh7lDCPvS

### Level 14 -> Level 15:
- telnet localhost 30000: opens up a connection to port 30000 on localhost
- send the password for the current level (level 14) through
- server responds with the password for level 15
- bandit15 password: 8xCjnmgoKbGLhHFAZlGE5Tmu4M2tKJQo

### Level 15 -> Level 16:
- openssl s\_client [host]:[port]: opens up a TLS/SSL connection to the specified host and port. You can then send messages to that port and it encrypts them for you with SSL/TLS.
- bandit16 password: kSkvUpMQ7lBYyCM4GBPvCvT1BfWRy0Dx

### Level 16 -> Level 17:
- first scan the ports using nmap -sV -p 31000-32000 to find the active port: 31790 in this case
- then run openssl s\_client -ign\_eof localhost:[port] to open up an SSL/TLS connection
- put in the password for the previous level: 
- you should get a private key in response.
- put the key in /tmp/sshkey.private
- then ssh -i /tmp/sshey.private -p 2220 
- now you have access to bandit17
- bandit17 password: EReVavePLFHtFlFsjn3hyzMlvSuSAcRD
   - located in /etc/bandit\_pass/bandit17

### Level 17 -> Level 18
- use diff to find the line that differs between passwords.old and passwords.new
- diff passwords.old passwords.new
   - <: lines in file 1 (passwords.old)
   - >: lines in file 2 (passwords.new)
   - the password is the line associated with passwords.new
- bandit18 password: x2gLTTjFwMOhQ8oWNbMN362QKxfRqGl

### Level 18 -> Level 19
- ssh is blocked by .bashrc but scp isn't ;)
- scp -P 2220 bandit18@bandit.labs.overthewire.org:/home/bandit18/readme [destination]
- bandit19 password: cGWpMaKXVwDUNgPAVJbWYuGHVn9zl3j

### Level 19 -> Level 20
- euid: effective uid
   - this is the user id you are currently running as
- run ~/bandit20-do cat /etc/bandit\_pass/bandit20
   - because you are "effectively" running as bandit20, you can read it to get the password
-bandit20 password: 0qXahG8ZjOVMN9Ghs7iOWsCfZyXOUbYO

### Level 20 -> Level 21
- confused by how to start so I looked up how to get started: https://mayadevbe.me/posts/overthewire/bandit/level21/
- basically suconnect works by connecting to a port that you specify and then compares whatever it finds at the port to the bandit 20 password, if it mathces it'll send back the password for bandit21. 
- in order to have text at a port that it can compare with you need to use nc
- first: echo [bandit20 password] | nc -l -p [random port] & 
    - the & is to background the process
    - echo "0qXahG8ZjOVMN9Ghs7iOWsCfZyXOUbYO" | nc -l -p 57628 &
- next: ./suconnect [random port]
    - ./suconnect 57628
- bandit21 password: EeoULMCra2q0dSkYj561DX7s1CpBuOBt

### Level 21 -> Level 22
- very confused about how to do this one at first. Had to look it up: https://mayadevbe.me/posts/overthewire/bandit/level22/ 
- cd /etc/cron.d: this is where the cron jobs are located
- look in cronjob\_bandit22: this shows you the commands being run by cron
    - cat cronjob\_bandit22
- the command that's run regularly (every minute each day) is /usr/bin/cronjob\_22.sh
- if you look inside that file you notice that /etc/bandit\_pass/bandit22 cats its password to a tmp file
- next just read that tmp file to find the password
    cat /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
- bandit22 password: tRae0UfB9v0UzbCdn9cY0gQnds9GF58Q

### Level 22 -> Level 23
- similar kind of deal:
- cat /etc/cron.d/cronjob\_bandit23: in this case i went straight to the next step becaause i assumed the command was the same and it was
- cat /usr/bin/cronjob\_bandit23.sh
- you'll notice that it's creating a hash of the phrase "I am user bandit23" and using that as the tmp file
    - don't do bandit22 (even though you see the whoami command) because you're trying to get bandit23's password
- and of course it's echoing the password into that tmp file so
- cat /tmp/8ca319486bfbbc3663ea0fbe81326349
- bandit23 password: 0Zf11ioIjMVN551jX3CmStKLYqjk54Ga

### Level 23 -> Level 24
- another one I had to look up after writing about 15 scripts that weren't getting me anywhere. turns out i jsut needed a temporary folder 
- similar kind of deal:
- cat /etc/cron.d/cronjob\_bandit24: in this case i went straight to the next step becaause i assumed the command was the same and it was
- cat /usr/bin/cronjob\_bandit24.sh
- ok so for this one we have to make a script that allows us to retrieve the password
- basically cronjob\_bandit24.sh loops through all the files in /var/spool/bandit24/foo. if they are owned by bandit23 it runs them with a timeout.
    - timeout -s 9 60: timeout for 60 seconds then kill with 9 as signal (kill -9)
- now how to get it to print the password you ask..
    - tried several versions and I had the right idea but I was creating the files in the wrong place. I should have been working in a temporary directory to create both the script and the file to store the password. 
    - I think my file was being deleted before it got to run or was run before i was done and then deleted after
- anyway, the following steps worked so far:
    - mktemp -d
    - cd [temp dir]
    - vi password
    - vi get\_pass.sh
         #! /bin/bash
         cat /etc/bandit\_pass/bandit24 > /tmp/[tmp dir]/password
        - very simple script 
    - chmod 777 /tmp/[tmp dir]
    - chmod 777 /tmp/[tmp dir]/*
    - cp get\_pass.sh /var/spool/bandit24/foo
    - vi password (after about a minute)
- bandit24 password: gb8KRRCsshuZXI0tUuR6ypOFjiZbf3G8

### Level 24 -> Level 25
- this one requires us to brute force a secret code to a daemon listening on port 30002
- at first i tried to run nc in a script and then feed in the responds then but i didn't account for the fact that it would wait for nc to run before running the for loop
- making a file with all the possibilities you want to try first and then catting that into nc is the way to go
- mktemp -d
- cd [temp dir]
- vi guess.sh
    #! /bin/bash
    for i in {0000..9999}; do
        echo gb8KRRCsshuZXI0tUuR6ypOFjiZbf3G8 $i
    done
- chmod 700 guess.sh
- ./guess.sh > possibilities.txt
- cat possibilities.txt | nc localhost 30002 > results.txt
- cat results.txt | grep -v Wrong!: finds the code by filtering out all the wrong
- bandit25 password: iCi86ttT4KSNe1armKiwbQNmB3YJP3q4
- pin was 9297 (apparently)
