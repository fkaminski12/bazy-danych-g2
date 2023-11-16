
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
