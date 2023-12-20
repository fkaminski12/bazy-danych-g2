# Zadania lab04 
### Zadanie 1

```sql
Create table postac (
id_postaci int NOT NULL AUTO_INCREMENT Primary Key,
nazwa varchar(40),
rodzaj enum('wiking','ptak','kobieta'),
data_ur date,
wiek int unsigned
)
;
```
```sql
insert into postac values(default, 'Bjorn','wiking','2000-01-01',300);
insert into postac values(default, 'Drozd','Ptak','2010-01-01',10);
insert into postac values(default, 'Tesciowa','kobieta','1000-01-01',2000);
```
```sql
Update postac
set wiek=88
where id_postaci=3;
```

### Zadanie 2
```sql
Create table walizka(
id_walizka int not null AUTO_INCREMENT Primary key,
pojemnosc int unsigned,
kolor enum('różowy','czerwony','tęczowy','żółty'),
id_wlasciciela int,
Foreign key(id_wlasciciela) references postac(id_postaci) on delete cascade
)
;
```
### zad3
```sql
create table izba(
adres_budynku varchar(50) not null,
nazwa_izby varchar(50) not null,
metraz mediumint unsigned not null,
wlasciciel int,
foreign key (wlasciciel)
references postac(id_postaci) on delete set null
);
```

### zad4
```sql
drop table izba;
select * from izba;
alter table izba add column
kolor varchar(30) default 'czarny'
after metraz;
describe izba;
insert into izba values 
('tramwaje 997','spizarnia',10,default,1);
select * from izba;
#dodac klucz glowny do abeli izba
alter table izba add
 primary key (adres_budynku,nazwa_izby);
```
### zad 5
```sql
create table przetwory(
id_przeworu int primary key ,
rok_produkcji smallint default '1654',
id_wykonawcy int,
zawartosc varchar(25),
dodatek varchar(30) default 'papryczka chilli',
id_konsumenta int,
foreign key (id_konsumenta) references postac(id_postaci),
foreign key (id_wykonawcy) references postac(id_postaci)
);
 
select * from przetwory;
insert into przetwory values 
(1,default,1,'bigos',default,1);
```
### zad6
```sql
insert into postac values 
(4,'lukasz','wiking','1700-11-09',323);
insert into postac values 
(5,'szymon','wiking','1700-11-09',323);
insert into postac values 
(6,'marek','wiking','1700-11-09',323);
insert into postac values 
(7,'Adrian','wiking','1700-11-09',323);
insert into postac values 
(8,'Thor','wiking','1700-11-09',323);
create table statek(
nazwa_statku varchar(50) primary key,
rodzaj_statku enum ('duży','sredni','maly') DEFAULT NULL,
data_wodowania date,
max_ladownosc int check (max_ladownosc > 0)
);
show create table postac;
insert into statek values ('czarnaperla',default,'1700-12-31',57
);
insert into statek values ('perlaexport',default,'1767-07-12',57
);
alter table postac add column
funkcja varchar(45);
update postac set funkcja='kapitan' where id_postaci=1
```
# lab 05
```sql
delete from postac
where nazwa<>'Bjorn'
and rodzaj='wiking'
order by data_ur asc limit 2;
alter table postac change
id_postaci int;
alter table postac change
id_postaci id_postaci int;
alter table postac modify
id_postaci int;
alter table izba
drop foreign key izba_ibfk_1;
alter table walizka
drop foreign key walizka_ibfk_1;
alter table przetwory
drop foreign key przetwory_ibfk_1;
alter table statek
drop foreign key statek_ibfk_1;
alter table postac change
id_postaci id_postaci int;
alter table postac
drop foreign key postac_ibfk_1;
show create table postac;
alter table postac change
id_postaci id_postaci int;
alter table postac modify
id_postaci int;
alter table przetwory
drop foreign key przetwory_ibfk_2;
alter table postac modify
id_postaci int;
alter table postac 
add column pesel varchar(11) first;
desc postac;
select * from postac;
update postac 
set pesel ='67390650623' + id_postaci;
alter table postac add primary key(pesel);
alter table postac modify rodzaj enum('wiking','ptak','kobieta','syrena');
select * from postac;
insert into postac values
(67390650623,'9','gertruda nieszczera','syrena','1700-11-09',345,null);
select nazwa from postac 
where nazwa like 'a%';

# select nazwa from postac 
# where nazwa regexp '^[a-f]';
update postac set statek ='czarnaperla'
where nazwa like '%a%';
select data_wodowania between '1600-01-01'
and  '2000-12-31';
update statek set max_ladownosc=max_ladownosc * 0.7
where year(data_wodowania) between 1600 and 2000;
alter table postac add check(wiek < 1000);
update postac set wiek=2000 where id_postaci=1;
select * from postac;
alter table postac modify 
rodzaj enum('wiking','ptak','kobieta','syrena','waz');
insert into postac values(
'14356789543','11','loko','waz','1600-11-09',460,null);
create table marynarz like postac;
create table marynarz2 as select * from postac 
where statek is not null;

update postac set statek=null;
describe marynarz;
alter table marynarz add column
(statek varchar(30) null );

alter table postac delete id_postaci='Adrian';
#funkcje argumentujace
# avg, sum, count , min , max
#zad 1 pkt 1

```
# lab6
```sql
create table infs_kaminskif.kreatura as select * from kreatura;
create table infs_kaminskif.zasob as select * from zasob;
create table infs_kaminskif.ekwipunek as select * from ekwipunek;
```
```sql
select * from zasob;
```
```sql
select * from zasob where rodzaj='jedzenie';
```
```sql
select idZasobu,ilosc from ekwipunek where idkreatury in (1,3,5)
```

