This is the answer of quiz35
```.py
class Account:
    def __init__(self):
        self.balance = 0
        self.holder_name = ""
        self.holder_email = "" #set the orijinal setting.
        import random
        number = []
        for i in [3, 5, 1]:
            number.append(random.randint(10**(i-1), 10**(i)))
        self.number = number #make the random numbers that has 3, 5, 1, digits. 


    def get_account_no(self):
        out = ""
        for i in self.number:
            out += str(i)
            if len(str(i)) != 1:
                out += "-" #Add the - inside the length.
        return out

    def set_holder_name(self, name):
        if self.holder_name == name:
            raise TypeError("This name is already setted")
        if isinstance(name, float) or isinstance(name, int):
            raise TypeError("Please enter strings")
        self.holder_name = name
        return f"Holder's name set to {name}"

    def set_holder_email(self, email):
        if str(email).count("@") != 1:
            raise ValueError("Please input email")
        self.holder_email = email
        return f"Holder's email set to {email}"

    def get_balance(self):
        return self.balance

    def deposit(self, amount):
        new_amout = self.balance + amount
        self.balance = new_amout
        return f"New balance: {new_amout} USD"
```

This is test file.
```.py
import pytest
from quiz35 import Account

def test_empty_account():
    bk = Account()
    assert bk.balance == 0
    assert bk.holder_name == ""
    assert bk.holder_email == ""
    assert isinstance(bk.number, list)
    number = bk.get_account_no().split("-")
    assert len(number) == 3 and len(number[0]) == 3 and len(number[1]) == 5 and len(number[2]) == 1

def test_create_account():
    bk = Account()
    assert bk.get_balance() == 0
    assert bk.set_holder_name(name="Bob") == "Holder's name set to Bob"
    assert bk.set_holder_email(email="bob@company.xyz") == "Holder's email set to bob@company.xyz"
    assert bk.deposit(amount=100) == "New balance: 100 USD"
    assert bk.get_balance() == 100


def test_value_errors():
    bk = Account()
    with pytest.raises(ValueError):
        bk.set_holder_email(email="bob@bob@bob")
        bk.set_holder_name(name=["Bob"])
        bk.set_holder_name(name=100)
```


And this is the results of the test.
```.py
/Users/yuyu/PycharmProjects/unit3/venv/bin/python /private/var/folders/dt/_jx_m4cn6nn8f5btht6cclwh0000gn/T/AppTranslocation/6AB0605A-4C57-4376-AF28-17871DE968A3/d/PyCharm.app/Contents/plugins/python/helpers/pycharm/_jb_pytest_runner.py --path /Users/yuyu/PycharmProjects/unit3/quiz35test.py 
Testing started at 15:13 ...
Launching pytest with arguments /Users/yuyu/PycharmProjects/unit3/quiz35test.py --no-header --no-summary -q in /Users/yuyu/PycharmProjects/unit3

============================= test session starts ==============================
collecting ... collected 3 items

quiz35test.py::test_empty_account PASSED                                 [ 33%]
quiz35test.py::test_create_account PASSED                                [ 66%]
quiz35test.py::test_value_errors PASSED                                  [100%]

============================== 3 passed in 0.02s ===============================

プロセスは終了コード 0 で終了しました

```
