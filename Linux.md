#### Basic commands
echo<br>
whoami<br>
ls<br>
cd<br>
cat<br>
pwd<br>
find -name filename<br>
wc -l filename<br>
grep "word" filename
#### Operators
'&' : This operator allows you to run commands in the background of your terminal.<br>
'&&'<br>
'>'<br>
'>>'
#### SSH Syntax
ssh username@IP_Address<br>
#### List
ls -a : -a is short for --all. This shows hidden folders as well.<br>
ls --help<br>
man ls
#### Advance Commands
| Command |	Full | Name	Purpose |
| ------- | ------- | -------- |
| touch	| touch	| Create file |
| mkdir | make directory | Create a folder |
| cp | copy | Copy a file or folder |
| mv | move	| Move a file or folder |
| rm | remove | Remove a file or folder |
| file | file | Determine the type of a file |
#### Permissions
ls -lh
#### Text Editor
nano filename<br>
VIM<br>
<b>Lab:</b><br>
ssh tryhackme@IP_Address<br>
passsword:<br>
cd /home<br>
ls<br>
nano task3<br>
<b>Result:</b> THM{TEXT_EDITOR}
#### Downloading Files
Example: <b>wget</b> https://assets.tryhackme.com/additional/linux-fundamentals/part3/myfile.txt
#### Transferring Files From Your Host - SCP (SSH)
<b>Example 1:</b> Copy an example file from our machine to a remote machine
| Variable | Value |
| ------- | ------- |
| The IP address of the remote system | 192.168.1.30 |
| User on the remote system |	ubuntu |
| Name of the file on the local system | important.txt |
| Name that we wish to store the file as on the remote system | transferred.txt |
scp important.txt ubuntu@192.168.1.30:/home/ubuntu/transferred.txt<br><br>
<b>Example 2:</b> Copy a file from a remote computer that we're not logged into<br>
| Variable | Value |
| -------- | ------ |
| IP address of the remote system |	192.168.1.30 |
| User on the remote system | ubuntu |
| Name of the file on the remote system | documents.txt |
| Name that we wish to store the file as on our system | notes.txt |
scp ubuntu@192.168.1.30:/home/ubuntu/document.txt notes.txt<br>