# lab07
```sql
select * from kreatura where udzwig>=50 and not rodzaj='wiedzma' or rodzaj is null and udzwig>=50; 
```
```sql
select * from zasob where waga between 2 and 5;
```
```sql
select * from kreatura where nazwa like '%or%' and udzwig between 30 and 70;
```


```sql
select * from zasob where month(dataPozyskania)=7 or month(datapozyskania)=8;
```
```sql
select * from zasob where rodzaj is not null order by waga;
```
```sql
select * from kreatura where dataur is not null order by dataur limit 5;
```


```sql
select distinct rodzaj from zasob;

select rodzaj from zasob group by rodzaj;
```
```sql
select concat(nazwa,'-',rodzaj) from kreatura where rodzaj like 'wi%';
```
```sql
select waga*ilosc as waga from zasob where year(datapozyskania) between 2000 and 20007 ;
```


```sql
select nazwa,waga*0.7 as netto,waga*0.3 as odpadki from zasob where rodzaj='jedzenie';
```
```sql
select * from zasob where rodzaj is null;
```
```sql
select distinct rodzaj from zasob where nazwa like 'Ba%' or '%os' order by rodzaj;
```

```sql
select avg(waga) from kreatura
where rodzaj='wiking';
select rodzaj, avg(waga), count(waga),
count(*)
from kreatura group by rodzaj;
select 2023 - year(dataUr) as wiek from kreatura;
select sum(waga*ilosc) from zasob order by rodzaj;
select avg(waga) from zasob group by nazwa having sum(ilosc)>=4 and sum(waga*ilosc)>10;
SELECT rodzaj, COUNT(DISTINCT nazwa) AS liczbanazw FROM zasob GROUP BY rodzaj HAVING min(liczbanazw) > 1;
select k.nazwa,e.idZasobu,z.nazwa from kreatura k inner join ekwipunek e on k.idKreatury=e.idKreatury;
select k.nazwa,e.idZasobu,z.nazwa from kreatura k inner join ekwipunek e on k.idKreatury=e.idKreatury inner join zasob z on
z.idZasobu=e.idZasobu;
select idKreatury from kreatura
where idKreatury not in 
(select distinct idKreatury from ekwipunek
where idKreatury is not null);
select k.nazwa, z.nazwa from kreatura k natural join ekwipunek e natural join zasob z where k.rodzaj='wiking' and year(dataur) between 1670 and 1679;
select k.nazwa from kreatura k inner join ekwipunek e on k.idkreatury=e.idkreatury inner join zasob z on e.idZasobu=z.idzasobu where z.rodzaj='jedzenie' order by year(now())-year(dataur) limit 5;
select concat(k1.nazwa,' - ',k2.nazwa)
from kreatura k1
inner join kreatura k2
where k1.idKreatury - k2.idKreatury = 5;
```
# lab08
```sql
create table kreatura as select * from wikingowie.kreatura;
create table uczestnicy as select * from wikingowie.uczestnicy;
create table etapy_wyprawy as select * from wikingowie.etapy_wyprawy;
create table sektor as select * from wikingowie.sektor;
create table wyprawa as select * from wikingowie.wyprawa;

select nazwa,id_uczestnika from kreatura k  left join uczestnicy u on u.id_uczestnika=k.idKreatury where id_uczestnika is null;

select w.nazwa,sum(e.ilosc) from wyprawa w inner join uczestnicy u on w.id_wyprawy=u.id_wyprawy 
inner join ekwipunek e on u.id_uczestnika=e.idKreatury group by w.nazwa;
select w.nazwa,count(distinct u.id_uczestnika),group_concat(k.nazwa separator ' | ') from wyprawa w 
inner join uczestnicy u on w.id_wyprawy=u.id_wyprawy 
inner join kreatura k on u.id_uczestnika=k.idKreatury
group by w.nazwa;
```

