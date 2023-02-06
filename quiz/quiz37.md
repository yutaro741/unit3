This is answer of quiz37.

```.py
class Compoundinterest:
    def __init__(self, principal, rate, years):
        self.principal = principal
        self.rate = rate
        self.years = years
    def get_intesert(self):
        self.interest = self.principal*(1+self.rate)**self.years
        return self.interest

class AccountingProgram:
    def __init__(self, principal, rate, years):
        self.data = Compoundinterest(principal=principal, rate=rate, years=years).get_intesert()

    def get_data(self):
        return self.data

data = Compoundinterest(principal=5, rate=2, years=3)
print(AccountingProgram(principal=5, rate=2, years=3).get_data())
```

```.py
import pytest
from quiz37 import AccountingProgram

def test_calculate_interest():
    program = AccountingProgram()
    program.set_principal(1000)
    program.set_rate(0.05)
    program.set_years(10)
    interest = program.calculate_interest()
    assert interest == 1628.89

def test_principal_validation():
    program = AccountingProgram()
    with pytest.raises(ValueError) as err:
        program.set_principal(-1000)
    assert "Principal should be greater than zero" in str(err.value)

def test_rate_validation():
    program = AccountingProgram()
    with pytest.raises(ValueError) as err:
        program.set_rate(-0.05)
    assert "Interest rate should be greater than zero" in str(err.value)

def test_years_validation():
    program = AccountingProgram()
    with pytest.raises(ValueError) as err:
        program.set_years(-10)
    assert "Years should be greater than zero" in str(err.value)
```

And this is the results.

```.py
/Users/yuyu/PycharmProjects/unit3/venv/bin/python /private/var/folders/dt/_jx_m4cn6nn8f5btht6cclwh0000gn/T/AppTranslocation/6AB0605A-4C57-4376-AF28-17871DE968A3/d/PyCharm.app/Contents/plugins/python/helpers/pycharm/_jb_pytest_runner.py --path /Users/yuyu/PycharmProjects/unit3/quiz37test.py 
Testing started at 15:31 ...
Launching pytest with arguments /Users/yuyu/PycharmProjects/unit3/quiz37test.py --no-header --no-summary -q in /Users/yuyu/PycharmProjects/unit3

============================= test session starts ==============================
collecting ... collected 4 items

quiz37test.py::test_calculate_interest PASSED                            [ 25%]
quiz37test.py::test_principal_validation PASSED                          [ 50%]
quiz37test.py::test_rate_validation PASSED                               [ 75%]
quiz37test.py::test_years_validation PASSED                              [100%]


============================== 4 passed in 0.03s ===============================

プロセスは終了コード 1 で終了しました
```
