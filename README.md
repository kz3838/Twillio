# Twillio
from bs4 import BeautifulSoup
import requests

url = 'https://postmates.com/los-angeles'
webpage = requests.get(url)
soup = BeautifulSoup(webpage.text, 'html.parser')
from twilio.rest import TwilioClient

account_sid = 'xxxxxxxxxxxxxxxxxxxxxxxx'
auth_token = 'xxxxxxxxxxxxxxxxxxxxxxxxx'
twilio_phone_number = '+xxxxxxxxxx'
my_phone_number = '+xxxxxxxx'

webpage = requests.get(url)
soup = BeautifulSoup(webpage.text, 'html.parser')

free_food = [s for s in soup.body.stripped_strings if 'free' in s.lower()]

if free_food:
	body = 'Free Postmates!\n\n' + '\n'.join(free_food)
	client = twilioClient(account_sid, auth_token)
	client.messages.create(
		body=body,
		to=my_phone_number,
		from_=twilio_phone_number
		) 
