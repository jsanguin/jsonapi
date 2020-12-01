This is a very simple example on how to use JSON functions in SQL to get a JSON structure from data in a table.

My table in this case has the following structure:

QCUSTCDT
--  Generate SQL 
--  Version:                   	V7R4M0 190621 
--  Generated on:              	20-12-01 23:20:50 
--  Relational Database:       	PUB400 
--  Standards Option:          	Db2 for i 
CREATE TABLE JSANGUIN1.QCUSTCDT ( 
--  SQL150B   10   REUSEDLT(*NO) in table QCUSTCDT in JSANGUIN1 ignored. 
	CUSNUM NUMERIC(6, 0) NOT NULL DEFAULT 0 , 
	LSTNAM CHAR(8) CCSID 37 NOT NULL DEFAULT '' , 
	INIT CHAR(3) CCSID 37 NOT NULL DEFAULT '' , 
	STREET CHAR(13) CCSID 37 NOT NULL DEFAULT '' , 
	CITY CHAR(6) CCSID 37 NOT NULL DEFAULT '' , 
	STATE CHAR(2) CCSID 37 NOT NULL DEFAULT '' , 
	ZIPCOD NUMERIC(5, 0) NOT NULL DEFAULT 0 , 
	CDTLMT NUMERIC(4, 0) NOT NULL DEFAULT 0 , 
	CHGCOD NUMERIC(1, 0) NOT NULL DEFAULT 0 , 
	BALDUE NUMERIC(6, 2) NOT NULL DEFAULT 0 , 
	CDTDUE NUMERIC(6, 2) NOT NULL DEFAULT 0 )   
	  
	RCDFMT CUSREC     ; 
  
LABEL ON TABLE JSANGUIN1.QCUSTCDT 
	IS 'PC Support Customer File' ; 
  
LABEL ON COLUMN JSANGUIN1.QCUSTCDT 
( CUSNUM TEXT IS 'Customer number field' , 
	LSTNAM TEXT IS 'Last name field' , 
	INIT TEXT IS 'First and middle initial field' , 
	STREET TEXT IS 'Street address field' , 
	CITY TEXT IS 'City field' , 
	STATE TEXT IS 'State abbreviation field' , 
	ZIPCOD TEXT IS 'Zip code field' , 
	CDTLMT TEXT IS 'Credit limit field' , 
	CHGCOD TEXT IS 'Charge code field' , 
	BALDUE TEXT IS 'Balance due field' , 
	CDTDUE TEXT IS 'Credit due field' ) ; 
  
GRANT ALTER , DELETE , INDEX , INSERT , REFERENCES , SELECT , UPDATE   
ON JSANGUIN1.QCUSTCDT TO JSANGUIN WITH GRANT OPTION ; 
  
GRANT SELECT   
ON JSANGUIN1.QCUSTCDT TO PUBLIC ; 
  
GRANT ALTER , DELETE , INDEX , INSERT , REFERENCES , SELECT , UPDATE   
ON JSANGUIN1.QCUSTCDT TO QSECOFR WITH GRANT OPTION ; 
  

data in the table has more than 1 row, the API uses the CUSNUM to fetch the resulting JSON structure

Forced this to have an embedded JSON structure for the address.

{"Customer_Id":938472,"Last_Name":"Henning ","Address":{"Street":"4859 Elm Ave ","City":"Dallas","State":"TX","ZipCode":75217}}   


Steps to follow to test :

Compile JSONAPI as Module
Create Service Program from this module

Use RPG004 to test, you will need to debug to see the value of the resulting field
Compile RPG004 as Module, consider here *source for the debug
Compile the module as PGM, biding to the service prgram JSONAPI

Test
                                                  