import requests
import json
import xml.etree.ElementTree as ET
from requests.auth import HTTPBasicAuth
import getpass
from bs4 import BeautifulSoup as soup
import lxml


#I debug with print statements XD
#Global variables
file_path="token.json"
jps_username = input("What is your username?: ")
jps_password = getpass.getpass()
jps_url="https://yourinstance.jamfcloud.com"


#Request token
def requestToken():
    api_endpoint="%s/api/v1/auth/token" % jps_url
    headers = {"accept": "application/json"}
    request = requests.post(api_endpoint, headers=headers, auth=HTTPBasicAuth(jps_username, jps_password))
    result = request.text
    global token1
    token1 = request.json()['token']
	

#Get Serial Number
def get_serialnumber():
    # Serial number to test with (copy and paste):
    global serial_number
    serial_number = input("What is the serial number?: ")
    url = (f"https://yourinstance.jamfcloud.com/JSSResource/mobiledevicehistory/serialnumber/{serial_number}")
    headers = {"Authorization": "Bearer " + token1 }
    global response
    response = requests.get(url, headers=headers)
    #print(response.text)


#Get id from xml data and strip tags
def get_id():
    variabul=soup(response.text,'lxml')
    val=str(variabul.findAll('id')[0])
    val = val.strip("</>id")
    return val


#Get my_app login and password, using mobile device id
def get_my_app():
    url = (f"https://yourinstance.jamfcloud.com/api/v2/mobile-devices/{id_string}/detail")
    headers = {"Authorization": "Bearer " + token1 }
    response = requests.get(url, headers=headers)
    obj = response.json()
    my_app_login = obj["extensionAttributes"][7]["value"]
    my_app_pass = obj["extensionAttributes"][8]["value"]
    #print(type(obj["extensionAttributes"][8]["value"]))
    my_app_login = my_app_login[0]
    my_app_pass = my_app_pass[0]
    print(f"The my_app login for sn# {serial_number} is: {my_app_login}")
    print(f"The my_app password is: {my_app_pass}")



requestToken()
get_serialnumber()
id_string = (get_id())
get_my_app()
input("Press enter to exit;")
