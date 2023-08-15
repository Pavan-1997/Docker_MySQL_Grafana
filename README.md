# Loading data into MySQL DB and visualizing data on Grafana where both are running on Docker 

### Setting up the server on Docker

![image](https://github.com/Pavan-1997/Docker_MySQL_Grafana/assets/32020205/f969c2c8-cae4-44b7-b9a9-e3b3fd80c64c)

![image](https://github.com/Pavan-1997/Docker_MySQL_Grafana/assets/32020205/2f37e590-7beb-46ec-9d6e-2926acf1dd1b)

---

# Loading data into MySQL DB and visualizing data on Grafana 

### Preq: Setup Docker


Step1: Run Grafana
```
docker run -d --name=grafana -p 3001:3000 -v grafana_config:/etc/grafana -v grafana_data:/var/lib/grafana -v grafana_logs:/var/log/grafana grafana/grafana
```

Step2: Give password as admin:admin and set a new password


Step3: Run MySQL
```
docker run -d --name mysqldb -p 3306:3306 -v db_data:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=password mysql:latest
```

Step4: Login to the MySQL container
```
docker exec -it mysqldb bash
```

Step5: Login to the MySQL
```
mysql -u root -p password 
```

Step5: Look for DB's inside
```
show databases;
```

Step6: Create a DB
```
create database team;
```

Step7: Use the new created DB
```
USE team;
```

Step8: Create a table in the DB
```
CREATE TABLE person ( person_id INT NOT NULL PRIMARY KEY, fname VARCHAR(40) NULL, lname VARCHAR(40) NULL, age INT NOT NULL, created TIMESTAMP );

```
Step9: Check the tables

show tables;


Step10: Insert data into the table

INSERT INTO person (person_id, fname, lname, age) VALUES (1,'Peter','Engineer', 32);
INSERT INTO person (person_id, fname, lname, age) VALUES (2, 'Richard', 'Gaol', 27);
INSERT INTO person (person_id, fname, lname, age) VALUES (3, 'Howard', 'Ken', 38);
INSERT INTO person (person_id, fname, lname, age) VALUES (4, 'Lucy', 'Dey', 32);


Step11: Add Datasource to the Grafana

Go to the Grafana dashboard select Data Sources give the following details:

Host - localhost:3306
Database - Database Name
User and Password 

If you get any error: Command to add the port to firewall:

firewall-cmd --permanent --zone=public --add-port=3306/tcp

firewall-cmd --reload


Step12: Add a dashboard with add a panel 
