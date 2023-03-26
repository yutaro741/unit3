This is the answer of quiz 47.


```.py

import sqlite3

from kivymd.app import MDApp
# from secure_password import encrypt_password

from passlib.context import CryptContext

pwd_config = CryptContext(schemes=["pbkdf2_sha256"],
                          default="pbkdf2_sha256",
                          pbkdf2_sha256__default_rounds=30000
                          )


def encrypt_password(user_password):
    """ This function receives the plain text password from the user and returns the hash salted.
    """
    return pwd_config.encrypt(user_password)

def check_password(user_password, hashed):
    return pwd_config.verify(user_password, hashed)


class database_worker:
    def __init__(self, name):
        self.connection = sqlite3.connect(name)
        self.cursor = self.connection.cursor()

    def search(self, query):
        result = self.cursor.execute(query).fetchall()
        return result

    def run_save(self, query):
        self.cursor.execute(query)
        self.connection.commit()

    def close(self):
        self.connection.close()


class quiz047(MDApp):
    def __init__(self, **kwargs):
        super().__init__(**kwargs)
        self.components = {"basic":0}

    def build(self):
        return

    def save(self):
        pass

    def update(self):
        #This function updates all the labels in the form using the base salary and the percentage
        # Pseudocode
        # 1- get the base salary from the GUI
        base = self.root.ids.base.text
        hash = ""

        if base != "":
            base = int(base)
            # 2???- if base salary define total=int(base) and an empty string to store build a hash (for_hash="") if no base then end the function
            total = int(base)
            hash += f"base{total}"
            # 3- for Each TextField with ids: "inhabitant","income_tax","pension","health" get the text property
            inhabitant = self.root.ids.inhabitant.text
            income_tax = self.root.ids.income_tax.text
            pension = self.root.ids.pension.text
            health = self.root.ids.health.text
            # 4- if the TextField.text has a number (value), calculate the equation new_value="(base*int(value)//100) JPY" and subbctract the equation to the total
            # 5- if no: then new_value = " JPY"
            new_value = []
            lists = ["inhabitant", "income_tax", "pension", "health"]
            nums = [inhabitant, income_tax, pension, health]
            for i in range(4):
                if nums[i] == "":
                    new_value.append(" JPY")
                    hash += f"{lists[i]}0"

                else:
                    nums[i] = int(nums[i])
                    new_value.append(f"{base*nums[i]//100} JPY")
                    total -= base*nums[i]//100
                    hash += f"{lists[i]}{nums[i]}"

            # 6- set the label next to the TextField (inhabitant_label, income_tax_label, etc) to the variable new_value
            self.root.ids.inhabitant_label.text = new_value[0]
            self.root.ids.income_tax_label.text = new_value[1]
            self.root.ids.pension_label.text = new_value[2]
            self.root.ids.health_label.text = new_value[3]

            # 7- concatenate to the hash variable the f"{id}{value}"
            # 8- set the text of the element id=total to the total with the JPY symbol
            self.root.ids.salary_label.text = f"{total} JPY"
            hash += f"total{total}"
        # 9- encrypt the hash and change the text of the label with id=hash to the last 50 characters of the hash
            hash = encrypt_password(hash)
        self.root.ids.hash.text = hash[:50]




    def save(self):
        #This function updates all the labels in the form using the base salary and the percentage
        # Pseudocode
        # 1- get the base salary from the GUI
        base = self.root.ids.base.text
        hash = ""

        if base != "":
            base = int(base)
            # 2???- if base salary define total=int(base) and an empty string to store build a hash (for_hash="") if no base then end the function
            total = int(base)
            hash += f"base{total}"
            # 3- for Each TextField with ids: "inhabitant","income_tax","pension","health" get the text property
            inhabitant = self.root.ids.inhabitant.text
            income_tax = self.root.ids.income_tax.text
            pension = self.root.ids.pension.text
            health = self.root.ids.health.text
            # 4- if the TextField.text has a number (value), calculate the equation new_value="(base*int(value)//100) JPY" and subbctract the equation to the total
            # 5- if no: then new_value = " JPY"


            new_value = []
            lists = ["inhabitant", "income_tax", "pension", "health"]
            nums = [inhabitant, income_tax, pension, health]
            for i in range(4):
                if nums[i] == "":
                    new_value.append(0)
                    hash += f"{lists[i]}0"

                else:
                    nums[i] = int(nums[i])
                    new_value.append(base*nums[i]//100)
                    total -= base*nums[i]//100
                    hash += f"{lists[i]}{nums[i]}"

            self.inhabitant_label = new_value[0]
            self.income_tax_label = new_value[1]
            self.pension_label = new_value[2]
            self.health_label = new_value[3]


            self.salary_label = total
            hash += f"total{total}"
        # 9- encrypt the hash and change the text of the label with id=hash to the last 50 characters of the hash
            hash = encrypt_password(hash)

        #repeat the algorithm in update but create variables to save the amount of each item:
        #base = int(base)
        #inhabitant = amount in JPY to remove from base for inhabitant tax
        #income_tax = amount in JPY to remove from base for income tax
        #pension = amount in JPY to remove from base for pension tax
        #health = amount in JPY to remove from base for health tax
        #total = total net salary
        #hahs = hash of the calcualtions in the format
        #inhabitant4,income_tax3,pension2,health1,total1103  (here the numbers next to the category are percentages)

        # query = f"""INSERT into payments
            query = f"""INSERT INTO payments(base, inhabitant, income_tax, pension, health, total, hash) VALUES('base', '{self.inhabitant_label}', '{self.income_tax_label}', '{self.pension_label}', '{self.health_label}', '{total}', '{hash}');"""


        # --here complete the code
        #
        # """
            db = database_worker("payments.db")
            db.run_save(query)
            db.close()
            self.root.ids.hash.text = f"Payment saved"

    def clear(self):
        for label in ["base", "inhabitant","income_tax","pension","health"]:
            self.root.ids[label].text = ""
            self.root.ids[label+"_label"].text = " JPY"

        self.root.ids["salary_label"].text = " JPY"
        self.root.ids.hash.text = "----"


test = quiz047()
test.run()
```


If we run the program, it will be like this.
![](https://github.com/yutaro741/unit3/blob/main/pictures/Screen%20Shot%202023-03-26%20at%2016.22.28.png)
As you enter the data, the results will automatically caliculated and spend it easelly.
![](https://github.com/yutaro741/unit3/blob/main/pictures/Screen%20Shot%202023-03-26%20at%2016.22.37.png)
If you press the save button, it will get in to the database with hashed data.
