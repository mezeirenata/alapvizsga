# Python anyagok
#00 - Extensions
#01 - Prímek
#02 - Bonyolult osztály
#03 - Statisztika
#04 - Legjobb függvény
#05 - Legnagyobb közös osztó (kivonásos)
#06 - Magánhangzók száma hétköznapokban
#07 - Egyéb 
#08 - Try - except függvények
#09 - Halmaz-e?
#10 - Ösvény és tócsa
#11 - Dátumok közötti eltelt napok + abs függvény
#12 - Pénzváltó + round, match - case
#13 - Eltelt idő két osztály elem között (SMS)
#14 - két soros csv kezelése (SMS)


### - 00
#Auto rename tag

### - 01
from random import randint

def main():
    szamok:list[int] = []
    for i in range(11):
        random = randint(10,99)
        szamok.append(random)
    
    for p in szamok:
        if ez_prim(p):
            print(szamok)
            print('Van prímszám a listában!')
            exit()
    print('Nincs prímszám a listában!')

def ez_prim(szam:int) -> bool:
    osztok = 0
    for i in range(1,(szam+1)):
        if szam % i == 0:
            osztok += 1
    
    if osztok >= 3:
        return False
    else:
        return True

main()
### - 02
class Tanulo:
    def __init__(self, row: str) -> None:
        adatok = row.strip().split('\t')
        self.nev = adatok[0]
        self.osztaly = str(adatok[1])
        self.matek= adatok[2]
        self.magyar= adatok[3]
        self.tori = adatok[4]
        self.info = adatok[5]
        self.angol = adatok[6]

        self.matek_lista = jegyek_listaba(self.matek)
        self.magyar_lista = jegyek_listaba(self.magyar)
        self.tori_lista = jegyek_listaba(self.tori)
        self.info_lista = jegyek_listaba(self.info)
        self.angol_lista = jegyek_listaba(self.angol)

        self.matek_atlag = round(atlag(self.matek_lista),2)
        self.magyar_atlag = round(atlag(self.magyar_lista),2)
        self.tori_atlag = round(atlag(self.tori_lista),2)
        self.info_atlag = round(atlag(self.info_lista),2)
        self.angol_atlag = round(atlag(self.angol_lista),2)

        self.matek_biz = kerekites(self.matek_atlag)
        self.magyar_biz = kerekites(self.magyar_atlag)
        self.tori_biz = kerekites(self.tori_atlag)
        self.info_biz = kerekites(self.info_atlag)
        self.angol_biz = kerekites(self.angol_atlag)

def jegyek_listaba(jegy_csoport: str) -> list:
    list = []
    for x in jegy_csoport.split(','):
        list.append(int(x))
    return list

def atlag(list:int) -> float:
    osszeg = 0
    for x in list:
        osszeg += x
    return osszeg/len(list) 

def kerekites(atlag:float) -> int:
    if atlag >= 4.5:
        return 5
    elif atlag <= 4.49  and atlag >= 3.5:
        return 4
    elif atlag <= 3.49 and atlag >= 2.5:
        return 3
    elif atlag <= 2.49 and atlag >= 2:
        return 2
    elif atlag <= 1.99:
        return 1

### - 03
def statisztika() -> dict:
    stat= {}
    for t in tanulok_listaja:
        if t.osztaly == "8A" or t.osztaly == "8B" or t.osztaly == "8C" or t.osztaly == "8D":
            if t.osztaly not in stat.keys():
                    stat[t.osztaly] = 1
            else:
                stat[t.osztaly] += 1
    return stat
### - 04
def legjobb_atlag() -> Tanulo:
    legjobb = tanulok_listaja[0]
    for t in tanulok_listaja:
        if t.osztaly == "7A":
            if t.matek_atlag > legjobb.matek_atlag:
                legjobb = t
    return legjobb
### - 05

def lnko(a,b):
    if a == b:
        return a
    elif a < b:
        return lnko(a,b-a)
    else:
        return lnko(a-b,b)

i1 = int(input('Kérem az egyik számot: '))
i2 = int(input('Kérem a második számot: '))
print('A legnagyobb közös osztó:',lnko(i1,i2))

### - 06
hetkoznapok:list[str] = ['hétfő','kedd','szerda','csütörtök','péntek']

def main():
    legtobb = 0
    legtobb_nap = ''
    for h in hetkoznapok:
        szam = maganhangzok_szama(h,hetkoznapok)
        if szam > legtobb:
            legtobb = szam
            legtobb_nap = h
    
    print(f'A legtöbb magánhangzó a {legtobb_nap}-ben van!')

