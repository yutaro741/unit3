#This is the answer of quiz 034.

```.py
def romantranslate(n):
    romandict = {1:"I", 5:"V", 10:"X", 50:"L", 100:"C", 500:"D", 1000:"M"} #Make a dictionally writing about each digits.
    if not isinstance(n, int):
        raise TypeError("input must be integer") #let it error if its not integer
    if n<=0 or n>3999:
        raise TypeError("input must be 1~3999") #let it error if its abobe 4000
    n = str(n) #Let it to strings to get easier to get highest digit of n. We will use int(x) tipe every time because I let it to str here.
    out = "" #We will add the program to here
    while n != "": #Continue until its gets zero.
        if 1<=int(n[0])<= 3:
            out += romandict[10**(len(n)-1)]*int(n[0]) #If highest digit is 1~3, just add that sign 1~3 times.
        if int(n[0]) == 4 or int(n[0]) == 9:
            out += romandict[10**(len(n)-1)] 
            out += romandict[(int(n[0])+1)*10**(len(n)-1)] #If n=4, 9, add n's digit sign first and n+1 sign next.
        if 5<=int(n[0])<=8:
            out += romandict[5*10**(len(n)-1)]
            out += romandict[10**(len(n)-1)]*(int(n[0])-5) #If n=5~8, just add n-[5-n] sign and do the same things at n=1~3.
        #if n=0, do nothing.
        n = n[1:] #delete highest digit and go back to roop.

    return out
    
    
    
######This is just test. It will continue until its does 100times roop, or gets 7%.
import random
for i in range(1, 100):
    r = random.randint(0, 4300)
    print(r, romantranslate(r))

```


#And this is the return
```
2372 MMCCCLXXII
1455 MCDLV
2480 MMCDLXXX
2104 MMCIV
2540 MMDXL
308 CCCVIII
1049 MXLIX
3492 MMMCDXCII
1030 MXXX
3740 MMMDCCXL
1569 MDLXIX
1451 MCDLI
1614 MDCXIV
3826 MMMDCCCXXVI
1203 MCCIII
3689 MMMDCLXXXIX
712 DCCXII
3067 MMMLXVII
105 CV
3894 MMMDCCCXCIV
1363 MCCCLXIII
2446 MMCDXLVI
910 CMX
3149 MMMCXLIX
363 CCCLXIII
1363 MCCCLXIII
764 DCCLXIV
3787 MMMDCCLXXXVII
739 DCCXXXIX
1248 MCCXLVIII
1914 MCMXIV
3769 MMMDCCLXIX
2667 MMDCLXVII
2800 MMDCCC
3524 MMMDXXIV
2258 MMCCLVIII
3321 MMMCCCXXI
2874 MMDCCCLXXIV
3905 MMMCMV
1231 MCCXXXI
2529 MMDXXIX
225 CCXXV
1186 MCLXXXVI
2419 MMCDXIX
1499 MCDXCIX
1266 MCCLXVI
1010 MX
3181 MMMCLXXXI
2020 MMXX
1387 MCCCLXXXVII
1189 MCLXXXIX
441 CDXLI
244 CCXLIV
2224 MMCCXXIV
1701 MDCCI
Traceback (most recent call last):
  File "/Users/yuyu/PycharmProjects/unit3/quiz34.py", line 26, in <module>
    print(r, romantranslate(r))
  File "/Users/yuyu/PycharmProjects/unit3/quiz34.py", line 6, in romantranslate
    raise TypeError("input must be 1~3999")
TypeError: input must be 1~3999

```

And this is the results.

```.py
#I realized that I have the test now.
from quiz34 import to_roman

import pytest

def test_to_roman():
    assert to_roman(1) == 'I'
    assert to_roman(4) == 'IV'
    assert to_roman(9) == 'IX'
    assert to_roman(37) == 'XXXVII'
    assert to_roman(44) == 'XLIV'
    assert to_roman(50) == 'L'
    assert to_roman(99) == 'XCIX'
    assert to_roman(100) == 'C'
    assert to_roman(77) == 'LXXVII'
    assert to_roman(93) == 'XCIII'


def test_to_roman_exceptions():
    # check that the program raises a ValueError. This program can do with 1~3999, so I changed to 4000 instead of 101.
    with pytest.raises(ValueError):
        to_roman(4000)
```
```.py
/Users/yuyu/PycharmProjects/unit3/venv/bin/python /private/var/folders/dt/_jx_m4cn6nn8f5btht6cclwh0000gn/T/AppTranslocation/6AB0605A-4C57-4376-AF28-17871DE968A3/d/PyCharm.app/Contents/plugins/python/helpers/pycharm/_jb_pytest_runner.py --path /Users/yuyu/PycharmProjects/unit3/quiz34test.py 
Testing started at 15:08 ...
Launching pytest with arguments /Users/yuyu/PycharmProjects/unit3/quiz34test.py --no-header --no-summary -q in /Users/yuyu/PycharmProjects/unit3

============================= test session starts ==============================
collecting ... collected 2 items

quiz34test.py::test_to_roman PASSED                                      [ 50%]
quiz34test.py::test_to_roman_exceptions PASSED                           [100%]

============================== 2 passed in 0.03s ===============================

プロセスは終了コード 0 で終了しました
```
