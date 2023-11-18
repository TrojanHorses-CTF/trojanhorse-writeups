# CTF Cheat Sheet

# cat
### Description:
Print to the terminal the contents of a file.

### Usage:
`$ cat filename`

### Example:
$ cat flag.txt

# cd
### Description:
Change directories

### Usage:
`$ cd directory`

### Examples:
* $ cd Documents
* $ cd ..
    * Go up/back a directory
    * `..` means the parent directory i.e. the directory one level up in the file tree.
* $ cd /
    * Go to root directory
    * `/` means root
* $ cd
    * Go to home directory
    * Same as $ cd ~
        * `~` means home

# chmod
### Description:
Change permissions on a file or directory.

### Usage:
`$ chmod +/- permission`

Note: Using `+` grants the permission and using `-` removes the permission

Possible permissions:
* Readable: `r`
    * If used on directory, this determines whether or not you can `ls` the directory contents
* Writeable: `w`
    * If used on directory, this determines whether or not you can create/delete files in the directory
* Executable: `x`
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
* `$ echo string`
    * Most common usage
* `$ echo "$(<filename)"`
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
`$ file filename`

### Examples:
$ file instructions.txt

# find
### Description:
Search for filename that is or includes the specified string.

### Usage:
`$ find . -type d/f -name "\*string*"`

### Examples:
* $ find . -type f -name "\*flag*"
* $ find . -type d -name "\*flag_dir*"

# grep
### Description:
Search inside files to find specified string

### Usage:
* `$ grep string filename`
* `$ grep -r string`
    * *Most Common* --- Used if you want to search in more than one file

### Examples:
* $ grep pico flag.txt
* $ grep -r pico

# head
### Description:
Prints the first 10 lines of a file (or command output if used with `pipe`)

### Usage:
* `$ head filename`
* `$ command | head`

### Examples:
* $ head script.py
* $ ls -l | head

# ls
### Description:
Print to the terminal what's in a directory

### Usage:
`$ ls`

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
`$ man commandname`

### Examples:
$ man ls

# md5sum
### Description:
Prints to the terminal the md5 hash of the file. This can be used to verify a file's integrity i.e. to make sure it wasn't changed when you download/receive it from someone.

### Usage:
`$ md5sum filename`

### Examples:
$ md5sum index.html

# nc
### Description:
Run a program that's stored in "the cloud" at the specified url and port number. 

The url is like telling the mailman which neighborhood to go to. The port is like telling the mailman which mailbox to go to.

### Usage:
`$ nc url portnumber`

### Examples:
$ nc mercury.picoctf.net 22342

# python3
### Description:
Runs a python file or spawns a python shell

### Usage
* `$ python3 pythonfilename`
* `$ python3`
    * This spawns a python shell where you can type and run one line of code at a time. 
        * This is useful if you just need to run something short like `print(ord('c') + ord('b'))`.

### Examples
$ python3 script.py

# sudo
### Description:
Run the specified command as the root user (user with unlimited permissions)

### Usage:
`$ sudo command`

### Examples:
* $ sudo vim flag.txt
* $ sudo ls
* $ sudo -l
    * This lists the commands the user is allowed to run with sudo

# ssh
### Description:
Open a new terminal containing a filesystem (e.g. files and directories) stored in "the cloud". This filesystem is totally separate from the filesystem on your computer.

### Usage:
`$ ssh username@url -p portnumber`

### Examples:
$ ssh ctf-player@venus.picoctf.net -p 49597

### Note:
You will probably be prompted with a question asking `Are you sure you want to continue connecting?` Type `yes`. You will then most likely be prompted to enter a password which is usually given to you in the CTF challenge description. When you paste the password into the ssh terminal prompt, you won't see anything change/appear in the prompt; just press enter after clicking paste and the password will go through.

# vim
### Description:
* Open/Create/Edit/Search a file
* `vi` is a different commaned that does the same thing as `vim`

### Usage: 
`$ vim filename`

### Example:
$ vim flag.txt

### Commands within vim:
* i - Enter INSERT mode to be able to edit file
* ESC - Exit INSERT mode and enter COMMAND mode to be able to run below commands
* / - search file for string (example usage: `/pico`)
* :w - save file
* :q - exit out of file
* dd - delete entire line that cursor is on
    * dXd - delete X number of lines beginning with the line the cursor is on and moving downwards
        * Example that deletes 50 lines: d50d
* u - undo previous change
* :sh OR :!/bin/bash - both of these spawn a bash shell with the permission of the user who ran vim to open the file
    * If you use `sudo vim` to open the file and run one of these commands, you spawn a root shell! This is a shell with unlimited permissions of the entire filesystem!

# Firefox
### Web Exploitation Tips:
* `html`: Right-click the page and click `View Page Source`
* `js`: Right-click the page, click `Inspect`, click the `Debugger` tab, then click around in the drop-down folders on the left to find `.js` files
* `css`: Right-click the page, click `Inspect`, then click `Style Editor`.
* `cookies`: Right-click the page, click `Inspect`, click the `Storage` tab, click the `Cookies` drop-down on the lefte
* Sometimes challenges will hide the flag or clues in the `robots.txt` file
    * Usage - add `robots.txt` to the end of the url: `https://jupiter.challenges.picoctf.org/problem/56830/robots.txt`
