This is answer of quiz 48.

```.py
import sqlite3

# secure password
import sqlite3

# secure password
from passlib.context import CryptContext

#Create an object of the class CryptContext
pwd_config = CryptContext(schemes=["pbkdf2_sha256"],
                          default="pbkdf2_sha256",
                          pbkdf2_sha256__default_rounds=30000
                          )

#this function receives the unsafe password
# and returns the hashed password
def encrypt_password(user_password):
    return pwd_config.hash(user_password)

def check_password(hashed_password, user_password):
    return pwd_config.verify(user_password, hashed_password)

# hash = encrypt_password("password123")
# print(hash)

class getinfo():
    def __init__(self):
        self.connection = sqlite3.connect("bitcoin_exchange.db")
        self.cursor = self.connection.cursor()

    def get_info(self, query):
        self.cursor.execute(query)
        return self.cursor.fetchall()

    def close(self):
        self.connection.close()

#Get each data from database and print it into 
for id in range(1, 6):
    query = f"""SELECT * FROM ledger WHERE id = '{id}'"""
    info = (getinfo().get_info(query))
    getinfo().close()

    info = list(info[0])
    hashing = f'"id {info[0]},sender_id {info[1]},receiver_id {info[2]},amount {info[3]}"'
    print(hashing)
    if check_password(encrypt_password(hashing), info[4]):
        print(True)
    else:
        print(False)
    print("\n")
```


And this is the output of the codes.

```
/Users/yuyu/PycharmProjects/unit3/venv/bin/python /Users/yuyu/PycharmProjects/unit3/quiz48.py 
"id 1,sender_id 560,receiver_id 371,amount 37255"
False


"id 2,sender_id 488,receiver_id 561,amount 1431"
False


"id 3,sender_id 254,receiver_id 920,amount 26756"
False


"id 4,sender_id 438,receiver_id 920,amount 15968"
False


"id 5,sender_id 744,receiver_id 261,amount 24371"
False



プロセスは終了コード 0 で終了しました
```
