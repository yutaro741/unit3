#This is answer of quiz 33

```.py
def mystery(list1, list2): #Get two list, list1 and list2
    output = [] #make empty list
    for i in list1:
        for j in list2: #Make roop within two list
            if i==j:
                output.append(i) #Add to output list if it same.
    return output

```

#And then, I test it with using pytest
```.py
import pytest
from quiz33 import mystery

def test_empty_lists():
  assert mystery([], []) == []

def test_one_common_element():
  assert mystery([1, 2, 3], [3, 4, 5]) == [3]

def test_multiple_common_elements():
  assert mystery([1, 2, 3, 4], [3, 4, 5, 6]) == [3, 4]
```

#This was the results that I got within Dr.Ruben's code

↓
```
Launching pytest with arguments quiz33test.py::test_multiple_common_elements --no-header --no-summary -q in /Users/yuyu/PycharmProjects/unit3

============================= test session starts ==============================
collecting ... collected 1 item

quiz33test.py::test_multiple_common_elements PASSED                      [100%]

============================== 1 passed in 0.01s ===============================
```
