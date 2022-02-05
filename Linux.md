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
##### Example 1: Copy an example file from our machine to a remote machine
| Variable | Value |
| ------- | ------- |
| The IP address of the remote system | 192.168.1.30 |
| User on the remote system |	ubuntu |
| Name of the file on the local system | important.txt |
| Name that we wish to store the file as on the remote system | transferred.txt |
> scp important.txt ubuntu@192.168.1.30:/home/ubuntu/transferred.txt
##### Example 2: Copy a file from a remote computer that we're not logged into<br>
| Variable | Value |
| -------- | ------ |
| IP address of the remote system |	192.168.1.30 |
| User on the remote system | ubuntu |
| Name of the file on the remote system | documents.txt |
| Name that we wish to store the file as on our system | notes.txt |
> scp ubuntu@192.168.1.30:/home/ubuntu/document.txt notes.txt
#### Serving Files From Your Host - WEB
Python helpfully provides a lightweight and easy-to-use module called "HTTPServer". This module turns your computer into a quick and easy web server that you can use to serve your own files, where they can then be downloaded by another computing using commands such as <b>curl</b> and <b>wget</b>.<br>
<b>python3 -m  http.server</b>
##### Lab: Download the file http://MACHINE_IP:8000/.flag.txt onto the TryHackMe AttackBox
In the Attack Box terminal<br>
ssh tryhackme@MACHINE_IP<br>
password:<br>
Connection Established<br>
In the home folder of the machine make the server<br>
python3 -m http.server<br>
Server setup completed<br>
Now in the attackbox: wget http://MACHINE_IP:8000/.flag.txt<br>
The file gets download<br>
cat .flag.txt<br>
Output:THM{WGET_WEBSERVER}<br>
### Process 101
Processes are the programs that are running on your machine. They are managed by the kernel, where each process will have an ID associated with it, also known as its PID. The PID increments for the order In which the process starts. I.e. the 60th process will have a PID of 60.<br>
#### Viewing Processes
We can use the friendly <b>ps</b> command to provide a list of the running processes as our user's session and some additional information such as its status code, the session that is running it, how much usage time of the CPU it is using, and the name of the actual program or command that is being executed.<br>
![alt img](https://assets.tryhackme.com/additional/linux-fundamentals/part3/ps1.png)<br>
Note how in the screenshot above, the second process ps has a PID of 204, and then in the command below it, this is then incremented to 205.
<br><br>
To see the processes run by other users and those that don't run from a session (i.e. system processes), we need to provide <b>aux</b> to the <b>ps</b> command like so: <b>ps aux</b><br>
![alt img](https://assets.tryhackme.com/additional/linux-fundamentals/part3/ps2.png)<br>
Note we can see a total of 5 processes -- note how we now have "root"  and "cmnatic"
<br><br>
Another very useful command is the top command; top gives you real-time statistics about the processes running on your system instead of a one-time view. These statistics will refresh every 10 seconds, but will also refresh when you use the arrow keys to browse the various rows. Another great command to gain insight into your system is via the <b>top</b> command<br>
![alt img](https://assets.tryhackme.com/additional/linux-fundamentals/part3/top1.png)
#### Managing Processes
You can send signals that terminate processes; there are a variety of types of signals that correlate to exactly how "cleanly" the process is dealt with by the kernel. To kill a command, we can use the appropriately named <b>kill</b> command and the associated PID that we wish to kill. i.e., to kill PID 1337, we'd use <b>kill 1337</b>.
<br>
Below are some of the signals that we can send to a process when it is killed:
<br>
SIGTERM - Kill the process, but allow it to do some cleanup tasks beforehand
SIGKILL - Kill the process - doesn't do any cleanup after the fact
SIGSTOP - Stop/suspend a process
#### How do Processes Start
Let's start off by talking about namespaces. The Operating System (OS) uses namespaces to ultimately split up the resources available on the computer to (such as CPU, RAM and priority) processes. Think of it as splitting your computer up into slices -- similar to a cake. Processes within that slice will have access to a certain amount of computing power, however, it will be a small portion of what is actually available to every process overall.
<br>
Namespaces are great for security as it is a way of isolating processes from another -- only those that are in the same namespace will be able to see each other.
<br>
We previously talked about how PID works, and this is where it comes into play. The process with an ID of 0 is a process that is started when the system boots. This process is the system's init on Ubuntu, such as <b>systemd</b>, which is used to provide a way of managing a user's processes and sits in between the operating system and the user. 
<br>
For example, once a system boots and it initialises, systemd is one of the first processes that are started. Any program or piece of software that we want to start will start as what's known as a child process of systemd. This means that it is controlled by systemd, but will run as its own process (although sharing the resources from systemd) to make it easier for us to identify and the likes.<br>
![alt img](https://assets.tryhackme.com/additional/linux-fundamentals/part3/process1.png)
#### Getting Processes/Services to Start on Boot
Some applications can be started on the boot of the system that we own. For example, web servers, database servers or file transfer servers. This software is often critical and is often told to start during the boot-up of the system by administrators.
<br><br>
In this example, we're going to be telling the apache web server to be starting apache manually and then telling the system to launch apache2 on boot.
<br><br>
Enter the use of systemctl -- this command allows us to interact with the systemd process/daemon. Continuing on with our example, systemctl is an easy to use command that takes the following formatting: systemctl [option] [service]
<br><br>
For example, to tell apache to start up, we'll use systemctl start apache2. Seems simple enough, right? Same with if we wanted to stop apache, we'd just replace the [option] with stop (instead of start like we provided)
<br><br>
We can do four options with systemctl:
<br>
Start
Stop
Enable
Disable
#### An Introduction to Backgrounding and Foregrounding in Linux
Processes can run in two states: In the background and in the foreground. For example, commands that you run in your terminal such as "echo" or things of that sort will run in the foreground of your terminal as it is the only command provided that hasn't been told to run in the background. "Echo" is a great example as the output of echo will return to you in the foreground, but wouldn't in the background - take the screenshot below, for example.<br>
![alt img](https://assets.tryhackme.com/additional/linux-fundamentals/part3/bg1.png)<br>
Here we're running <b>echo "Hi THM"</b> , where we expect the output to be returned to us like it is at the start. But after adding the <b>&</b> operator to the command, we're instead just given the ID of the echo process rather than the actual output -- as it is running in the background.<br>
<br><br>
This is great for commands such as copying files because it means that we can run the command in the background and continue on with whatever further commands we wish to execute (without having to wait for the file copy to finish first)
<br><br>
We can do the exact same when executing things like scripts -- rather than relying on the & operator, we can use Ctrl + Z on our keyboard to background a process. It is also an effective way of "pausing" the execution of a script or command like in the example below:<br>
![alt img](https://assets.tryhackme.com/additional/linux-fundamentals/part3/bg2.png)<br>
This script will keep on repeating "This will keep on looping until I stop!" until I stop or suspend the process. By using Ctrl + Z (as indicated by T^Z). Now our terminal is no longer filled up with messages -- until we foreground it, which we will discuss below.
#### Foregrounding a process
Now that we have a process running in the background, for example, our script "background.sh" which can be confirmed by using the ps auxcommand, we can back-pedal and bring this process back to the foreground to interact with.<br>
![alt img](https://assets.tryhackme.com/additional/linux-fundamentals/part3/bg3.png)<br>
With our process backgrounded using either Ctrl + Z or the & operator, we can use fg to bring this back to focus like below, where we can see the fg command is being used to bring the background process back into use on the terminal, where the output of the script is now returned to us.<br>
![alt img](https://assets.tryhackme.com/additional/linux-fundamentals/part3/bg4.png)<br>
![alt img](https://assets.tryhackme.com/additional/linux-fundamentals/part3/bg5.png)
