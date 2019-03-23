# DB08

Made by:
- Chris Rosendorf
- Vikto Kim Christiansen
- William Pfaffe

## IMPORTANT NOTICE:
In order to create your own slave, or point to the right master server, make sure your slave has IO Access, otherwise it won't be able to read the log file.
Read the guide properly before making additional slaves.

## 4
```
INSERT INTO customers (customerNumber, customerName, contactLastName, contactFirstName, phone, addressLine1, city, state, postalCode, country, creditLimit) VALUES (498, 'Viktos Sutter', 'Suttemanden', 'SKalBrugeDocker', '85858585', 'Suttegaden 85', 'Denmark', 'Copenhagen', '2630', 'Denmark', '100000.00'); 
```
## 5
Using the following transaction, the new update will not be displayed properly
```
START TRANSACTION;
	UPDATE customers SET customerName = "Vikto Ikke Sutte" WHERE customerNumber=497;
```

Using this however:
```
START TRANSACTION;
	UPDATE customers SET customerName = "Vikto Ikke Sutte" WHERE customerNumber=497;
COMMIT;
```
Will make the changes on the slave

Notice: The slave cannot detect ANY changes that are made, untill commit has been done. Any inserts afterwards or updates will not be replicated, before a commit has happened.
