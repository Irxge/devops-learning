**Bandit level 1-20**

Level 0

Task :The password for the next level is stored in a file called
**readme** located in the home directory.

Solution : <img src="screenshots/media/image11.png"
style="width:6.5in;height:1.625in" />

Explanation: Logged in as bandit1, then used cat to print the contents
of the readme file, which held the password for level 2.

Level 1

Task:The password for the next level is stored in a file called **-**
located in the home directory

Solution : <img src="screenshots/media/image8.png"
style="width:5.82292in;height:1.85417in" />

Explanation: Adding "./" forces cat to treat it as an actual file in the
current directory.

Challenges: The filename itself was the obstacle , needed to know the
"./" trick to reference a file named "-"

Level 2

Task: The password for the next level is stored in a file called
--spaces in this filename-- located in the home directory

Solution: <img src="screenshots/media/image4.png"
style="width:6.5in;height:1.59722in" />

Explanation: Spaces needed quotes; leading "--" needed "./" so cat
didn't read it as options.

Level 3

Task:The password for the next level is stored in a hidden file in the
**inhere** directory.

Solution:

<img src="screenshots/media/image2.png"
style="width:6.29688in;height:2.79525in" />

Explanation: Ls doesn't show hidden files, using ls -la revealed a file
named "...Hiding-From-You"

challenges:The file was hidden

Level 4

Task:The password for the next level is stored in the only
human-readable file in the **inhere** directory. Tip: if your terminal
is messed up, try the “reset” command.

Solution:

<img src="screenshots/media/image21.png"
style="width:3.60938in;height:3.75345in" />

Explanation:Most files came back as "data" when checked with file,
meaning binary junk. -file07 was the only one marked ASCII text, so
that's the one with the real password.

Challenges: Had to check file types first since there was no way to tell
which file was readable just by name.

Level 5

Task : The password for the next level is stored in a file somewhere
under the **inhere** directory and has all of the following properties:

- human-readable

- 1033 bytes in size

- not executable

Solution:

<img src="screenshots/media/image12.png"
style="width:7.02083in;height:1.15008in" />

Explanation:

Used find to search all the subfolders inside inhere at once, filtering
for a regular file, exactly 1033 bytes, and not executable which is much
faster than checking each folder by hand.

Challenges :

Had to dig through man find to find the right size/executable flags.

Level 6

Task: The password for the next level is stored **somewhere on the
server** and has all of the following properties:

- owned by user bandit7

- owned by group bandit6

- 33 bytes in size

Solution:

<img src="screenshots/media/image19.png"
style="width:6.5in;height:1.06944in" />

Explanation : filtering by file size, owner, and group all at once.
Redirected error messages (from folders I don't have permission to
access) to /dev/null so only the real match showed up.

Level 7

Task : The password for the next level is stored in the file
**data.txt** next to the word **millionth**

Solution:

<img src="screenshots/media/image9.png"
style="width:5.27604in;height:1.11609in" />

Explanation : grep scans a file line by line and prints any line
containing the given pattern

Level 8

Task : The password for the next level is stored in the file
**data.txt** and is the only line of text that occurs only once

Solution :

<img src="screenshots/media/image14.png"
style="width:4.93229in;height:1.26259in" />

Explanation : The -u flag on uniq stands for unique it tells uniq to
print only the lines that have no duplicates at all

Level 9

Task: The password for the next level is stored in the file **data.txt**
in one of the few human-readable strings, preceded by several ‘=’
characters.

Solutions:

<img src="screenshots/media/image5.png"
style="width:5.55729in;height:1.45225in" />

Explanation: strings pulls out only the readable text. Piping that into
grep with several = signs filtered it down to the lines around the
password.

Challenges: My first grep had the arguments backwards and wasn't
connected to strings. Piping fixed that

Level 10

task:The password for the next level is stored in the file **data.txt**,
which contains base64 encoded data

Solution :

<img src="screenshots/media/image6.png"
style="width:6.16667in;height:1.1875in" />

Explanation : The file's contents looked like random letters and numbers
ending in ==, which is typical of Base64. Piping it into base64 -d
decoded it back to plain text.

Level 11

Task : The password for the next level is stored in the file
**data.txt**, where all lowercase (a-z) and uppercase (A-Z) letters have
been rotated by 13 positions

Solution:

<img src="screenshots/media/image3.png"
style="width:6.5in;height:1.09722in" />

Explanation : tr swaps each letter for the one 13 places along, which
undoes the shift and reveals the sentence with the password.

Challenges: tr needed separate ranges for lowercase and capitals

Level 12

Task: The password for the next level is stored in the file
**data.txt**, which is a hexdump of a file that has been repeatedly
compressed. For this level it may be useful to create a directory under
/tmp in which you can work. Use mkdir with a hard to guess directory
name. Or better, use the command “mktemp -d”. Then copy the datafile
using cp, and rename it using mv (read the manpages!)

Solution: <img src="screenshots/media/image7.png"
style="width:4.32813in;height:2.89583in" /><img src="screenshots/media/image13.png"
style="width:4.36458in;height:2.79778in" />

Explanation : I used file to check each file type, then used the correct
command to extract it until I reached the final text file.

Challenges :

The main challenge was knowing which command to use for each file type.
I also made a few mistakes with tar, but fixed them using the error
messages.

