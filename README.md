# SophosAutoLogin
### Sophos WiFi access point auto login with Linux Cronjob

Our office's wifi networks vendor is Sophos. So every time we connect, we need to do login in a web address and keep that browser tab alive to get internet connection. 

So I decided to create a script to automate this task and wrote that script in python. Then I added a cronjob to execute this python script in my Linux PC every 3 mins.
This script will check current WiFi SSID and if it is your office network it will try to log in and keep the connection alive.

## Installation

clone this repo

```bash
git clone https://github.com/z3r0c00l-2k/SophosAutoLogin.git 
```

Install dependencies

```bash
pip install -r requirements.txt
```

Add your connection config to sophos_login.py, find and edit these lines

```python
LOGIN_URL = "your login url"
LOGIN_MODE = "your login mode"
USERNAME = "Your username here"
PASSWORD = "Your password here"

....

LIVE_URL = "your live url"
LIVE_MODE = "your live mode"

....

if "Your Sophos Wifi SSID" in str(stdout):
    return True
else:
    return False
```

After all these done move the script to root directory

```bash
sudo cp sophos_login.py /usr/bin/sophos_login
```

Make it executable

```bash
sudo chmod +x /usr/bin/sophos_login
```

finally create a crone job. run this command (You can leave EDITOR flag if want Vim as text editor)

```bash
sudo EDITOR=nano crontab -e    
```

then add the following line to the file

```
*/3 * * * * /usr/bin/sophos_login
```

Reboot the system and you are done.... 😎😎😎