# Highlight_VACCINE_DATA_SQL
This project Shows Emphasizing important information: Highlighting can be used to emphasize important information in a text, Table This can make it easier for readers to scan a text and find the most important Filtered Information.

DAX CODE USED TO HIGHLIGHT:
bar to highlight new = 
var _selectedmonths =
           VALUES( months[month name])
var monthtohighlight =
            SELECTEDVALUE(EASTWESTSOUTHBACKUP[month name])
var filtered = 
             ISFILTERED(months[month name])
return

SWITCH (TRUE, NOT(filtered) ,"Grey", monthtohighlight IN _selectedmonths && filtered,"Yellow","Grey")


**SQL SOURCE: **

CREATE TABLE VaccineData(
VaccineID INT PRIMARY KEY ,
Vaccine VARCHAR(255) NOT NULL );
INSERT INTO VaccineData
values
('1','Covaxin'),
('2','Covisheild'),
('3','Fizer'),
('4','Corbevax'),
('5', 'ZyCoV-D'),
('6','Vaxzevria');
select * from VaccineData;


CREATE TABLE NORTH_INDIA(
VaccineID INT ,
NAME VARCHAR(255) NOT NULL,
Dose INT,
Hospital_Name VARCHAR(255) NOT NULL);
INSERT INTO NORTH_INDIA
VALUES
('2','Dilbag Singh','1','Leela Hospital'),
('6','Gulmohar Pratap','1','Leela Hospital'),
('5','Preetam Kumar','2','Moon Hospital'),
('5','Tamanna L','2','Moon Hospital'),
('1','Afreen Patel','1','Lakeview Hospital'),
('1','Milkha Singh','2','Lakeview Hospital'),
('3','Helen Khan','1','Leela Hospital'),
('4','Celina K','1','City Hospital'),
('6','Naira R','2','River Hospital'),
('2','Bagga','3','Jatt Hospital');
SELECT*FROM NORTH_INDIA;

SELECT NORTH_INDIA.NAME, NORTH_INDIA.Hospital_Name, NORTH_INDIA.Dose,NORTH_INDIA.VaccineID,VaccineData.Vaccine
FROM VaccineData
INNER JOIN NORTH_INDIA ON VaccineData.VaccineID=NORTH_INDIA.VaccineID;


CREATE TABLE SOUTH_INDIA(
VaccineID INT ,
NAME VARCHAR(255) NOT NULL,
Dose INT,
Hospital_Name VARCHAR(255) NOT NULL,
Region VARCHAR(255) NOT NULL,
DATE DATETIME);
INSERT INTO SOUTH_INDIA
VALUES
('1','Amit B','2','Jeevan Hospital','SouthIndia','01/01/2021'),
('4','Vinay K','2','KLE Hospital','SouthIndia','02/03/2021'),
('2','Sandesh M','1','KLE Hospital','SouthIndia','01/12/2021'),
('6','Anish D','1','Lakeview Hospital','SouthIndia','12/12/2021'),
('3','Pavan D','2','Civil Hospital','SouthIndia','1/05/2021'),
('3','Pratik K','1','Bison Hospital','SouthIndia','1/06/2021'),
('1','Silvester R','2','Bison Hospital','SouthIndia','1/06/2021'),
('5','Winston K','1','City Hospital','SouthIndia','2/06/2021'),
('5','Rahul M','2','Military Hospital','SouthIndia','2/05/2021'),
('2','Shivani P','1','Club Hospital','SouthIndia','1/05/2021');
SELECT*FROM SOUTH_INDIA;



SELECT SOUTH_INDIA.NAME, VaccineData.Vaccine,SOUTH_INDIA.Hospital_Name,SOUTH_INDIA.Region
FROM (VaccineData
INNER JOIN SOUTH_INDIA ON VaccineData.VaccineID=SOUTH_INDIA.VaccineID);