Level 13

Task : The password for the next level is stored in
/etc/bandit_pass/bandit14 and can only be read by user bandit14. For
this level, you don’t get the next password, but you get a private SSH
key that can be used to log into the next level. Look at the commands
that logged you into previous bandit levels, and find out how to use the
key for this level.

Solution :

<img src="screenshots/media/image18.png"
style="width:6.5in;height:1.34722in" />

Level 14

Task: The password for the next level can be retrieved by submitting the
password of the current level to **port 30000 on localhost**.

Solution:

<img src="screenshots/media/image17.png"
style="width:6.5in;height:0.98611in" />

Explanation : I used cat to read the current Bandit14 password and piped
it to nc, which sent the password to the service running on port 30000.

**Challenges:**

The main challenge was figuring out that the password needed to be sent
to a local network service using nc

Level 15:

Task: The password for the next level can be retrieved by submitting the
password of the current level to **port 30001 on localhost** using
SSL/TLS encryption.

Solution:

<img src="screenshots/media/image10.png"
style="width:6.5in;height:1.02778in" />

Explanation:

I used cat to read the Bandit15 password and \| to send it to ncat. I
used --ssl because the service requires an encrypted SSL connection, and
localhost 30001 connects to the service running on port 30001

Challenges : --ssl

Level 16

Task:The credentials for the next level can be retrieved by submitting
the password of the current level to **a port on localhost in the range
31000 to 32000**. First find out which of these ports have a server
listening on them. Then find out which of those speak SSL/TLS and which
don’t. There is only 1 server that will give the next credentials, the
others will simply send back to you whatever you send to it.

Solution :

Level 16 → 17

bandit16@bandit:~\$ nmap -p 31000-32000 localhost

31790/tcp open

bandit16@bandit:~\$ cat /etc/bandit_pass/bandit16 \| ncat --ssl
localhost 31790

Correct!

-----BEGIN OPENSSH PRIVATE KEY-----

\[private key\]

-----END OPENSSH PRIVATE KEY-----

bandit16@bandit:~\$ vim /tmp/bandit17.key

bandit16@bandit:~\$ chmod 600 /tmp/bandit17.key

bandit16@bandit:~\$ exit

ragei2004@cloudshell:~\$ scp -P 2220
bandit16@bandit.labs.overthewire.org:/tmp/bandit17.key /tmp/bandit17.key

bandit16@... password:

100%

ragei2004@cloudshell:~\$ chmod 600 /tmp/bandit17.key

ragei2004@cloudshell:~\$ ssh -p 2220 -i /tmp/bandit17.key
bandit17@bandit.labs.overthewire.org

bandit17@bandit:~\$

**Explanation**: I used nmap to find the open port, then used ncat --ssl
to get the SSH key. I saved and copied the key, then used it to log into
Bandit17.

**Challenges:** The main challenge was finding the correct port and
saving the SSH key correctly.

Level 17

Task : There are 2 files in the homedirectory: passwords.old and
passwords.new. The password for the next level is in passwords.new and
is the only line that has been changed between passwords.old and
passwords.new

Solution :

<img src="screenshots/media/image16.png"
style="width:6.5in;height:2.20833in" />

**Explanation:  
** I used ls to see the two files, then used diff to compare them. The
different line marked with \> was from passwords.new, which gave me the
password for Bandit18.

**Challenges:  
** The main challenge was understanding the diff output and knowing that
\< refers to the first file and \> refers to the second file.

Level18

Task The password for the next level is stored in a file **readme** in
the homedirectory. Unfortunately, someone has modified **.bashrc** to
log you out when you log in with SSH.

Solution :

<img src="screenshots/media/image20.png"
style="width:6.5in;height:2.80556in" />

Explanation :

I used SSH to run commands directly because the normal shell immediately
logged me out. I used ls to find the readme file, then used cat readme
through SSH to read the password.

Level 19

task:To gain access to the next level, you should use the setuid binary
in the homedirectory. Execute it without arguments to find out how to
use it. The password for this level can be found in the usual place
(/etc/bandit_pass), after you have used the setuid binary.

Solution:

<img src="screenshots/media/image15.png"
style="width:6.5in;height:2.29167in" />

**Explanation:  
** I used file to identify bandit20-do as a setuid executable. I then
used it to run commands as bandit20, including cat to read the Bandit20
password file.

**Challenges:  
** The main challenge was understanding what a setuid executable does
and how bandit20-do allows commands to be run as another user.

**Level 20**

Task : There is a setuid binary in the homedirectory that does the
following: it makes a connection to localhost on the port you specify as
a commandline argument. It then reads a line of text from the connection
and compares it to the password in the previous level (bandit20). If the
password is correct, it will transmit the password for the next level
(bandit21).

Solution :

<img src="screenshots/media/image1.png"
style="width:6.5in;height:1.23611in" />

Explanation: suconnect connects to a port on localhost, reads a line,
and checks it against the bandit20 password. nc -l listens on a port of
my choosing and sends that password to whatever connects. The & runs the
listener in the background so I can start suconnect from the same shell.

Challenges: A second Cloud Shell tab kept timing out, so I couldn't run
the listener and suconnect in two windows. Running the listener in the
background with & fixed it.
