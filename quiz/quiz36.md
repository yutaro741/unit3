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