* Access a file by appending it to the url: http://mercury.picoctf.net:52362/flag.txt
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
    * Note: don't include the `s` at the end of `phps` when running a command like `curl` on a file like `authentication.phps`
        * Example of how TO do it: `$ curl http://mercury.picoctf.net:14804/authentication.php`

* PHP Sandbox
    * https://onlinephp.io/
    * Allows you to run (and therefore test) PHP code
* `flask-unsign`
    * Description: Command line tool to fetch, decode, brute-force and craft session cookies of a Flask application by guessing secret keys.
    * How to Install: `pip3 install flask-unsign`
    * Usage (see `Most Cookies` on picoGym and the [solution](https://github.com/vivian-dai/PicoCTF2021-Writeup/blob/main/Web%20Exploitation/Most%20Cookies/MostCookies.md) for better understanding):
        * `$ flask-unsign --decode --cookie 'eyJ2ZXJ5X2F1dGgiOiJibGFuayJ9.ZVeyiQ.bWA_2WeiTOts0OWM7Z0qaDhrFqs'`
            * This decodes the cookie and prints it in the session cookie structure
        * `$ flask-unsign --unsign --server 'http://mercury.picoctf.net:65344/' --wordlist wordlist.txt`
            * This gets the secret key
            * The `--server` value is the url of the web site/server
            * The `--wordlist` value contains a new line separated list of the possible cookie values for the website(?) (the possible values could be found in a "server.py" script)
* Encoding flask session cookies
    * Use [this](https://github.com/noraj/flask-session-cookie-manager) tool
    * Usage:
        * `$ git clone https://github.com/noraj/flask-session-cookie-manager.git && cd flask-session-cookie-manager`
            * This installs the tool
        * `$ python -m venv venv`
            * This creates the virtual environment
        * `$ source venv/bin/activate`
            * This makes your terminal enter the virtual environment
        * `$ python setup.py install`
            * This setups the virutal environment(?)
        * `$ flask_session_cookie_manager3.py encode -s 'peanut butter' -t "{'very_auth':'admin'}"`
            * `-s` is the secret key found with `flask-unsign`
            * `-t` is your custom cookie in its session cookie structure
* Accessing errors on web server: (this could be wrong/unhelpful in some way)
    * Errors are stored in files on web servers and can be accessed via the url + ?error= + filename_without_extension
        * e.g. https://notepad.mars.picoctf.net/?error=bad_content will return bad_content.html

# SQL/psql/sqlite3 
### Description:
Usually used for sql injection in web exploitation challenges

### Helpful Syntax:
* Basic SQL syntax:
    * To print the contents of a table in the database:
        * `SELECT` specifies the columns to print
            * `*` will return ALL columns from the table
        * `FROM` specifies the table in the database
        * `WHERE` specifies a condition (like an if-statement) to determine which rows of the specified column(s) are printed
        * Example: `SELECT name FROM users WHERE home='Indiana'` will return the `names` of all people in the `users` table whose `home` is `Indiana`.
    * When SELECTing from a table, you can specify `null`, integers (e.g. `1`), and/or strings (e.g. "hi"). The query will return a column with nothing in it, the integer you specified, and/or the string you specified respectively.
        * Example: `SELECT name, null, 1, "hi" FROM users` would return `| Joshua |   | 1 | hi |`
* `--` or `/*`
    * This creates a comment in the query meaning whatever follows it is ignored
    * Example: 
        * `SELECT * FROM 'user_input_table' WHERE name != "flag"`
        * Input `table'--` or `table'/*`
            * Closes quotes for 'user_input_table'
            * Changes query to either of these respectively:
                * `SELECT * FROM 'table'--' WHERE name != "flag"`
                * `SELECT * FROM 'table'/*' WHERE name != "flag"`
            * Ignores the `WHERE` that prevents flag from being printed
* "Force True"
    * This is one way to get around the password field.
    * Example:
        * The password field could initiate a query like `SELECT admin FROM users WHERE password='<userinput>'` where \<userinput> is the password you submit. This only lets you login if the `WHERE` clause is `TRUE` i.e. you enter the correct password.
        * You could force this password condition to resolve to `TRUE` with the `or` operator and some logic like `1=1` or `a’IS NOT’b`.
        * Type `' or 1=1` into the password field to close the set of quotes the query expects. Add your `or` condition which will always resolve to `TRUE`.
        * This results in the following query which now has a `WHERE` clause that always resolves to `TRUE`: `SELECT admin FROM users WHERE password='' or 1=1` 
* `;`
    * This ends the current query, allowing you to start a new one
    * Example: 
        * Original url: `http://mercury.picoctf.net:65344/items.php?id=2`
            * Which results in `SELECT * FROM items WHERE ID = 2`
        * Add `; SELECT * from flag_table` to url
        * Resulting url: `http://mercury.picoctf.net:65344/items.php?id=2; SELECT * from flag_table`
            * Which results in `SELECT * FROM items WHERE ID = 2; SELECT * from flag_table`
            * Where `flag_table` contains a row with the flag
* `||`
    * This concatenates strings i.e. joins to strings together
    * Example:
        * Let's say you need to login as admin on a webpage. The problem is that you aren't allowed to enter "admin" as your username. You could enter `adm'||'in`. This will join `adm` and `in` together to result in `admin` while allowing you to get around the aforementioned "admin" username rule.
* `UNION`
    * Combines the results of two or more queries
    * Could use this to add a query of your own onto a preexisting query (like `;`)
        * Example:
            * Type the following into an input field on a webpage: `' union select name, sql, 1 from sqlite_master;`
* psql
    * When connected to a psql shell:
        * `\l` lists the databases
        * `\c databasename` connects to the specified database
        * `\dt` lists the tables in the database
        * You can also run queries: `select * from tablename;`
            * The query isn't caps sensitive, but you must end query with a semicolon.
* sqlite3
    * If you don't know what tables are present in a database, you can query the `sqlite_schema` table which is ALWAYS present.
        * Alternatives names for this table are: `sqlite_master`, `sqlite_temp_schema`, and ` sqlite_temp_master`.
        * It's columns are `type`, `name`, `tbl_name`, `rootpage`, and `sql`.

# Misc
* This enables you to run commands when the terminal won't let you (for some reason related to the challenge) run them normally
    * `$ ${parameter=command}`
        * `$ ${parameter=ls}`
        * `$ ${parameter=cat flag.txt}`
    * `$ /bin/ls`
        * Type full path of the command
* `$ compgen -c`
    * List all bash commands that are available for the user to run
        * Pressing tab twice does the same thing
* Type `echo`, DON'T PRESS ENTER, then press tab twice and it lists the contents of the current directory.
* `^c`
    * Press `c` while holding the `control` key down (ctrl-c)
    * Quit out of most programs when they're running. It kills the progam/terminal command that's currently executing.
* `$ ./` runs "executable" files
    * How do you know if it's an "executable" file?
        * It will usually not have a file extension.
        * Run the `file` command on it and see if "executable" is somewhere in the output.
    * Python files are the exception. They can't be run using `./`.
* Different Data Types:
    * ASCII
        * Readable text
        * e.g. `hello`
    * Decimal
        * Our normal number system
        * Base10 (0-9)
        * e.g. `114`
    * Binary
        * All 1's and 0's
        * Base2 (0,1)
        * Can also be recognized by a `0b` prefix (e.g. `0b1011'`)
        * e.g. `10101110`
    * Hex
        * Found in sets of two characters/integers
        * Base16 (0-9)(A-F)
        * Can also be recognized by a `0x` prefix (e.g. `0x0F`)
        * e.g. `0F AF C4 54`
    * Base64
        * An unreadable string
        * Usually comprised of integers (ranging from 0 to 9), uppercase letters, and lowercase letters
        * Usually pretty long
        * Sometimes ends in one or two equal signs (but sometimes it doesn't!)
        * e.g. `WW91IGZvdW5kIG1lISBUaGlzIGlzIGFuIGVhc3RlciBlZ2cgdGhhdCBKb3NodWEgU2hpbmtsZSBjcmVhdGVkIQo=`
    * Octal
        * Base8 (0-7)
        * e.g. `27`

# Pipe
### Description:
* This isn't a command
* It's this character-> |
* It passes the output of the first command as the input to the second command

### Usage:
`$ command1 | command2`

### Examples:
* $ ls | grep "Do"
* $ cat names.txt | sort
* $ cat names.txt | sort | unique

# tar
### Description:
Bundles files into (or extracts files from) a `.tar` which can be thought of like a `.zip` file.

### Usage:
* `$ tar -cvf tarfile.tar file1 file2 file3`
    * Create a tar file that holds several other files
* `$ tar -xvf tarfile.tar`
    * Extracts files from a tar file

### Examples:
* $ tar -cvf challenge.tar script.py README.md hint.png
* $ tar -xvf notepad.tar

# regex
This isn't a terminal command. It's a sequence of characters that forms a search pattern. Check out this link for symbols and their examples: https://www.hallme.com/blog/the-power-of-regular-expressions/

# Helpful Links
#### Data Converter
* https://www.rapidtables.com/convert/number/ascii-hex-bin-dec-converter.html
    * For some reason, some converters online just don't work!

### JSON Beautifier
* http://www.jsnice.org/
    * Pass messy JSON (ex. JSON that's crammed onto one line) into this web tool, and it will add perfect spacing to it, making it much more readable.

### Base64 File Decoder
* https://www.base64decode.org/
    * You can drag and drop an entire Base64 encoded file into this web tool, and it will return the decoded file.

### ASCII Table
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

# 
### Description:

### Usage:

### Examples: