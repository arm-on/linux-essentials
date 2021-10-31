# Linux Essentials

| | |
|-|-|
|__command__|__what it does__|
|__General__|
| clear | clear the terminal | 
| history | list all of the commands we executed |
| du -hs /path/to/a/directory/ | see the volume of a directory |
| df -h | see the disk space left for all of the disks |
| nvtop | see the status of the NVIDIA GPU |
| htop | see the status of the CPUs and RAM |
| pwd | show the current directory that the commands are being executed in |
|__HELP__|
| ls --help | documentation of the "ls" command |
| man echo | manual of the "echo" command |
| info echo | more information about the "echo" command (Note: More complete than "man" and "help" commands) |
| whatis ls | what is "ls"? (a very short answer to this) |
|__Audio/Video__|
| ffmpeg -i whatever.webm -c copy whatever.mp4 | convert webm file to mp4 |
|__Working with Files__|
|cd /the/path/of/a/folder/ | change directory |
| cd ~ | change directory to the home dir |
| cd / | change directory to the root dir |
| ls | list the files in the current directory |
|ls -a | list the files in the current directory (including the hidden files) (-a means all) - the files having . at the beginning of their names are hidden |
| ls -l | list the files in the directory with more information (including their read/write access, owner, volume, date&time of creation) |
| ls -la | list ALL of the files in the directory with more information (including their read/write access, owner, volume, date&time of creation) |
| ls /path/to/some/directory/ | list the files in a given directory |
| ls mypattern* | list the files in the current directory with names starting with "mypattern" |
| ls *mypattern | list the files in the current directory with names ending with "mypattern" |
|rm -rf /directory/ | remove everything inside a directory ("r" is for recursive deletion, "f" removes read-only files without asking |
| mkdir directory_name | make a new directory (folder) |
| touch test.txt | make a new file named "test.txt" in the current directory |
| nano test.txt | edit the "test.txt" file in terminal |
| cat test.txt | print the content of "test.txt" in the terminal |
| rm test.txt | remove the file "test.txt" |
| rm porteqal.mp4 sound.mp3 linux.png | remove the three files "porteqal.mp4", "sound.mp3", and "linux.png" |
| rmdir /mydirectory/ | remove the directory "mydirectory" (NOTE: works if it's empty) |
| sudo chmod +x myscript.sh | make the script "myscript.sh" executable |
| x=2 | define the variable "x" to be 2 |
| echo $x | print the content of the variable "x" |
| echo "salam" | print the word "salam" |
| echo $a $b | print the content of the variable "a", then a space, and then the content of the variable "b" |
| scp -r speaker* arman@120.233.50.2:~/wavfiles | Copy the folders whose name start with "speaker" from here to the server 120.233.50.2, while logging into that server with the username "arman" |
| cp test.txt /path/to/a/directory | copy the file "test.txt" to a directory |
| cp -r * /path/to/a/directory/ | copy everything inside the current directory (including the folders) to another directory |
| cp -r /first/dir/ /second/dir/ | copy the first directory into the second directory |
| mv test.txt /path/to/a/directory/ | move the file "test.txt" to another directory |
| mv *.txt /path/to/a/directory/ | move all of the files whose name end with ".txt" to another directory |
| mv a.txt b.txt | rename "a.txt" to "b.txt" |
| whereis ls | show the directory in which the "ls" library exists |
| less a.txt | read the contents of a text file one page(one screen) at a time. |
|__Compression__|
| zip media.zip porteqal.mp4 sound.mp3 linux.png | make a zip file containing the tree files "porteqal.mp4", "sound.mp3", and "linux.png". Name the file "media.zip" |
| unzip media.zip | decompress the file "media.zip", and move its contents to the current directory |
| zip linux.zip /path/to/a/directory/ | make a compressed file containing a directory itself (without the files it contains!!!) |
| zip -r tutorial.zip /path/to/a/directory/  | make a compressed file containing a directory and its contents | 
| unzip media.zip /path/to/a/directory/ | decompress the file "media.zip", and move its contents to a desired directory |
| tar -cf myfile.tar porteqal.mp4 sound.mp3 linux.png | "create" a tar "file" (a compressed file with no volume decreasion), given a list of files |
| tar -xf myfile.tar | decompress (extract) a tar file |
| tar -vxf myfile.tar | decompress (extract) a tar file while printing out the things inside it |
| gzip myfile.tar | compress the given "tar" file (which is not volume-efficient) to a .tar.gz compressed file (more compressed than the tar file) |
| gunzip myfile.tar.gz | decompress the .gz file into the .tar file |
| bzip2 myfile.tar | compress the given "tar" file into a .tar.bz2 compressed file (more compressed than "tar") |
| bunzip2 myfile.tar.bz2 | decompress the .bz2 file into the .tar file |
| tar -cvzf media.tgz sound.mp3 porteqal.mp4 | compress some files directly to a tar gzip file (instead of first compressing as "tar", and then "gzip") - Note: "v" stands for "verbose mode" |
| tar -cvjf media.bz2 sound.mp3 porteqal.mp4 | compress some files directly to a tar bzip file (instead of first compressing as "tar", and then "bzip") |
| tar -xvzf media.tgz  | Decompress the .tgz file directly into the original files |
| tar -xvjf media.bz2 | Decompress the .bz2 file directly into the original files |
|__Search for Information / Information Extraction from Files__|
| less myfile.txt | displays the content of a file "page by page" with scrolling option |
| head myfile.txt | Displays the first 10 lines of a file |
| tail myfile.txt | Displays the last 10 lines of a file |
| head -n 15 myfile.txt | Displays the first 15 lines of a file |
| tail -n 15 myfile.txt | Displays the last 15 lines of a file |
| sudo find / | Search in the whole files and directories recognized by the OS for files, and list them |
| find Downloads/ -type f | Search for files (not folders) in the "Downloads" folder (and list them!) |
| sudo find / -name "python" | Search for files and directories named "python", and list them |
| sudo find / -name "python*" | Search for files and directories whose name starts with "python" |
| grep arman myfile.txt | Search for the expression "arman" inside the file "myfile.txt", and if it exists, print the token containing it (e.g., print "arman.ir") - Note: If the expression doesn't exist, the output of this command will be empty! |
| grep arman * | Search for the expression "arman" inside all of the files inside the current directory, and show the results (as a list) |
| grep "arman malekzadeh" * | Search for the long expression "arman malekzadeh" inside all of the files inside the current directory, and show the results (as a list) |
| sort myfile.txt | Display the content of the file "myfile.txt" (with lines sorted alphabetically!) - Note: Each line is considered as a separate string |
| sort -n myfile.txt  | Display the content of the file "myfile.txt" (with lines sorted based on numbers) - Note: Each line is considered as a separate string |
| sort -r myfile.txt | Display the content of the file "myfile.txt" sorted in the reverse order |
| sort -R myfile.txt | Display the content of the file "myfile.txt" sorted randomly! |
| cut -c3-6 myfile.txt | Display the content of the file "myfile.txt", but only columns 3 to 6 for each line |
| cut -c3,6 myfile.txt | Display the content of the file "myfile.txt", but only the third and sixth character for each line |
| cut -c3- myfile.txt | Display the content of the file "myfile.txt", but only the third character and everything after it, for each line |
| cut -d" " -f4 myfile.txt  | Split the contents of a file using the space character, consider each part as a "field", and display the content of the fourth field - Note: this is useful for reading "csv" files |
| cut -d" " -f4- myfile.txt  | Split the contents of a file using the space character, consider each part as a "field", and display the content of the fourth field, and every field after it |
| cut -d" " -f4-6 myfile.txt  | Split the contents of a file using the space character, consider each part as a "field", and display the content of the fourth field up to the sixth field |
| cut -d" " -f4,6 myfile.txt  | Split the contents of a file using the space character, consider each part as a "field", and display the content of the fourth field and the sixth field |
| cut -d" " -f3-6 myfile.txt > output.txt | Split the contents of a file using the space character, consider each part as a "field", and display the content of the third field up to the sixth field. Finally, write the output into the file "output.txt"  |
| cut -d" " -f3-6 myfile.txt >> output.txt | Split the contents of a file using the space character, consider each part as a "field", and display the content of the third field up to the sixth field. Finally, append the output to the content of the file "output.txt"  |
| wc myfile.txt | Display the number of lines that the file contains, then the number of words (tokens separated by space), and the number of characters |
|__REGEX__|
| grep ^arman myfile.txt | Search for the lines starting with "arman" inside "myfile.txt", and show the results (as a list) |
| grep arman$ myfile.txt | Search for the lines ending with "arman" inside "myfile.txt", and show the results (as a list) |
| grep a.m myfile.txt | Search for the lines starting with "a", having "m" as their third character, (don't care about the second character) inside "myfile.txt", and show the results (as a list) | 
| grep a..m myfile.txt | Search for the lines starting with "a", having "m" as their fourth character, (don't care about the second and third characters) inside "myfile.txt", and show the results (as a list) | 
| grep ^....$ myfile.txt | Search for the lines having only 4 characters inside "myfile.txt", and show the results (as a list) | 
|__PIPE__|
| command1 \| command2 | run the first command, and take its output to the second command as its input |
| ls \| grep ^D |/ list the files of the current directory, but only show the results starting with the "D" character |
| ls \| grep s$ | list the files of the current directory, but only show the results ending with the "s" character   |
| find . type f \| grep python | find the files in the system named "python" |
| cut -d" " -f3 myfile.txt \| cut -c2 |display the second character of the third token from each row |
|__BASH__|
| ls sh | get the path to the interpreter of the bash language |
| #!/bin/bash </br> your bash code goes here | how to write a shell script with bash |
| #! /etc/bash</br> echo "please write your name" </br> if [[ "$1" == "arman" ]]; </br> then </br>&nbsp;&nbsp;&nbsp;&nbsp;echo "yes" </br>else </br>&nbsp;&nbsp;&nbsp;&nbsp; echo "no" </br>fi | a demo bash script using the conditional statement "if" |
| sudo chmod 777 myscript.sh | Give the full permission to everyone to do everything with the file "myscript.sh" (including the permission to run it) |
| bash ./myscript.sh | run my shell script named "myscript.sh" |
| bash ./myscript.sh arman | run my shell script named "myscript.sh" taking "arman" as input |
| #! /etc/bash</br>for i in {1..10}</br>do</br>&nbsp;&nbsp;&nbsp;&nbsp;echo $i</br>done | print the numbers 1 to 10 |
| #! /etc/bash</br>for (( i=1 ; i <= 50 ; i++ ))</br>do</br>&nbsp;&nbsp;&nbsp;&nbsp; echo "number : $i$"</br>done</br>echo "done" | write the numbers from 1 to 50 with a "number : " string on the left side of them |
|__MAIN DIRECTORIES IN LINUX__|
| etc | all of the linux tools are here, including bluetooth, apache, python, and everything you can install on it. So, if you wanna configure sth, here is the place to look for the .conf file |
| bin | contains the code for all of the commands such as "ls" |
| lib | contains the libraries |
| /var/log | the logs in linux are here |
| dmsg | show the logs in a beautiful way (for instance, if you connect a usb, this will show sth) |
|__PROCESSES__|
| ps | list the processes that are running |
| ps -aux | show the list of the processes being run by any user, along with the process IDs (PIDs) (Note: aux stands for all user execute) |
| kill 5577 | kill the process with ID 5577 |
| top | show the processes that are being run (live!) |
| free | show the ram (memory), how much of it is used, how much is free, and the same things for the swap (which is used to accelerate the speed of the system) |
| free -tb | show the ram (memory), how much (how many bytes) of it is used, how much is free, and the same things for the swap (which is used to accelerate the speed of the system) |
| free -tm | show the ram (memory), how much (how many megabytes) of it is used, how much is free, and the same things for the swap (which is used to accelerate the speed of the system) |
|__NETWORKING__|
| /etc/resolv.conf | the file containing the configure of the DNS </br>It may contain sth like this:</br>`nameserver 127.0.0.25`</br>`options edns0`</br>`search localdomain` </br> To add another DNS (like the DNS server of the google which is 8.8.8.8), append the following line:</br>nameserver 8.8.8.8 |
| ifconfig | shows some information about the conifiguration of the network (such as the MAC address), the networking cards, ...  (Note: "if" stands for "interface") |
| ifconfig -a | show the network cards including the disabled ones |
| sudo ifconfig eth0 192.168.245.120 | change the ip address of the network card "eth0" to 192.168.245.120 |
| sudo ifconfig eth0 down | disable the network card "eth0" |
| sudo ifconfig eth0 up | enable the network card "eth0" |
| dig arman.ir | reveal some information about the website "arman.ir" including the IP addresses it has - Actually, this command sends a request to the nameservers of the website |
| ping 192.168.200.567 | send requests to the given ip address to see if we can have a connection with the device (pc) having that ip address - Note: in the result of this command, you will see "TTL". If the value of "ttl" is more than 100, the pc has a windows installed on it. Otherwise, the OS is linux. - Note2: You are not required to write an ip address. Instead, you can write a domain, such as `ping arman.ir` - Note3: This command is used to see if the connection between two clients or a client and a server has been established |
|__USERS__|
| who | shows the current user, with a little bit of extra info |
| w | shows which users are logged in, the time of their login, and what they are doing |
| whoami | shows the current user's name |
| id | shows the unique id of the current user, the groups he/she belongs to - Note: From 0 to 499, is for system users, and 500 to 6000 is for standard users |
| id anotheruser | shows the unique id of the given user named "anotheruser", the groups he/she belongs to |
| cat /etc/passwd | the file `/etc/passwd` contains information about all of the users, including the uid of them and the id the group they belong to, and the home directory (a.k.a profile) (for the standard users) |
| cat /etc/group | the file `/etc/group` contains information about all of the groups, including the id of each group and the users belonging to each group |
| sudo cat /etc/shadow | the file `/etc/shadow` contains the hashed passwords for all users |
| sudo command | execute the command using the permission level of the `root` user |
| su arman | change the user to `arman` in order to execute commands on his/her behalf (this will ask for the password of the user `arman`) |
| sudo adduser arman | create a new user named `arman` - Note: this will ask for a password for the new user, and some other info (such as phone number!) |
| sudo addgroup mynewgroup | create a new group named `mynewgroup` |
| sudo passwd | change the password of the current user |
| sudo passwd arman | change the password of the user named `arman` |
| last | shows the last logins in the system |
| sudo usermod -a -G mygroup arman| Add the user `arman` to the group `mygroup` ("a" stands for "add", "G" for "group") |
| sudo usermod -a -G root arman | Add the user `arman` to the `root` group |
| sudo userdel arman | delete the user `arman`, but keep his/her profile - Note: the path `/home/arman/` will remain. |
| sudo userdel -r arman | delete the user `arman` and his/her profile (files) |
| sudo groupdel mygroup | delete a group named `mygroup` |
|__PERMISSIONS__|
| ls -l | The first character: "d" means directory, and "-" means file</br>The three characters after that: "r" = read, "w" = write, "x" = execute. If instead of any of them, a "-" is written, means that we cannot "read", "write" or "execute" that file. </br> The first three characters correspond to the permissions of the owner of the file</br>The second three characters correspond to the group members of the owner </br>The last three characters correspond to other users (any kind of user) </br>The "execute" permission for directories means changing directory to those dirs (using the `cd` command) |
| About the numbers of the characters mentioned above | "r" (read) = 4, "w" (write) = 2, "x" (execute) = 1 - Note that the sum of them is 7.</br>So, 777 means that anyone can do anything with that file/directory |
| sudo chmod u  | give the permission of ... to the user named `` |
| sudo chmod o  | give the permission of ... to the other users named `` |
| sudo chmod g+w myfile.txt  | give the permission to write ("w") to the file "myfile.txt" to the group members of the owner of the file |
| sudo chmod uog+w myfile.txt  | give the permission to write ("w") to the file "myfile.txt" to everyone |
| sudo chmod g+rw myfile.txt  | give the permission to read and write ("rw") to the file "myfile.txt" to the group members of the owner of the file |
| sudo chmod g+rxw myfile.txt  | give the permission to read, execute and write ("rxw") to the file "myfile.txt" to the group members of the owner of the file |
| sudo chmod g+rxw myfile.txt  | give the permission to read, execute and write ("rxw") to the file "myfile.txt" to the group members of the owner of the file |
| sudo chmod gou-wx myfile.txt | take away the permissions to write to and execute the file "myfile.txt" from every user |
| sudo chmod ug+w myfile.txt | give the permission to write to the file "myfile.txt" to the owner and the group it belongs to |
| sudo chmod 700 myfile.txt | give the permission to do anything to the owner of the file "myfile.txt", and do nothing to others |
| sudo chmod +x myfile.txt | give the permission to write to the file "myfile.txt" to everyone! |
| sudo chown arman myfile.txt | change the owner of the file "myfile.txt" to the user "arman" |
| sudo chgrp mygroup myfile.txt | change the group of the file "myfile.txt" to the group "mygroup" |
| sudo chown arman myfolder -R | change the owner of the directory named "myfolder" to the user "arman", along with all of its subfolders and files inside it |
|__SYMBOLIC LINKS (EQUIVALENT OF SHORTCUTS IN WINDOWS)__|
| ln -s /path/to/the/original/file.txt myshortcut.txt | create a shortcut of the file which is located at `/path/to/the/original/file.txt` in the current directory, and name it as `myshortcut.txt` |
|__STICKY BIT__|
| sudo chmod o+t myfolder/ | every user can only change the files that he/she owns |
| sudo chmod 777 myfolder | remove the sticky bit mode |
|__AWS__|
| aws s3 cp /path/to/a/file.txt s3://[bucket-name]/path/to/file.txt --endpoint-url https://[bucket-name].parspack.net | copy a file to a bucket |
| aws s3 cp /path/to/a/folder s3://[bucket-name]/ --recursive --endpoint-url https://[bucket-name].parspack.net | copy a folder to a bucket |
| aws s3 ls s3://[bucket-name]/path/to/a/folder/ -endpoint-url https://[bucket-name].parspack.net | list the contents of a folder |
|__ANACONDA__|
| source ~/anaconda3/bin/activate | activate the Anaconda's environment |