#!/usr/bin/python
import calendar
import subprocess
import time
import xml.etree.ElementTree as ET

import requests

LOGIN_URL = "your login url"
LOGIN_MODE = "your login mode"
USERNAME = "Your username here"
PASSWORD = "Your password here"
TIME = calendar.timegm(time.gmtime())
PRODUCT_TYPE = "0"

LIVE_URL = "your live url"
LIVE_MODE = "your live mode"


def login():
    login_data = {
        "mode": LOGIN_MODE,
        "username": USERNAME,
        "password": PASSWORD,
        "a": TIME,
        "producttype": PRODUCT_TYPE
    }

    r = requests.post(url=LOGIN_URL, data=login_data)

    row = r.text

    root = ET.fromstring(row)

    res = root.find("message").text

    if res == "You are signed in as {username}":
        print("on Login")
        return True
    else:
        return False


def live():
    url = [LIVE_URL, "?mode=", LIVE_MODE, "&username=", USERNAME, "&a=", str(TIME), "&producttype=", PRODUCT_TYPE]

    s = "".join(url)

    try:
        r = requests.get(url=s, timeout=1)
    except:
        return False

    row = r.text
    root = ET.fromstring(row)

    res = root.find("ack").text

    if res == "ack":
        print("On Live")
        return True
    else:
        return False


def check_wifi():
    command = ['nmcli', '-t', '-f', 'name,device', 'connection', 'show', '--active']

    out = subprocess.Popen(command,
                           stdout=subprocess.PIPE,
                           stderr=subprocess.PIPE)
    stdout, stderr = out.communicate()
    if "Sophos Wifi SSID" in str(stdout):
        return True
    else:
        return False


if __name__ == '__main__':
    if check_wifi():
        if not live():
            login()
