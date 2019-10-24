 ************** for adding data to newlye created column - DON NOT IUSE INSERT!

 UPDATE `test` SET `last updated`= '2019-01-26 14:30:00' WHERE `fullname` = 'Simon Capet';
 UPDATE `test` SET `last updated`= '2018-01-26 16:30:00' WHERE `fullname` = 'Simon New';
 UPDATE `test` SET `last updated`= '2017-01-26 04:30:00' WHERE `fullname` = 'Kasia Pranke';
 UPDATE `test` SET `last updated`= '2016-01-26 13:45:00' WHERE `fullname` = 'Josh Sweet';
************

###  Add a new column for 'last updated'.

The single column should store the date and time the row was last updated (make these times up!).
There are various data types that are suitable for storing dates and times, so do a bit of research.
Advanced: populate and update field automatically.

ALTER TABLE `test` ADD COLUMN `created` TIMESTAMP default now();

ALTER TABLE `test` ADD COLUMN `last updated` TIMESTAMP default now() ON UPDATE CUnow();

###  Create a search query.

Find a way of returning just the rows that have `fullname` starting with 'Simon'.

SELECT `fullname` FROM `test` WHERE `fullname` LIKE 'Simon%';

/the percent sign indicates if theres anything before or after the serarch query.

### Totaling up columns. 

Find the total age from the rows that have a "t" in the location.

SELECT sum(`age`) FROM `test` WHERE `location` LIKE '%t%';


### Make another table to store information about pets owned by the people in our `test` table.

CREATE TABLE IF NOT EXISTS `pets` (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `owner id` int(11) NOT NULL,
  `animal` varchar(255) NOT NULL,
  PRIMARY KEY (`id`)
) ENGINE=InnoDB  DEFAULT CHARSET=latin1 AUTO_INCREMENT=6 ;

UPDATE `pets` SET `animal` ='rat' WHERE `id` = 1;
UPDATE `pets` SET `animal` ='dog' WHERE `id` = 2;
UPDATE `pets` SET `animal` ='cat' WHERE `id` = 3;
UPDATE `pets` SET `animal` ='elephant' WHERE `id` = 4;


### to modify column's definition

ALTER TABLE `test` MODIFY COLUMN `favourite beverage` VARCHAR(255) NOT NULL;
---> Use this to modify column's definition. For example, to change column `favourite beverage` to VARCHAR(255)



### Creating Table for id/activation code/ email / password / activation status / 

CREATE TABLE IF NOT EXISTS `users` (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `email` varchar(255) NOT NULL,
  `password` varchar(255) NOT NULL,
  `activation code` int(11) NOT NULL,
  `activation state` varchar(255) NOT NULL, 
  PRIMARY KEY (`id`)
) ENGINE=InnoDB  DEFAULT CHARSET=latin1 AUTO_INCREMENT=1 ;

UPDATE `rt` SET `animal` ='rat' WHERE `id` = 1;
UPDATE `rt` SET `animal` ='dog' WHERE `id` = 2;
UPDATE `rt` SET `animal` ='cat' WHERE `id` = 3;
UPDATE `rt` SET `animal` ='elephant' WHERE `id` = 4;




### If you want to SAVE YOUR DATABSE  to external file

```command
$ cd /var/www/public
```

mysqldump -u root -proot scotchbox > db-dump.sql
mysql -u root -proot scotchbox < db-dump.sql









