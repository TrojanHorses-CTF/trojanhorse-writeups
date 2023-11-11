# CTF Cheat Sheet

# cat
### Description:
Print to the terminal the contents of a file.

### Usage:
$ cat filename

### Example:
$ cat flag.txt

# cd
### Description:
Change directories

### Usage:
$ cd directory

### Examples:
* $ cd Documents
* $ cd ..
    * Go up/back a directory
* $ cd /
    * Go to root directory
* $ cd
    * Go to home directory
    * Same as $ cd ~

# chmod
### Description:
Change permissions on a file or directory.

### Usage:
$ chmod +/- permission

Note: Using `+` grants the permission and using `-` removes the permission

Possible permissions:
* Readable: r
    * If used on directory, this determines whether or not you can `ls` the directory contents
* Writeable: w
    * If used on directory, this determines whether or not you can create/delete files in the directory
* Executable: x 
    * If used on directory, this determines whether or not you can `cd` the directory contents

### Examples:
* $ chmod +r flag.txt
* $ chmod -w myfile.txt
* $ chmod +x script.py
* $ chmod -r flag_directory
* $ chmod +w flag_directory
* $ chmod -x flag_directory

# echo
### Description:
Prints specified string to terminal

### Usage:
* $ echo string
    * Most common usage
* $ echo "\$(<filename)"
    * Used to print file contents to terminal

### Examples:
* $ echo hello
    * Prints hello in terminal
* $ echo "\$(<flag.txt)"
    * Prints contents of flag.txt to terminal like if you used `cat`

# file
### Description:
Prints information about the file type to the terminal.

### Usage:
$ file filename

### Examples:
$ file instructions.txt

# find
### Description:
Search for filename that is or includes the specified string.

### Usage:
$ find . -type d/f -name "\*string*"

### Examples:
* $ find . -type f -name "\*flag*"
* $ find . -type d -name "\*flag_dir*"

# grep
### Description:
Search inside files to find specified string

### Usage:
* $ grep string filename

* $ grep -r string
    * *Most Common* --- Used if you want to search in more than one file

### Examples:
* $ grep pico flag.txt
* $ grep -r pico

# head
### Description:
Prints the first 10 lines of a file (or command output if used with `pipe`)

### Usage:
* $ head filename
* $ command | head

### Examples:
* $ head script.py
* $ ls -l | head

# ls
### Description:
Print to the terminal what's in a directory

### Usage:
$ ls

### Helpful Options
* $ ls -l
    * Lists more details about files and directories
* $ ls -a
    * Lists hidden files and directories

### Examples:
* $ ls
* $ ls Documents
    * lists contents of specified directory

# man
### Description:
Open the documentation for a terminal command

### Usage:
$ man commandname

### Examples:
$ man ls

# md5sum
### Description:
Prints to the terminal the md5 hash of the file. This can be used to verify a file's integrity i.e. to make sure it wasn't changed when you download/receive it from someone.

### Usage:
$ md5sum filename

### Examples:
$ md5sum index.html

# nc
### Description:
Run a program that's stored in "the cloud" at the specified url and port number. 

The url is like telling the mailman which neighborhood to go to. The port is like telling the mailman which mailbox to go to.

### Usage:
$ nc url portnumber

### Examples:
$ nc mercury.picoctf.net 22342

# python3
### Description:
Runs a python file or spawns a python shell

### Usage
* $ python3 pythonfilename
* $ python3
    * This spawns a python shell where you can type and run one line of code at a time. 
        * This is useful if you just need to run something short like `print(ord('c') + ord('b'))`.

### Examples
$ python3 script.py

# sudo
### Description:
Run the specified command as the root user (user with unlimited permissions)

### Usage:
$ sudo command

### Examples:
* $ sudo vim flag.txt
* $ sudo ls
* $ sudo -l
    * This lists the commands the user is allowed to run with sudo

# ssh
### Description:
Open a new terminal containing a filesystem (e.g. files and directories) stored in "the cloud". This filesystem is totally separate from the filesystem on your computer.

### Usage:
$ ssh username@url -p portnumber

### Examples:
$ ssh ctf-player@venus.picoctf.net -p 49597

### Note:
You will probably be prompted with a question asking `Are you sure you want to continue connecting?` Type `yes`. You will then most likely be prompted to enter a password which is usually given to you in the CTF challenge description. When you paste the password into the ssh terminal prompt, you won't see anything change/appear in the prompt; just press enter after clicking paste and the password will go through.

# vim
### Description:
* Open/Create/Edit/Search a file
* `vi` is a different commaned that does the same thing as `vim`

### Usage: 
$ vim filename

### Example:
$ vim flag.txt

### Commands within vim:
* i - Enter INSERT mode to be able to edit file
* ESC - Exit INSERT mode and enter COMMAND mode to be able to run below commands
* / - search file for string (example usage: /pico)
* :w - save file
* :q - exit out of file
* dd - delete entire line that cursor is on
    * dXd - delete X number of lines beginning with the line the cursor is on and moving downwards
        * Example that deletes 50 lines: d50d
