# Linux Essentials

Table of contents:<br>
- [Linux Essentials](#linux-essentials)
  - [General](#general)
  - [Help](#help)
  - [Audio/Video](#audiovideo)
  - [Working with Files](#working-with-files)
  - [Compression](#compression)
  - [Search for Information / Information Extraction from Files](#search-for-information--information-extraction-from-files)
  - [REGEX](#regex)
  - [Pipe](#pipe)
  - [Bash](#bash)
  - [Main Directories in Linux](#main-directories-in-linux)
  - [Processes](#processes)
  - [Networking](#networking)
    - [How to configure static ip address](#how-to-configure-static-ip-address)
  - [Users](#users)
  - [Permissions](#permissions)
  - [SYMBOLIC LINKS (EQUIVALENT OF SHORTCUTS IN WINDOWS)](#symbolic-links-equivalent-of-shortcuts-in-windows)
  - [Sticky Bit](#sticky-bit)
  - [AWS](#aws)
  - [Anaconda](#anaconda)
  - [GPU](#gpu)
    - [How to Install CUDA](#how-to-install-cuda)
  - [Screen (Do Something while I'm gone)](#screen-do-something-while-im-gone)
  - [Server](#server)
  - [Docker](#docker)
  - [Common Problems](#common-problems)
## General
[Back to top](#)
| | |
|-|-|
|__command__|__what it does__|
| clear | clear the terminal | 
| history | list all of the commands we executed |
| du -hs /path/to/a/directory/ | see the volume of a directory |
| df -h | see the disk space left for all of the disks |
| nvtop | see the status of the NVIDIA GPU |
| htop | see the status of the CPUs and RAM |
| pwd | show the current directory that the commands are being executed in |
| rm -rf ~/.local/share/Trash/* | Empty the trash |
| lsof / \| grep deleted | List the files that should have been deleted, but are not deleted until now! |
| lsof\|grep deleted\|awk '{print $2}'\|xargs kill -9 | Get rid of the deleted files for which a job/process is still open, preventing the file from being deleted |
| pip cache purge | clear the cache for pip |
## Help
[Back to top](#)
| | |
|-|-|
| ls --help | documentation of the "ls" command |
| man echo | manual of the "echo" command |
| info echo | more information about the "echo" command (Note: More complete than "man" and "help" commands) |
| whatis ls | what is "ls"? (a very short answer to this) |
## Audio/Video
[Back to top](#)
| | |
|-|-|
| ffmpeg -i whatever.webm -c copy -strict experimental whatever.mp4 | convert webm file to mp4 (Note: "-strict experimental" was added due to the outdated ffmpeg package) |
| ffmpeg -fflags -genpts -i whatever.webm -r 24 whatever.mp4 | convert webm file to mp4 (Another method) |
| ffmpeg -i input.mp3 -acodec pcm_s16le -ac 1 -ar 16000 out.wav | convert 'input.mp3' to a wav file named 'out.wav' (16000 and mono) |
## Working with Files
[Back to top](#)
| | |
|-|-|
| sudo du -aBm / 2>/dev/null \| sort -nr \| head -n 10 | list the biggest files/directories in terms of volume (top 10) |
| du -hsx * \| sort -rh \| head -10 | list the biggest files/directories in terms of volume (top 10) |
| find . -type f -printf '%s %p\n'\| sort -nr \| head -10 \| numfmt --field=1 --to=iec | list the largest files in terms of volume (top 10) |
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
| scp -r /Users/armanmalekzadeh/Documents/BERT-NEW/ user01@123.22.456.22:~/arman/BERT-Refactor/codes/training/bert-checkpoints/ | Copy the folders and files inside the "BERT-NEW" directory on my own laptop to the "bert-checkpoints" directory on a remote server |
| cp test.txt /path/to/a/directory | copy the file "test.txt" to a directory |
| cp -r * /path/to/a/directory/ | copy everything inside the current directory (including the folders) to another directory |
| cp -r /first/dir/ /second/dir/ | copy the first directory into the second directory |
| cp -a /source/. /dest/ | copy everything from the "source" to the "dest" folder |
| rsync -vau --remove-source-files source/ dst/ | Move all files from the "source/" directory to the "dst/" directory (Note: It's sometimes faster than the "cp"/"mv" command) |
| mv test.txt /path/to/a/directory/ | move the file "test.txt" to another directory |
| mv *.txt /path/to/a/directory/ | move all of the files whose name end with ".txt" to another directory |
| mv a.txt b.txt | rename "a.txt" to "b.txt" |
| whereis ls | show the directory in which the "ls" library exists |
| less a.txt | read the contents of a text file one page(one screen) at a time. |
## Compression
[Back to top](#)
| | |
|-|-|
| zip media.zip porteqal.mp4 sound.mp3 linux.png | make a zip file containing the tree files "porteqal.mp4", "sound.mp3", and "linux.png". Name the file "media.zip" |
| unzip media.zip | decompress the file "media.zip", and move its contents to the current directory |
| zip linux.zip /path/to/a/directory/ | make a compressed file containing a directory itself (without the files it contains!!!) |
| zip -r tutorial.zip /path/to/a/directory/  | make a compressed file containing a directory and its contents | 
| unzip media.zip -d /path/to/a/directory/ | decompress the file "media.zip", and move its contents to a desired directory |
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
## Search for Information / Information Extraction from Files
[Back to top](#)
| | |
|-|-|
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
## REGEX
[Back to top](#)
| | |
|-|-|
| grep ^arman myfile.txt | Search for the lines starting with "arman" inside "myfile.txt", and show the results (as a list) |
| grep arman$ myfile.txt | Search for the lines ending with "arman" inside "myfile.txt", and show the results (as a list) |
| grep a.m myfile.txt | Search for the lines starting with "a", having "m" as their third character, (don't care about the second character) inside "myfile.txt", and show the results (as a list) | 
| grep a..m myfile.txt | Search for the lines starting with "a", having "m" as their fourth character, (don't care about the second and third characters) inside "myfile.txt", and show the results (as a list) | 
| grep ^....$ myfile.txt | Search for the lines having only 4 characters inside "myfile.txt", and show the results (as a list) | 
## Pipe
[Back to top](#)
| | |
|-|-|
| command1 \| command2 | run the first command, and take its output to the second command as its input |
| ls \| grep ^D |/ list the files of the current directory, but only show the results starting with the "D" character |
| ls \| grep s$ | list the files of the current directory, but only show the results ending with the "s" character   |
| find . type f \| grep python | find the files in the system named "python" |
| cut -d" " -f3 myfile.txt \| cut -c2 |display the second character of the third token from each row |
## Bash
[Back to top](#)
| | |
|-|-|
| ls sh | get the path to the interpreter of the bash language |
| #!/bin/bash </br> your bash code goes here | how to write a shell script with bash |
| #! /etc/bash</br> echo "please write your name" </br> if [[ "$1" == "arman" ]]; </br> then </br>&nbsp;&nbsp;&nbsp;&nbsp;echo "yes" </br>else </br>&nbsp;&nbsp;&nbsp;&nbsp; echo "no" </br>fi | a demo bash script using the conditional statement "if" |
| sudo chmod 777 myscript.sh | Give the full permission to everyone to do everything with the file "myscript.sh" (including the permission to run it) |
| bash ./myscript.sh | run my shell script named "myscript.sh" |
| bash ./myscript.sh arman | run my shell script named "myscript.sh" taking "arman" as input |
| #! /etc/bash</br>for i in {1..10}</br>do</br>&nbsp;&nbsp;&nbsp;&nbsp;echo $i</br>done | print the numbers 1 to 10 |
| #! /etc/bash</br>for (( i=1 ; i <= 50 ; i++ ))</br>do</br>&nbsp;&nbsp;&nbsp;&nbsp; echo "number : $i$"</br>done</br>echo "done" | write the numbers from 1 to 50 with a "number : " string on the left side of them |
## Main Directories in Linux
[Back to top](#)
| | |
|-|-|
| etc | all of the linux tools are here, including bluetooth, apache, python, and everything you can install on it. So, if you wanna configure sth, here is the place to look for the .conf file |
| bin | contains the code for all of the commands such as "ls" |
| lib | contains the libraries |
| /var/log | the logs in linux are here |
| dmsg | show the logs in a beautiful way (for instance, if you connect a usb, this will show sth) |
## Processes
[Back to top](#)
| | |
|-|-|
| ps | list the processes that are running |
| ps -aux | show the list of the processes being run by any user, along with the process IDs (PIDs) (Note: aux stands for all user execute) |
| kill 5577 | kill the process with ID 5577 |
| top | show the processes that are being run (live!) |
| free | show the ram (memory), how much of it is used, how much is free, and the same things for the swap (which is used to accelerate the speed of the system) |
| free -tb | show the ram (memory), how much (how many bytes) of it is used, how much is free, and the same things for the swap (which is used to accelerate the speed of the system) |
| free -tm | show the ram (memory), how much (how many megabytes) of it is used, how much is free, and the same things for the swap (which is used to accelerate the speed of the system) |
## Networking
[Back to top](#)
| | |
|-|-|
| /etc/resolv.conf | the file containing the configure of the DNS </br>It may contain sth like this:</br>`nameserver 127.0.0.25`</br>`options edns0`</br>`search localdomain` </br> To add another DNS (like the DNS server of the google which is 8.8.8.8), append the following line:</br>nameserver 8.8.8.8 |
| ifconfig | shows some information about the conifiguration of the network (such as the MAC address), the networking cards, ...  (Note: "if" stands for "interface") |
| ifconfig -a | show the network cards including the disabled ones |
| sudo ifconfig eth0 192.168.245.120 | change the ip address of the network card "eth0" to 192.168.245.120 |
| sudo ifconfig eth0 down | disable the network card "eth0" |
| sudo ifconfig eth0 up | enable the network card "eth0" |
| dig arman.ir | reveal some information about the website "arman.ir" including the IP addresses it has - Actually, this command sends a request to the nameservers of the website |
| ping 192.168.200.567 | send requests to the given ip address to see if we can have a connection with the device (pc) having that ip address - Note: in the result of this command, you will see "TTL". If the value of "ttl" is more than 100, the pc has a windows installed on it. Otherwise, the OS is linux. - Note2: You are not required to write an ip address. Instead, you can write a domain, such as `ping arman.ir` - Note3: This command is used to see if the connection between two clients or a client and a server has been established |

### The best way to configure DNS

1. Run `sudo nano /etc/netplan/00-installer-config.yaml` to edit this file. The file contains something like this:
   
   ```
      nameservers:
        addresses: [8.8.8.8]
   ```
   Add your preferred DNS in the addresses variable. It will become something like this:

   ```
      nameservers:
        addresses: [123.123.123.123, 234.234.234.234]
   ```
2. Save the file and get back to the terminal. Then run `sudo netplan apply`.

### How to configure static ip address
1. Identify the name of the ethernet interface using `ip link` (or `ip a`, `ip addr`). The output will be something like this:
```
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN mode DEFAULT group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
2: eno1: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc mq state UP mode DEFAULT group default qlen 1000
    link/ether 0c:c4:7a:cc:59:70 brd ff:ff:ff:ff:ff:ff
3: eno2: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc mq state UP mode DEFAULT group default qlen 1000
    link/ether 0c:c4:7a:cc:59:71 brd ff:ff:ff:ff:ff:ff
```
Here the name is `eno1`. It can be `ens1`, `eth0` or sth like that in other cases.

2. Go to the `/etc/netplan/` directory. There are some files with the `.yaml` postfix. Edit those files and make them like this:
```
network:
  version: 2
  renderer: networkd
  ethernets:
    eth0:
      dhcp4: no
      addresses:
        - 192.168.121.199/24
      gateway4: 192.168.121.1
      nameservers:
          addresses: [8.8.8.8, 1.1.1.1]
```
In the above lines, `eth0` is the name of your interface, `192.168.121.199/24‍‍‍` is the static ip address. If you want multiple addresses, type another line for the other address.

3. Test the connection to the network (if you want to) using `sudo netplan try`.

4. Apply the new network plan by running `sudo netplan apply`.

5. Verify the changes by running `ip addr show dev eno1`. Remember that `eno1` was the name of our interface. The output will be something like this:
```
3: eno1: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc mq state UP group default qlen 1000
    link/ether 56:00:00:60:20:0a brd ff:ff:ff:ff:ff:ff
    inet 192.168.121.199/24 brd 192.168.121.255 scope global dynamic eno1
       valid_lft 3575sec preferred_lft 3575sec
    inet6 fe80::5054:ff:feb0:f500/64 scope link 
       valid_lft forever preferred_lft forever
```

---

Note: For older Ubuntu versions (e.g., 16), there might be no `/etc/netplan/` directory. In this case, check for the `/etc/network/interfaces` file. It should look like this:
```
# interfaces(5) file used by ifup(8) and ifdown(8)
auto eno1
iface eno1 inet static
 address 213.220.120.2 (ip address of the server)
 netmask 255.255.255.0 (always the same)
 gateway 213.220.180.1 (ask this from the server admin)
 dns-nameservers 4.4.4.4 8.8.8.8 (always the same)
```

After doing this, restart the network service by running `sudo /etc/init.d/networking restart`.
## Users
[Back to top](#)
| | |
|-|-|
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
| sudo su - arman | change the user to `arman` in order to execute commands on his/her behalf (without asking for their permission). This only works if you are a sudoer. |
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
| sudo adduser arman sudo | add user `arman` to the sudo group |
| usermod -aG sudo arman | add user `arman` to the sudo group |
| sudo deluser arman sudo | revoke sudo access from `arman` |
| `grep -Po '^sudo.+:\K.*$' /etc/group` | get the list of sudoers |

### Passwordless Login using SSH Keys

Everytime you try logging into your server? Are you tired of it? If yes, do the following steps:

1. Run `ssh-keygen -t rsa -b 4096 -C "your_email@gmail.com"` in the terminal. This will create a ssh key-pair. You will be prompted with something like this:
   ```
   Generating public/private rsa key pair.
   Enter file in which to save the key (/Users/armanmalekzadeh/.ssh/id_rsa):
   ```
Consider a new path for the key. For instance, type `/Users/armanmalekzadeh/.ssh/id_rsa_new` and hit enter. You will be asked for a passphrase. Choose something appropriate if you want. Finally, you will be shown something like this:
  ```
  Your identification has been saved in /Users/armanmalekzadeh/.ssh/id_rsa_new
  Your public key has been saved in /Users/armanmalekzadeh/.ssh/id_rsa_new.pub
  The key fingerprint is:
  SHA256:blahblahblah your_email@gmail.com
  The key's randomart image is:
  +---[RSA 4096]----+
  | blah blah blah  |
  +----[SHA256]-----+
  ```

2. Run `ssh-copy-id -i .ssh/id_rsa_test.pub your_user_name@your_server` in the terminal. This will make a copy of the public key on your remote server.
3. Run `nano ~/.ssh/config` to edit `~/.ssh/config`. Add something like this at the end of the file:
   ```
   Host 123.123.123.123 (replace with your_servers_ip)
   HostName 123.123.123.123 (replace with your_servers_ip)
   User your_user_name
   IdentityFile ~/.ssh/id_rsa_new
   ```

## Permissions
[Back to top](#)
| | |
|-|-|
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
| sudo chmod -R 777 /path/to/your/directory | give every user the permission to do everything with the `/path/to/your/directory` and all its contents (including files and folders) |
## SYMBOLIC LINKS (EQUIVALENT OF SHORTCUTS IN WINDOWS)
[Back to top](#)
| | |
|-|-|
| ln -s /path/to/the/original/file.txt myshortcut.txt | create a shortcut of the file which is located at `/path/to/the/original/file.txt` in the current directory, and name it as `myshortcut.txt` |
## Sticky Bit
[Back to top](#)
| | |
|-|-|
| sudo chmod o+t myfolder/ | every user can only change the files that he/she owns |
| sudo chmod 777 myfolder | remove the sticky bit mode |
## AWS
[Back to top](#)
| | |
|-|-|
| aws s3 cp /path/to/a/file.txt s3://[bucket-name]/path/to/file.txt --endpoint-url https://[bucket-name].parspack.net | copy a file to a bucket |
| aws s3 cp /path/to/a/folder s3://[bucket-name]/ --recursive --endpoint-url https://[bucket-name].parspack.net | copy a folder to a bucket |
| aws s3 ls s3://[bucket-name]/path/to/a/folder/ -endpoint-url https://[bucket-name].parspack.net | list the contents of a folder |
## Anaconda
[Back to top](#)
| | |
|-|-|
| source ~/anaconda3/bin/activate | activate the Anaconda's environment |
| conda create --name your_desired_name python=3.8 | make a new environment which uses a specific Python version |
| conda env list | list all environments built inside anaconda |
| conda env remove --name ENVIRONMENT_NAME  | remove the conda environment named "ENVIRONMENT_NAME" |
| jupyter notebook --no-browser --port=8080 | Run a jupyter notebook on the server without using the browser on the port 8080 |
| jupyter notebook password | Define a new password for the jupyter notebook (instead of the token, you will give this password to anyone who will use the jupyter) | 
| jupyter notebook --no-browser --port=8080 --notebook-dir=/home/user01/ | Run a jupyter notebook on the server (at path `/home/user01/` without using the browser on the port 8080 |
| jupyter server list | Get the list of all jupyter servers (the log also contains the token for each notebook) |
| tensorboard --logdir /path/to/save/the/logs --port 8895 | Run Tensorboard on port 8895 and save its logs to the specified directory (logdir) |
| ssh -L 8080:localhost:8888 <REMOTE_USER>@<REMOTE_HOST> | Use a jupyter which is running on port `8888` (on a remote server) on your local port `8080` (by connecting to the `<REMOTE_USER>@<REMOTE_HOST>` using SSH) - This is called "port forwarding" | 

### To install Anaconda for all linux users, do the following steps:

1. Download Anaconda .sh installation file from its website.
2. Run `sudo -i` to be the root user.
3. Run `sudo apt-get update`
4. Execute `bash Anaconda[...].sh` to run the installation file.
5. Accept the license (type yes)
6. For the install location, choose `/opt/anaconda3`
7. It asks "Do you wish the installer to initialize blah blah blah"? Say "yes". (The installation is finished).
8. Run `exit` to again be a normal user.
9. Now your user does not recognize conda (For instance if you type `conda -V`, it will say `command not found`).
10. Run `sudo nano /etc/environment`.
11. At the beginning of the `PATH` variable, after the `"` character, add `/opt/anaconda3/bin:`, and save the file using `CTRL+O`.
12. Log out from your own user and do the SSH again. Now if you run `conda -V`, the user will recognize it.

### Add Users to JupyterHub
1. First, locate the file named `jupyterhub_config.py` using this command:
   ```
   ps aux | grep jupyterhub
   ```
   The result will contain something like this:
   ```
   root     1215751  0.4  0.0 262044 98504 ?        Ssl  10:30   0:01 /opt/py-venvs/py3.11/bin/python3 /opt/py-venvs/py3.11/bin/jupyterhub -f /opt/py-venvs/py3.11/etc/jupyterhub/jupyterhub_config.py
   ```
   Obviously, the path to `jupyterhub_config.py` is there.
2. Inside that `jupyterhub.config.py` file, there is a line similar to the following:
   ```
   c.Authenticator.allowed_users = {'arman', 'another_user', 'blah_blah_user'}
   ```
   Note that the file is very long. So, be patient (or search inside it). Add the desired user to the `allowed_users` variable.
3. Finally, you should restart JupyterHub using this command:
   ```
   sudo systemctl restart jupyterhub
   ```

## GPU
[Back to top](#)
| | |
|-|-|
| Installing CUDA 11.2 and cuDNN 8.1 | [Unofficial Link](https://medium.com/analytics-vidhya/install-cuda-11-2-cudnn-8-1-0-and-python-3-9-on-rtx3090-for-deep-learning-fcf96c95f7a1) - [NVIDIA Link for cuDNN Installation](https://docs.nvidia.com/deeplearning/cudnn/install-guide/index.html) - [How to verify cuDNN Installation](https://stackoverflow.com/questions/31326015/how-to-verify-cudnn-installation/36978616) |
| lsmod \| grep nvidia | Check the GPU Model |
| pgrep nvidia-smi | Get all `nvidia-smi` processes by ID |
| sudo /usr/local/cuda-11.4/bin/cuda-uninstaller | Uninstall CUDA using its own uninstallation script |
| sudo /usr/bin/nvidia-uninstall | Uninstall NVIDIA using its own uninstallation script |
| ubuntu-drivers devices | Get the available NVIDIA drivers along with recommendations |

### How to Install CUDA
- `sudo apt-get update`
- `sudo apt-get install -y build-essential cmake unzip pkg-config`
- `sudo apt-get install -y libxmu-dev libxi-dev libglu1-mesa libglu1-mesa-dev`
- `sudo apt-get install -y libjpeg-dev libpng-dev libtiff-dev`
- `sudo apt-get install -y libavcodec-dev libavformat-dev libswscale-dev libv4l-dev`
- `sudo apt-get install -y libxvidcore-dev libx264-dev`
- `sudo apt-get install -y libgtk-3-dev`
- `sudo apt-get install -y libopenblas-dev libatlas-base-dev liblapack-dev gfortran`
- `sudo apt-get install -y libhdf5-serial-dev graphviz`
- `sudo apt-get install -y python3-dev python3-tk python-imaging-tk`
- `sudo apt-get install -y linux-image-generic linux-image-extra-virtual`
- `sudo apt-get install -y linux-source linux-headers-generic`
- `sudo apt-get purge nvidia*` (remove any nvidia drivers already installed)
- `sudo add-apt-repository ppa:graphics-drivers/ppa` (add graphic drivers ppa)
- `sudo apt-get update`
- `ubuntu-drivers devices` (search for available drivers). The output will be something like this:
```
== /sys/devices/pci0000:00/0000:00:03.0/0000:03:00.0 ==

vendor   : NVIDIA Corporation

model    : GM200 [GeForce GTX TITAN X]

modalias : pci:v000010DEd000017C2sv000010DEsd00001132bc03sc00i00

driver   : nvidia-415 - third-party free

driver   : nvidia-430 - third-party free recommended

driver   : nvidia-418 - third-party free

driver   : nvidia-410 - third-party free

driver   : nvidia-384 - distro non-free

driver   : xserver-xorg-video-nouveau - distro free builtin
```
- `sudo apt-get install nvidia-driver-430` (install the driver with the best version). The result was `unable to locate package`. Run `sudo apt-get install nvidia-430` instead, and it will work!
- `sudo reboot` (before the reboot, `nvidia-smi` won't work. It will say something other than `command not found` which means a driver is there, but it will not work)
- To install tensorflow for a conda env: First activate it, and then run `conda install -c anaconda tensorflow-gpu` (install `tensorflow-gpu`) (while installing this, cuda-toolkit and cudnn will also be installed)
- `apt install nvidia-cuda-toolkit` (run as root and the base conda env)
- Run `nvcc -V` to get the version of the cuDNN! (Now it should work!)

### What if `nvidia-smi` hangs with no output?

Uninstall both NVIDIA and CUDA using the built-in uninstallation scripts and install another driver.

## Screen (Do Something while I'm gone)
[Back to top](#)
| | |
|-|-|
| screen -S arman | Start a screen with name `arman`. You can detach from the screen (get out of it) by using `ctrl+a` and then pressing `d` |
| screen -r arman | Resume a screen named `arman` |
| screen killall | Kill all screens |
| screen -ls | List all running screens |
| screen -r -d 29284 | Resume a screen with ID 29284 |
## Server
[Back to top](#)
| | |
|-|-|
| apt install ubuntu-desktop | install a desktop on an Ubuntu server |

## Docker
[Back to top](#)
| | |
|-|-|
| docker ps | List all running containers with their ID and name |
| docker ps -a | List all containers with their ID and name |
| docker stop <container_id> | Stop a container with a given ID  |
| docker rm <container_id> | Remove a container with a given ID |
| docker exec -it <container_id_or_name> /bin/bash | attach to an existing container to run code interactively |
| docker attach <container_id_or_name> | Attach to a running container |
| `CTRL+P` followed by `CTRL+Q` | Detach from a running container |
| `docker run -d <image_name>:<tag>` | Run a Container in Detached Mode |
| `docker run --gpus all -it -v ~/path/to/host_folder:/out_path -p 8002:8889 --entrypoint /bin/bash lorenzopapa5/cuda11.6-python3-pytorch1.12.0:latest` | Run a docker named `cuda11.6-python3-pytorch1.12.0:latest` uploaded by a user called `lorenzopapa5` (available on Dockerhub) while giving it access to all gpus available on the host machine. This command also makes a folder called `out_path` in the docker files and maps it to the real path `/path/to/host_folder` on the host machine. Moreover, it maps the docker port `8889` to the real port `8002` on the host machine. |
| docker stop <container_id_or_name> | Stop a Running Container |
| docker start <container_id_or_name> | Start a Stopped Container |
| docker exec -it <container_id_or_name> <command> | Execute a Command in a Running Container |
| docker logs <container_id_or_name> | View Container Logs |
| docker system df | Get a summary of all Docker disk usage |
| docker system df --verbose | Get a detailed report on all Docker disk usage |

### How to install the docker on Ubuntu Linux
1. Run `sudo apt update`.
2. Install the docker using `sudo apt install -y docker.io`.
3. Start the docker: `sudo systemctl start docker`.
4. Enable the docker: `sudo systemctl enable docker`.
5. Verify Installation: `docker --version`.

### How to get a docker image from docker hub and use it
1. Download the image from docker hub: `docker pull <dockerhub_username>/<repository_name>:<tag>`.
2. To run the image interactively and get access to the bash shell, use the `-it` flags: `docker run -it <dockerhub_username>/<repository_name>:<tag> /bin/bash`.
3. When the container starts, you’ll be dropped into its bash shell. You can now run any commands interactively inside the container.
4. When you're done, type `exit` to  leave the container. This will also stop the container unless you run it with `--rm` to remove it automatically.

### How to push your own docker container to docker hub
1. Run `docker ps` to get its ID
2. Use the `docker commit` command to create a new image. Replace <container_id> with the ID or name of your running container and <image_name> with the desired name for your new image. Run `docker commit <container_id> <image_name>:<tag>` (Choose an image name and a tag, .e.g, `docker commit 00784f83a867 torch112cu116:latest`)
3. Run `docker images` to make sure the image has been created.
4. (Optional) Save the Image: If you want to back up or transfer the image to another system, you can save it as a tar file by running `docker save -o <path_to_file>.tar <image_name>:<tag>` (e.g., `docker save -o my_new_image.tar my_new_image:latest`). Then, you can load it using `docker load -i <path_to_file>.tar`.
5. Run `docker login` to log into the docker hub.
6. Docker Hub requires images to be tagged with your Docker Hub username and repository name. To do this, run `docker tag <image_name>:<tag> <dockerhub_username>/<repository_name>:<tag>` (e.g., `docker tag torch112cu116:latest armanmalekzadeh/gpulinux:latest`).
7. Push the tagged image to Docker Hub by running `docker push armanmalekzadeh/gpulinux:latest`.

## Common Problems
[Back to top](#)

### `sudo apt-get update` fails

This is usually due to a corrupted `sources.list.d` file.

```
sudo mv /etc/apt/sources.list{,.bk}
sudo mkdir /etc/apt/sources.list.d
sudo cp /usr/share/doc/apt/examples/sources.list /etc/apt/sources.list
sudo apt-get update
```