CREATE TABLE EAST_INDIA(
VaccineID INT ,
NAME VARCHAR(255) NOT NULL,
Dose INT,
Hospital_Name VARCHAR(255) NOT NULL,
Region VARCHAR(255) NOT NULL,
DATE DATETIME);
INSERT INTO EAST_INDIA
VALUES
('2','Baban','2','Jeevan Hospital','EastIndia','01/03/2020'),
('1','Babita','2','Babumoshai Hospital','EastIndia','03/03/2020'),
('6','Abdul','1','Gokul Hospital','EastIndia','03/03/2020'),
('4','Bhide','1','Sarovar Hospital','EastIndia','03/05/2020'),
('4','Tapu','2','Sarovar Hospital','EastIndia','05/05/2020'),
('3','Sakaram','2','Toofan Hospital','EastIndia','03/01/2020'),
('5','Sodhi','1','Roshan Hospital','EastIndia','02/01/2020'),
('5','Jethalal','1','Gada Hospital','EastIndia','01/01/2021'),
('3','Mehta','1','Anjali Hospital','EastIndia','01/04/2021'),
('2','Hathi','1','Komal Hospital','EastIndia','04/04/2021');
SELECT*FROM EAST_INDIA;


SELECT*INTO Joined FROM SOUTH_INDIA UNION SELECT * FROM EAST_INDIA;

SELECT*FROM Joined


SELECT Joined.NAME, VaccineData.Vaccine,Joined.Hospital_Name,Joined.Region,Joined.DATE
FROM (VaccineData
INNER JOIN Joined ON VaccineData.VaccineID=Joined.VaccineID);



SELECT * FROM Joined
WHERE NAME LIKE 'S%';

SELECT*FROM Joined
ORDER BY DATE;

SELECT * FROM Joined
WHERE DATE BETWEEN '2020-01-03' AND '2021-01-06';




CREATE PROCEDURE  SelectAllJoinedRegion @Region varchar(30),@Dose INT
AS
SELECT * FROM Joined WHERE Region = @Region AND Dose= @Dose
GO

EXEC SelectAllJoinedRegion @Region= 'SouthIndia' , @Dose= '2';


CREATE TABLE WEST_INDIA(
VaccineID INT ,
NAME VARCHAR(255) NOT NULL,
Dose INT,
Hospital_Name VARCHAR(255) NOT NULL,
Region VARCHAR(255) NOT NULL,
DATE DATETIME);
INSERT INTO WEST_INDIA
VALUES
('1','Sam','2','Mumba Hospital','WestIndia','01/04/2020'),
('2','Rocky','1','Mumba Hospital','WestIndia','04/04/2021'),
('3','Dwanye','1','City Hospital','WestIndia','02/02/2021'),
('4','Austin','2','City Hospital','WestIndia','02/01/2021'),
('5','Brock','2','Tomas Hospital','WestIndia','02/02/2021'),
('6','Kane','1','Smith Hospital','WestIndia','06/02/2021'),
('1','Ortan','1','Bill Hospital','WestIndia','06/02/2021'),
('2','Rollins','2','Billard Hospital','WestIndia','03/02/2021'),
('3','MVP','2','Richards Hospital','WestIndia','03/04/2021'),
('4','Mysterio','2','Richards Hospital','WestIndia','03/04/2021');
SELECT*FROM WEST_INDIA;


SELECT VaccineData.VaccineID, EAST_INDIA.NAME, WEST_INDIA.Hospital_Name,VaccineData.Vaccine
FROM ((VaccineData
FULL OUTER JOIN EAST_INDIA ON VaccineData.VaccineID = EAST_INDIA.VaccineID)
FULL OUTER JOIN WEST_INDIA ON VaccineData.VaccineID = WEST_INDIA.VaccineID);


SELECT*INTO EASTWESTSOUTH FROM SOUTH_INDIA UNION SELECT * FROM EAST_INDIA UNION SELECT*FROM WEST_INDIA;

SELECT*FROM EASTWESTSOUTH;

SELECT * INTO EASTWESTSOUTHBACKUP
FROM EASTWESTSOUTH;



select * from EASTWESTSOUTHBACKUP;


ALTER TABLE "EASTWESTSOUTHBACKUP" 
 ALTER COLUMN  'Regionnew' VARCHAR(255) where column name = 'Region'  ;

 EXEC sp_rename 'EASTWESTSOUTHBACKUP.Region', 'Region new', 'COLUMN';

 SELECT*FROM EASTWESTSOUTHBACKUP;


 

SELECT COUNT(NAME), Dose
FROM EASTWESTSOUTHBACKUP
GROUP BY Dose;

SELECT COUNT(NAME), [Region new]
FROM EASTWESTSOUTHBACKUP
GROUP BY [Region new];





ALTER TABLE EASTWESTSOUTHBACKUP
ADD CHECK (Hospital_Name = 'Club Hospital');

SELECT * FROM EASTWESTSOUTHBACKUP
ORDER BY VaccineID;

