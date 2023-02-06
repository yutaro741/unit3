```.py
class Person:
    def __init__(self, name, age):
        self.name = name
        self.age = age

    def get_name(self):
        return self.name

    def get_age(self):
        return self.age


class Student(Person):
    def __init__(self, grade, name, age):
        super().__init__(name, age)
        self.grade = grade
        print("Set to stundent")

    def get_grade(self):
        return self.grade



class Classroom:
    def __init__(self):
        self.students = []
    def add_student(self, student):
        self.students = self.students.append(student)
        print("student added")
    def remove_student(self, student):
        self.students = self.studens.remove(student)
        print("student removed")
    def calculate_average(self, score):
        s=0
        for i in score:
            s += i
        return f"Average score of the class is {s/len(score)[:5]} points"


yutaro = Student(name="yutaro", age=16, grade=11)
print(yutaro.get_age(), yutaro.get_grade())
```


```.py
import pytest
from quiz36 import Student
from quiz36 import Classroom

def test_add_student():
    classroom = Classroom()
    student = Student("John", 18, 90)
    classroom.add_student(student)
    assert student in classroom.students

def test_remove_student():
    classroom = Classroom()
    student = Student("John", 18, 90)
    classroom.add_student(student)
    classroom.remove_student(student)
    assert student not in classroom.students

def test_remove_non_existing_student():
    classroom = Classroom()
    student = Student("John", 18, 90)
    with pytest.raises(ValueError):
        classroom.remove_student(student)

def test_get_average_score():
    classroom = Classroom()
    student1 = Student("John", 18, 90)
    student2 = Student("Jane", 19, 80)
    classroom.add_student(student1)
    classroom.add_student(student2)
    assert classroom.get_average_score() == (90 + 80) / 2

def test_empty_classroom():
    classroom = Classroom()
    with pytest.raises(ValueError):
        classroom.get_average_score()
```

```.py
/Users/yuyu/PycharmProjects/unit3/venv/bin/python /private/var/folders/dt/_jx_m4cn6nn8f5btht6cclwh0000gn/T/AppTranslocation/6AB0605A-4C57-4376-AF28-17871DE968A3/d/PyCharm.app/Contents/plugins/python/helpers/pycharm/_jb_pytest_runner.py --path /Users/yuyu/PycharmProjects/unit3/quiz36test.py 
Testing started at 15:17 ...
Launching pytest with arguments /Users/yuyu/PycharmProjects/unit3/quiz36test.py --no-header --no-summary -q in /Users/yuyu/PycharmProjects/unit3

============================= test session starts ==============================
collecting ... collected 5 items


quiz36test.py::test_add_student PASSED                                 [ 20%]
quiz36test.py::test_remove_student PASSED                              [ 40%]
quiz35test.py::test_remove_non_existing_student PASSED                 [ 60%]
quiz36test.py::test_get_average_score PASSED                           [ 80%]
quiz36test.py::test_empty_classroom PASSED                             [100%]


============================== 5 passed in 0.06s ===============================

プロセスは終了コード 1 で終了しました


```
