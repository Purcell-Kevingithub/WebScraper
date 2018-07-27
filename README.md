# Web-Scraper
*Scrapes the weatherchannel for 10 day forecast

from bs4 import BeautifulSoup
import requests
import csv

Instantiate variable to access webpage and parser to seperate HTML

source = requests.get("https://weather.com/weather/tenday/l/USNJ0524:1:US").text
soup = BeautifulSoup(source, 'lxml')

Open csv file to store weather details
csv_file = open('weatherchannel_scrape.csv', 'w')
csv_writer = csv.writer(csv_file)
csv_writer.writerow(['day', 'date', 'description', 'temp'])

Loop over parsed HTML to find day, date, description, and temperature
for tr in soup.find_all('tr', class_='clickable closed'):

    day = tr.find('span', class_='date-time').text
    print(day)

    date = tr.find('span', class_='day-detail clearfix').text
    print(date)

    description = tr.find('td', class_='description').span.text
    print(description)

    temp = tr.find('td', class_='temp').text
    print(temp)

    print()

    csv_writer.writerow([day, date, description, temp])

close file
csv_file.close()
