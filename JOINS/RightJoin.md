# RIGHT JOIN
The RIGHT JOIN keyword returns all records from the right table (table2), and the matching records (if any) from the left table (table1).
![image](https://github.com/yadhukishore/EnteSQL/assets/110115711/ee15f9ba-f4e6-4426-9084-5e119a1b2eac)


```sql
CREATE DATABASE db2;
USE db2;
CREATE TABLE country(
co_code VARCHAR(10) NOT NULL,
co_name VARCHAR(50),
PRIMARY KEY(co_code)
);
INSERT INTO country
VALUES
('IN','India'),
('UK','United Kingdom'),
('NP','Nepal'),
('PK','Pakisthan'),
('SL','Sri Lanka');
SELECT * FROM country;

CREATE TABLE capital(
cap_id VARCHAR(10) NOT NULL,
co_code VARCHAR(10),
cap_name VARCHAR(100),
PRIMARY KEY(cap_id),
FOREIGN KEY(co_code) REFERENCES country(co_code)
);
INSERT INTO capital
VALUES
('c1','UK','London'),
('c2','IN',"New Delhi"),
('c3','PK','Islamabad');
SELECT * FROM capital;

/*Right join*/
SELECT * FROM country RIGHT JOIN capital
ON country.co_code = capital.co_code;
```

### Right table ill ollath ellam kaata left ill ath ayi match avne left side recordum labikum.