def maganhangzok_szama(nap:str, list:list[str]) -> int:
    maganhangzok: list[str] = ['a','á','e','é','i','í','o','ó','ö','ő','u','ú','ü','ű']
    osszes = 0
    for x in nap:
        if x in maganhangzok:
            osszes += 1
    
    return osszes

main()

### - 07
import math
math.sqrt
math.pi
math.inf
import random
randint
random.choice(lista)
import datetime
datetime.date(ev,honap,nap)
#break
#exit()

### - 08
while:
try:
    #valami ami igaz pl. szamn = int(szam)
except:
    #írja ki hogy nem jó
#törjön ki

### - 09
from random import randint

def main():
    for i in range (1,9):
        halmaz: list[int] = []
        for n in range(5):
            halmaz.append(randint(0,9))
        if ismetlodes(halmaz):
            print(f'{i}. {halmaz} -> Halmaznak nem tekinthető!')
        else:
            print(f'{i}. Halmaznak tekinthető!')

def ismetlodes(halmaz:list[int]) -> bool:
    ertekek = {}
    if len(halmaz) == 5:
        for h in halmaz:
            if h not in ertekek.keys():
                ertekek[h] = 1
            elif h in ertekek.keys():
                ertekek[h] += 1
    for key,value in ertekek.items():
        if ertekek[key] > 1:
            return True
main()
### - 10
from random import randint
def main():
    szamsorozat: list[int] = []
    for i in range (0,25):
        n = randint(0,1)
        szamsorozat.append(n)
    print(szamsorozat)
    if szaraz_e(szamsorozat):
        print('Piroska át tud kelni száraz lábbal az ösvényen.')
    else:
        print('Piroska nem tud átkelni száraz lábbal az ösvényen.')

    

def szaraz_e(szamsorozat:list[int]) -> bool:
    pocsolyak: int = 0
    for s in szamsorozat:
        if s == 1:
            pocsolyak += 1
        elif s == 0:
            pocsolyak = 0
    
    if pocsolyak >= 4:
        return False
    else:
        return True
main()

### - 11
import datetime

def number_input(szoveg:str, maximum:int) -> int:
    szam = 0
    while szam <= 0 or szam > maximum: 
        try:
            szam = int(input(szoveg))
        except:
            print('Nem megfelelő szám')
    return szam 

def eltelt_napok(ev1,honap1,nap1,ev2,honap2,nap2) ->int:
    date1 = datetime.date(ev1,honap1,nap1)
    date2 = datetime.date(ev2,honap2,nap2)
    diff = date2-date1
    return abs(diff.days)

elso_ev = number_input("Kérem az első dátum évét:", 2024)
elso_honap = number_input("Kérem az első dátum hónapját:",12)
elso_nap = number_input("Kérem az első dátum napját:", 30)

masodik_ev= number_input("Kérem a második dátum évét:", 2024)
masodik_honap = number_input("Kérem a második dátum hónapját:",12)
masodik_nap = number_input("Kérem a második dátum napját:", 30)

print(f'{elso_ev}.{elso_honap}.{elso_nap} és {masodik_ev}.{masodik_honap}.{masodik_nap} között {eltelt_napok(elso_ev,elso_honap,elso_nap,masodik_ev,masodik_honap,masodik_nap)} nap volt!')
### - 12
eur_vagy_ft = str(input('Eurót (EUR) vagy forintot (HUF) akarsz váltani?'))
match eur_vagy_ft:
    case 'EUR':
        mennyi = int(input('Hány eurót akarsz beváltani?'))
        print(f'{mennyi} euróért {mennyi * 365} forintot kapsz.')
    case 'HUF':
        mennyi = int(input('Hány forintot akarsz beváltani?'))
        euro = round(mennyi / 365,2) 
        print(f'{mennyi} forintért {euro} eurót kapsz.')
### - 13
def longest_time_between_message_of_girlfriend():
    max_gap = 0
    prev_message = None
    for m in messages:
        if m.phone == '123456789':
            if prev_message == None:
                prev_message = m
            else:
                gap = m.total_minutes - prev_message.total_minutes
                prev_message = m
                if gap > max_gap:
                    max_gap = gap
    return max_gap
### - 14
def load_from_file(filename: str) -> None:
    file = open(filename, 'r', encoding = 'utf-8')
    # sor = file.readline()
    sorok = file.readlines()
    for i in range(0, len(sorok), 2):
        # splitted = sorok[i].strip().split(' ')
        ora, perc, phone = sorok[i].strip().split(' ')
        messages.append(Message(int(ora), int(perc), phone ,  sorok[i+1].strip()))
    file.close()
###
