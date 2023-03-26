This is the answer of quiz 46.

```.py
import sqlite3

class database_handler():#Database handler defs.
    def __init__(self, namedb:str):
        self.connection = sqlite3.connect(namedb)
        self.cursor = self.connection.cursor()

    def run_query(self, query):
        self.cursor.execute(query)
        self.connection.commit()

    def close(self):
        self.connection.close()

    def get_info(self, query):
        self.cursor.execute(query)
        return self.cursor.fetchall()

    def add_note(self, length, word):
        query = f"""INSERT INTO words(length, word) VALUES('{length}', '{word}')"""
        self.run_query(query)

#Open the database, and make the table "words" if there is no table.
addtable = f"""CREATE TABLE if not exists words(id INTEGER PRIMARY KEY,length INTEGER not null,word text not null);"""
db = database_handler("haikudb.db")
db.run_query(addtable)


haiku = "Code flows like a stream Algorithms guide its way In silence, it solves"
for word in haiku.split():#split the haiku into each words and add word and lenght of the word to the database "word".
    length = len(word)
    db.add_note(length, word)

#Find the average length of the words.
query = """SELECT AVG(length) from words"""

haiku = db.get_info(query)
db.close()#Close the database.

haiku = list(haiku[0])[0]
print(haiku)#Print the average length of the words.
```

The message I got is below.

```
/Users/yuyu/PycharmProjects/unit3/venv/bin/python /Users/yuyu/PycharmProjects/unit3/quiz46.py 
4.538461538461538

プロセスは終了コード 0 で終了しました
```
