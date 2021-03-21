from datetime import datetime
from pprint import pprint
import requests

def connect_to_bank():
    try:
        result = requests.get('https://bank.gov.ua/NBUStatService/v1/statdirectory/exchangenew?json')
        result = result.json()
        return result
    except:
        return ConnectionError

def write_to_file():
     data = connect_to_bank()
     cur = []
     now = datetime.now()
     for i in data:
          cur.append(f"{i['txt']} to UAH: -> {i['rate']}")
     pprint(str(now))
     pprint(cur)
     with open('Курс валюты.txt', 'wt') as file:
          file.write(str(now) + '\n' + str(cur))
     return cur

write_to_file()

print('-' * 50)
class Exchange():
    val = None
    date = None

    def __init__(self, v, d):
        if not isinstance(v, str):
            raise TypeError
        if len(v) != 3:
            raise TypeError
        if len(d) != 8:
            raise TypeError
        try:
            d = int(d)
            d = d
        except:
            raise TypeError
        self.val, self.date = v, d

currency = Exchange(input("Введите код валюты в формате USD ").upper(), input("Введите дату в формате YYYYMMDD "))

def Api_get():
    try:
        curs = requests.get(f'https://bank.gov.ua/NBUStatService/v1/statdirectory/exchange?json?\
        valcode={currency.val}&date={currency.date}')
        curs = curs.json()
        return curs
    except:
        raise ConnectionError

def result():
    cur = Api_get()
    vl = currency.val
    my_list = []
    for x in cur:
        if x['cc'] == vl:
            my_list.append(f"{x['txt']} to UAH: -> {x['rate']}")
    with open('Курс валюты по дате.txt', 'wt') as file:
        file.write(str(currency.date) + '\n' + str(my_list))
    return my_list

print(result())
