
#zad1
```sql
use infs_kaminskif;
select * from postac;
select * from walizka;
create table izba(
adres_budynku varchar(50) not null,
nazwa_izby varchar(50) not null,
metraz mediumint unsigned not null,
wlasciciel int,
foreign key (wlasciciel)
references postac(id_postaci) on delete set null
);
```
#on delete lub on update -> restrict|set null|cascade
#zad2
```sql
drop table izba;
select * from izba;
alter table izba add column
kolor varchar(30) default 'czarny'
after metraz;
describe izba;
#zad3
insert into izba values 
('tramwaje 997','spizarnia',10,default,1);
select * from izba;
#dodac klucz glowny do abeli izba
alter table izba add
 primary key (adres_budynku,nazwa_izby);
```
#3
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
#4
```sql
select * from postac;
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
select* from postac ;
UPDATE `infs_kaminskif`.`postac` SET `funkcja` = 'kapitan' WHERE (`id_postaci` = '1');
```
zad 5
```sql
use infs_kaminskif;
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
```
zad 6
```sql
#funkcje argumentujace
# avg, sum, count , min , max
#zad 1 pkt 1
select avg(waga) from kreatwagawagaura;
use infs_kaminskif;
select avg(waga) from kreatura
where rodzaj = 'wiking';
#lub "napiechote"
select rodzaj,nazwa, avg(waga), count(waga),
count(*)
from kreatura group by rodzaj;
select 2023 - year(dataUr) as wiek from kreatura;
select sum(waga) from zasob order by rodzaj;
select avg(waga) from zasob group by nazwa having sum(ilosc)>=4 and sum(waga*ilosc)>10;
```

