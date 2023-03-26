This is the answer of quiz 44.

This is database file.
```
--There is 4 tables in database

SELECT * from INHABITANT WHERE gender = "Male" and state = "Friendly";
--There is 4 Male inhabitants are friendly
SELECT avg(gold) from INHABITANT;
--ave gold is 123.75
SELECT item from ITEM where item LIKE "A%";
--There is 3 items
SELECT count(distinct Job) from INHABITANT;
--There is 15 types of job.
SELECT item from ITEM where owner = (SELECT personid from INHABITANT where job = "herbalists");
--herbalists don't have item.
```

