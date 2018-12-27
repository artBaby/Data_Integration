##Describing of our environment

Connection to H2 Database:

![alt text](https://pp.userapi.com/c848520/v848520025/eac27/ptUNAdXBirc.jpg)


Objects:

![alt text](https://pp.userapi.com/c848520/v848520025/eac3e/qVXcRNND8vw.jpg)


Data Properties:

![alt text](https://pp.userapi.com/c848520/v848520025/eac2e/1N-BMZhiwuE.jpg)


Object Properties:

![alt text](https://pp.userapi.com/c848520/v848520025/eac45/zBaifGpJXb8.jpg)


Mapping sql queries to model:

![alt text](https://pp.userapi.com/c848520/v848520025/eac37/F2MR0_SSd7I.jpg)


DB1

create table db1.car(carid int primary key,
manufacturer varchar(255), 
model varchar(255));   
insert into db1.car (carid, manufacturer, model) values

(1, 'LADA', 'VESTA'),

(2, 'FIAT', 'ALBEA'),

(3, 'MERCEDES-BENZ', 'C63'),

(4, 'TOYOTA', 'CAMRY');

------------------------
create table db1.comfort(carid int primary key,
manufacturer varchar(255), 
model varchar(255),
comfort int);   
insert into db1.comfort (carid, manufacturer, model, comfort) values

(1, 'LADA', 'VESTA', 1),

(2, 'FIAT', 'ALBEA', 3),

(3, 'MERCEDES-BENZ', 'C63', 7),

(4, 'TOYOTA', 'CAMRY', 6);


------------------------

create table db1.sales(carid int, managerid int);   
insert into db1.sales (carid, managerid) values

(1, 55)

(2, 923)

(3, 1),

(4, 7736);


------------------------

create table db1.managers(managerid int primary key, name varchar(255));

insert into db1.managers (managerid, name) values

(55, 'Art'),

(923, 'Den'),

(1, 'Van'),

(7736, 'Man');

DB2

create table db2.vehicle(id int primary key,
manufacturer varchar(255), 
country varchar(255), 
avr_price int);
   
insert into db2.vehicle (id, manufacturer, country, avr_price) values
(111, 'VAZ', 'RUS', 1000),
(222, 'FIAT', 'ITA', 2000),
(333, 'MERCEDES-BENZ', 'DEU', 4000),
(444, 'TOYOTA', 'JPN', 3000);

------------------------
			  

create table db2.max_speed(id int , speed int);

insert into db2.max_speed(id, speed) values
(111, 150),
(222, 170),
(333, 250),
(444, 220);

------------------------

create table db2.pilots (pilotid int primary key, name VARCHAR(255), surname VARCHAR(255));

insert into db2.pilots(pilotid, name, surname) values
(101, 'Artemii', 'Bab'),
(202, 'Denis', 'Rom'),
(303, 'Slava', 'Chel');

------------------------

create table db2.races(raceid int primary key, id int, pilotid int, place int);

insert into db2.races(raceid, id, pilotid, place) values 
(456, 111, 101, 1),
(789, 333, 303, 2);


To deploy SPARQL endpoint and check results:

1. Download and unzip the archive with Tomcat [tomcat-ontop-bundle.zip](https://github.com/ontop/ontop-examples/raw/master/ekaw-tutorial-2016/tomcat-ontop-bundle.zip)
2. Start tomcat from the *bin folder* using the commands: 
	* On Mac/Linux: using the terminal run `sh startup.sh` or  `sh catalina.sh start`.
	* On Windows: click on the executable `startup.bat`.
3. Connect to Sesame Workbench at http://localhost:8080/openrdf-workbench/ .
4. You will be automatically redirected to the repositories view .

## Setting up a Quest Virtual RDF Repository using the Sesame Workbench

1. Download [this OWL ontology file](https://github.com/ontop/ontop-examples/blob/master/ekaw-tutorial-2016/session1/university-complete.ttl) .
2. Download [this mapping file](https://github.com/ontop/ontop-examples/blob/master/ekaw-tutorial-2016/session1/university-complete.obda) .

3. Click on *New repository*
  * Select *Ontop Virtual RDF Store* from the list.
  * Give an ID to your new repository (ex: Project).
  * Give optionally also a descriptive title (ex: Universities Repository).
  * Click on *Next*.

On the next page:
  * Specify path to downloaded files
  * Keep the default options.
  * Click on *Create*.


Examples of SPARQL queries:

PREFIX : <http://www.semanticweb.org/artemiy/ontologies/2018/11/untitled-ontology-8#>
PREFIX obda: <https://w3id.org/obda/vocabulary#>
PREFIX owl: <http://www.w3.org/2002/07/owl#>
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX xsd: <http://www.w3.org/2001/XMLSchema#>
PREFIX xml: <http://www.w3.org/XML/1998/namespace>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>

SELECT distinct ?n ?m WHERE
{ 
?name :Manager_Name ?n .
?p :hasManager ?name .
?p :Model ?m .
}

SELECT   ?c ?m ?sp WHERE
{ 
?c a :Car .
?c :Manufacturer ?m .
?c :Max_Speed ?sp
}

SELECT distinct  ?manuf  WHERE
{ 
?m :Manufacturer ?manuf
}

SELECT ?name WHERE
{ 

?w :Pilot_Name ?name
}

SELECT * WHERE
{ 
?id a :Car .
?id ?p ?o
}
