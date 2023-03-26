This is answer of quiz 43.

This is console.

```.py
#Create the Movies table.
CREATE TABLE if NOT exists Movies(
    id INTEGER PRIMARY KEY,
    year INTEGER not NULL,
    budget TEXT not NULL,
    category TEXT not NULL,
    director TEXT not NULL,
    producer TEXT not NULL,
    name TEXT not NULL
);

#Add movie "Suzume no tojimari"
INSERT INTO Movies(year, budget, category, director, producer, name) VALUES(2022, "14.21bil", "fantasy adventure", "Makoto Shinkai", "Genki Kawamura", "Suzume no tojimari");

#Add movie "one piece film red"
INSERT INTO Movies(year, budget, category, director, producer, name) VALUES(2022, "19.7bil", "fantasy action-adventure", "Gorō Taniguchi", "Eiichiro Oda", "one piece film red");

#Show everything that in database.
SELECT * FROM Movies
```

The results will be like this.

![](https://github.com/yutaro741/unit3/blob/main/pictures/Screen%20Shot%202023-03-26%20at%2015.46.39.png)
