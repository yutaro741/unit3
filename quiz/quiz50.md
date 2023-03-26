This is answer of quiz 50.


```.py
class airline():#Question 1: Make the class.
    def __init__(self, flight_number, origin, destination, departure_time, duration):
        self.flight_number = flight_number
        self.origin = origin
        self.destination = destination
        self.departure_time = departure_time
        self.duration = duration

    def get_duration(self):#The function that returns string.
        return f"{self.duration[0]} hours {self.duration[1]} minutes {self.duration[2]} seconds"

#Two examples of the class.
test1 = airline(flight_number="AA123", origin="New York", destination="Los Angeles", departure_time="10:00 AM", duration=[5, 30, 3])
test2 = airline(flight_number="ZX741", origin="Naha", destination="Haneda", departure_time="6:00 AM", duration=[2, 30, 9])
print(test1.get_duration())
print(test2.get_duration())
```

And it is the output of the program.
```
/Users/yuyu/PycharmProjects/unit3/venv/bin/python /Users/yuyu/PycharmProjects/unit3/quiz50.py 
5 hours 30 minutes 3 seconds
2 hours 30 minutes 9 seconds

プロセスは終了コード 0 で終了しました
```