* u - undo previous change
* :sh OR :!/bin/bash - both of these spawn a bash shell with the permission of the user who ran vim to open the file
    * If you use `sudo vim` to open the file and run one of these commands, you spawn a root shell! This is a shell with unlimited permissions of the entire filesystem!

# Misc Commands
* This enables you to run commands when the terminal won't let you (for some reason related to the challenge) run them normally
    * ${parameter=command}
        * ${parameter=ls}
        * ${parameter=cat flag.txt}
    * /bin/ls
        * Type full path of the command
* compgen -c
    * List all bash commands that are available for the user to run
        * Pressing tab twice does the same thing
* type echo, DON'T PRESS ENTER, then press tab twice and it lists the contents of the current directory
* ^c
    * Press `c` while holding the `control` key down (ctrl-c)
    * Quit out of most programs when they're running. It kills the progam/terminal command that's currently executing.

# `|` aka pipe
### Description:
* This isn't a command
* It passes the output of the first command as the input to the second command

### Usage:
$ command1 | command2

### Examples:
* $ ls | grep "Do"
* $ cat names.txt | sort
* $ cat names.txt | sort | unique

# Firefox
### Web exploitation tips:
* `html`: Right-click the page and click `View Page Source`
* `js`: Right-click the page, click `Inspect`, click the `Debugger` tab, then click around in the drop-down folders on the left to find `.js` files
* `css`: Right-click the page, click `Inspect`, then click `Style Editor`.
* `cookies`: Right-click the page, click `Inspect`, click the `Storage` tab, click the `Cookies` drop-down on the lefte
* Sometimes challenges will hide the flag or clues in the `robots.txt` file
    * Usage - add `robots.txt` to the end of the url: `https://jupiter.challenges.picoctf.org/problem/56830/robots.txt`
* `.htacess` file manages Apache server permissions
* In Macs, a `.DS_Store` file stores the configurations for how the desktop looks (eg. icon location, etc.)
* `wget`
    * This downloads the html page of the specified url
    * Usage: $ wget url
    * Examples:
        * $ wget https://login.mars.picoctf.net/
        * $ wget http://mercury.picoctf.net:52362/ --header="User-Agent: PicoBrowser" --header="Referer: http://mercury.picoctf.net:52362/" --header="Date: Wed, 21 Oct 2018 07:28:00 GMT" --header="DNT: 1" --header="X-Forwarded-For: 31.3.152.55" --header="Accept-Language: sv,en;q=0.9"
* `curl`
    * This downloads the html page of the specified url
        * Usage: $ curl url
        * Examples:
            * $ curl https://login.mars.picoctf.net/
            * $ curl --user mother:ovomorph -A "MU-TH-UR 6000" https://spooky-aliens-make-me-wanna-curl-web.chals.io/flag
                * This features username and password authentication as well as changing the User-Agent header to MU-TH-UR 6000
* `Postman`
    * https://web.postman.co/
    * This is super helpful for creating custom requests
* XML is is just information wrapped in tags. XML was designed to carry data with focus on what data is. HTML was designed to display data with focus on how data looks.
    * XXE
        * XML external entity injection
        * It's a web security vulnerability that allows an attacker to interfere with an application's processing of XML data. It often allows an attacker to view files on the application server filesystem, and to interact with any back-end or external systems that the application itself can access.
        * Checkout this link for more info: https://portswigger.net/web-security/xxe
* Watch the search bar as you navigate to and within a website, looking for any redirections happening.
    * Or use wireshark to do this. Maybe follow http(s) stream.
* `phps` files are php source files; check for the `index.phps` file by adding it to the end of the url: http://mercury.picoctf.net:14804/index.phps

# regex
This isn't a terminal command. It's a sequence of characters that forms a search pattern. Check out this link for symbols and their examples: https://www.hallme.com/blog/the-power-of-regular-expressions/

# Data Converter
* https://www.rapidtables.com/convert/number/ascii-hex-bin-dec-converter.html
    * For some reason, some converters online just don't work!

# JSON Beautifier
* https://codebeautify.org/jsonviewer
    * Pass messy JSON (ex. JSON that's crammed onto one line) into this web tool, and it will add perfect spacing to it, making it much more readable.

# Base64 File Decoder
* https://www.base64decode.org/
    * You can drag and drop an entire Base64 encoded file into this web tool, and it will return the decoded file.

# ASCII Table
* https://coding.tools/ascii-table

# OSINT
* It stands for open source intelligence. It's the gathering of information from publicly available sources, such as social media, company websites, and news articles. There is a great deal of information that can be gathered about a company or person through open source intelligence.

# PWN
Binary exploitation challenges (pronounced "pone" I think)

# NOT YET TAUGHT/EXPLORED
* ROT13
* exiftool
    * https://www.geeksforgeeks.org/installing-and-using-exiftool-on-linux/
* Reverse Engineering Tips
    * Separate operations into their own line of code, assigning them to a variable
        *  Start in the inmost parenthesis and work your way out
    * ...
* teach them to view page source and click on linked files like .js and .php

# 
### Description:

### Usage:

### Examples: