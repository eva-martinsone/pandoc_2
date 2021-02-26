---
title: "Datu kārtošana"
author: [Eva Mārtiņsone]
date: "26.02.2021."
subject: "Programmēšana"
keywords: [Markdown, Example]
subtitle: "Referāts"
lang: "en"
titlepage: true,
titlepage-rule-color: "360049"
titlepage-background: "evasfons.pdf"
...

# Darba mērķis
Veikt datu kārtošanu pēc vairākiem atlases kritēriem. Iegūtās datu kopas nosūtītas atbildīgajiem uz e-pastiem

# Izmantotie moduļi
pandas.DataFrame - izmantots ar mērķi veikt darbības ar datiem tabulā gan pēc rindu, gan pēc kolonnu etiķetēm
smtplib - izmatots ar mērķi izveidot e-pastu izsūtīšanas sesiju
MIMETex - izmantots ar mērķi sagatavot e-pastu un tā pielikumu

# CSV faila imports
pandas.read_csv - nodrošina csv faila nolasīšanu, kurā ir atdalītas vērtības
r - nodrošina nepabeigtu vērtību atdalīšanu
(fails) - importētā faila atrašanās vieta 

Izpildītais kods:
```java
saraksts = pd.read_csv (r'C:\Users\Lietotajs\Desktop\ievades_dati.csv')
print(saraksts)
```

# Datu indeksēšana
## Izmantotās funkcijas:
.index - nodrošina katras tabulas kolonas vai rindas indeksēšanu kā atevišķu vienumu
.loc - nodrošina indeksēto tabulas kolonu vai rindu vienumu atlasi

## Datu indeksēšana pēc tabulas kolonas 'Organizācija'
Nodrošina visu organizāciju pieteikumu indeksēšanu
Izpildītais kods:
```java
pak_kolonas = saraksts.set_index('Organizacija')'
print(pak_kolonas)
```

## Datu grupēšana no indeksētās kolonas 'Organizācija'
Nodrošina konkrētu organizāciju pieteikumu atlasi
Izpildītais kods:
```java
iestade = pak_kolonas.loc[['Labklajibas departaments', 'Rigas Socialais dienests', 'Rigas pasvaldibas policija', 'Socialais dienests']]
print(iestade)
print(pak_kolonas)
```

## Atlasīto datu tālākā indeksēšana pēc kolonas 'Darba grupai'
Nodrošina konkrētu orgaizāciju pieteikumu indeksēšanu
Izpildītais kods:
```java
pak_vaditaji = iestade.set_index('Darba grupai')
print(pak_vaditaj)
```

## Datu grupēšana pēc indeksētajiem datiem, kas nepieciešams e-pastu saturam
Nodrošina konkrētu orgaizāciju pieteikumu grupēšanu pēc to atbildīgajiem
Izpildītais kods:
```java
Normunds = pak_vaditaji.loc[['Datu bazu un sistemu nodala']]
print('DBSN pieteikumi', Normunds)

Mihails = pak_vaditaji.loc[['Tehnisko resursu uzturesanas sektors']]
print('TRU sektota pieteikumi', Mihails)

Jorens = pak_vaditaji.loc[['Fiziskas drosibas un integreto sistemu sektors']]
print('FDIS sektota pieteikumi', Jorens)
```

# Epatsu izsūtīšana
Par katru datu kopu, kas iegūta iepriekš aprakstīto datu indeksēšanā un grupēšanā pēc organizāciju pieteikumiem un atbildīgajiem, tiek sagatavots e-pasts pēc turpmāk esošā parauga

## Nepieciešamās komponentes
```java
import smtplib
from email.mime.text import MIMEText
import email
```

## Pieslēguma izveide
```java
server=smtplib.SMTP('smtp.gmail.com',587)
server.starttls()
```

## Izsūtītāja e-pasta rekvizīti
```java
email="mmmartinsone@gmail.com"
PASSWORD="parole"
```

## E-pasta saturs
```java
server.login(email,PASSWORD)
masaage=MIMEText('Kāpēc nav izpildīti uzdevumi', str == Normunds)
masaage["From"]=email
masaage["To"]=email
masaage["Subject"]="Neizpildītie uzdevumi"
```

## E-pasta izsūtīšanu
```java
server.sendmail(email,email,masaage.as_string())
print('e-pasts nosūtīts')
```
