# Twillio
from bs4 import BeautifulSoup
import requests

url = 'https://postmates.com/los-angeles'
webpage = requests.get(url)
soup = BeautifulSoup(webpage.text, 'html.parser')
from twilio.rest import TwilioClient

account_sid = 'ACeedbb0e2ed746bef196d6a56f3a3464e'
auth_token = 'b2ae7256c8c4336f09a96d64b807d765'
twilio_phone_number = '+19712647006'
my_phone_number = '+19715335857'

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
