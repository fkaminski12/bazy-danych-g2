# zad1
```sql
 create table postac (
    -> id_postaci int auto_increment primary key,
    -> nazwa varchar(40),
    -> rodzaj enum('wiking','ptak','kobieta'),
    -> data_ur date,
    -> wiek int unsigned);

  ## zad2

 create table walizka( id_ int primary key auto_increment, pojemnosc int unsigned, kolor enum('rozowy','czerwony','teczowy','zloty'), id_wlasciciela int, foreign key (id_wlasciciela) references postac(id_postaci) on delete cascade);

