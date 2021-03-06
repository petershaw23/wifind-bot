# wifind-bot
Telegram bot using nmap to scan for devices in local wifi / LAN, running on raspberry pi

Outputs IP- and MAC addresses of found devices in telegram.


## installation:

raspian / debian etc:

`sudo apt install git`

`git clone https://github.com/petershaw23/wifind-bot/`

`sudo apt install python3-pip`

`sudo pip3 install telepot` installs telepot / telegram library for python

`sudo pip3 install python-nmap` installs nmap library for python

`sudo apt install nmap` installs nmap. not sure if needed

## usage / setup:


### edit the main script:

`cd wifind-bot`

`sudo nano wifind.py`


1. change "target_mac" in line 24 (optional)
2. change "hosts='192.168.**0**.0/24'" in line 66, if IP mask is _not_ 192.168.**0**.X. (192.168.**1**.X is also common)
   
   example: if your IP range is 192.168.1.1, change line 66 to "hosts='192.168.**1**.0/24'"

save and close the file.

____

### create a telegram bot 
create a new telegram bot by using BotFather, instructions here:

https://core.telegram.org/bots#6-botfather

note the secret bot token-key.

define the bot command "wifi" by navigating to "edit bot" -> "set commands", using BotFather.

optional: define the bot command "uptime"... shows the uptime of your host device / raspberry pi.

(sending "wifi" or "uptime" manually to the bot will work aswell)

____

### create config files
create "pibot_token.py" and "IDList.py" in same directory as wifind.py:


create token config file:

`sudo nano pibot_token.py`


content:

`token = "xxxx"` insert telegram bot token-key here

save and close the file.

create ID list config file:

`sudo nano IDList.py`

content:

`IDList = [xxxxxx, xxxxxx, ...]` insert telegram IDs (should be a number like 123456789), that are allowed to use the bot, here. multiple IDs separated by commas. IDs not found in the list are blocked from using the bot.

(how to find your telegram ID: https://www.alphr.com/telegram-find-user-id/, or start the bot without entering any vaild IDs, then read the python output after sending a message to the bot. the python output will show your telegram ID)

save and close the file.

____

### run the script

`sudo python3 wifind.py` starts the bot with _root_ privileges, without root privileges nmap cannot find MAC addresses!

## using the bot

type command, or use pre-defined pop-up-commands (defined via BotFather -> edit bot -> set commands)

`/wifi`  scan wifi / LAN and send all found devices as a list

`/uptime`  show device / raspberry pi uptime in days:hours:minutes format

![image](https://user-images.githubusercontent.com/44604841/119889914-76131280-bf37-11eb-9a57-cbf3acd40d62.png)
