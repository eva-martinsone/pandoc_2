---
title: "Datu kartošana"
author: [Eva Martinsone]
date: "2021-02-24"
subject: "Programmēšana"
keywords: [Markdown, Example]
subtitle: "Referats"
lang: "en"
titlepage: true,
titlepage-rule-color: "360049"
titlepage-background: "evasfons.pdf"
...

# Darba mērķis
Veikt datu kārtošanu pēc vairākiem atlases kritēriem. Iegūtās datu kopas nosūtīt uz e-pastu atbildīgajiem

## Izmantotie moduļi
pandas.DataFrame modulis izmantots ar mērķi veikt darbības ar datiem tabulā gan pēc rindu, gan pēc kolonnu etiķetēm
smtplib modulis izmatots ar mērķi izsūtīt e-pastu

# CSV faila imports
pandas.read_csv - nodrošina csv faila nolasīšanu, kurā ir atdalītas vērtības
r - nodrošina nepabeigtu vērtību atdalīšanu
(faila atrašanās ceļš) - importētā faila atrašanās vieta 

Izpildītais kods:
```java
saraksts = pd.read_csv (r'C:\Users\Lietotajs\Desktop\ievades_dati.csv')
print(saraksts)
```

# Datu indeksēšana
Izmantotas funkcijas:
.index - nodrošina katras tabulas kolonas/līnijas indeksēšanu kā atevišķu vienumu
.loc - nodrošina indeksēto tabulas kolonu/līniju vienumu atlasi

## Nodrošinas datu indeksēšanu pēc kolonas 'Organizācija'
Izpildītais kods:
```java
pak_kolonas = saraksts.set_index('Organizacija')'
print(pak_kolonas)
```

## Nodrošina konkrēto vērtību atlasi pēc indeksētās kolonas 'Organizācija'
Izpildītais kods:
```java
iestade = pak_kolonas.loc[['Labklajibas departaments', 'Rigas Socialais dienests', 'Rigas pasvaldibas policija', 'Socialais dienests']]
print(iestade)
print(pak_kolonas)
```

## Nodrošina iepriekšējā punktā iegūto datu tālāko indeksēšanu to tālākai apstrādei pēc kolonas 'Darba grupa'
Izpildītais kods:
```java
pak_vaditaji = iestade.set_index('Darba grupai')
print(pak_vaditaj)
```

## Nodrošina konkrēto vērtību atlasi pēc indeksētajiem datiem, kas nepieciešams e-pastu saturam
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
Katram no iepriekšējā sadaļā iegūtajām datu kopām, kas iegūta pēc e-pasta satura tiek sagatavots e-pasta sagatave pēc turpmāk redzamajās apakšsadaļās

## Nodrošina SMTP savienojuma izveidi
```java
import smtplib
```

## Nodrošina e-pasta pamatelementus
```java
To = "mmmartinsone@gmail.com" 
Subject = "neizpilditie uzdevumi"
Text = 'tetsa e-pasts'
```

## Nodrošina e-pasta servisamgi
```java
smtp_server = "smtp.gmail.com"
port = 587
```

## Izsūtītāja e-pasta rekvizīti
```java
e_pasta_sender = "mmmartinsone@gmail.com"
e_pasta_parole = "parole" 
```

## Pieslegums e-pasta servisiem
```java
server = smtplib.SMTP('smtp.gmail.com', 587)
server.ehlo() 
server.starttls()
server.ehlo() 
server.login(e_pasta_sender, e_pasta_parole)
```

## E-pasta saturs
```java
Text = '\r\n'.join([
   'To: %s' % To,
   'From: %s' % e_pasta_sender,
   'Subject: %s' % Subject,
   '',
   Normunds
   ])
```

## Nodrošina e-pasta izsūtīšanu
```java
try:
   server.sendmail(e_pasta_sender, [To], saturs)
   print('epasts nosutits')
except:
   print('e_pasts nav nosutits') 
server.quit()
```



Lorem markdownum Letoia, et alios: figurae flectentem annis aliquid Peneosque ab
esse, obstat gravitate. Obscura atque coniuge, per de coniunx, sibi **medias
commentaque virgine** anima tamen comitemque petis, sed. In Amphion vestros
hamos ire arceor mandere spicula, in licet aliquando.