```.py
import matplotlib.pyplot as plt
import random
random.seed(0)

class coordinate:
    def __init__(self, x, y):
        self.x = x
        self.y = y

    def __repr__(self)->str:
        return f"[Coordinate Object] x:{self.x}, y:{self.y}"

class city:
    def __init__(self,name:str, location:coordinate):
        self.name = name
        self.location = location

    def __repr__(self)->str:
        return f"[City Object] City {self.name} is located at {self.location}"

    def distance(self, cityB):
        if isinstance(cityB, city):
            xa, ya = self.location.x, self.location.y
            xb, yb = cityB.location.x, cityB.location.y
        else:
            raise TypeError("Input should be an object of the class city")
        d = ((xa-xb)**2 + (ya-yb)**2)**(1/2)
        return d

class country:
    def __init__(self, name:str):
        self.name = name
        self.cities = []

    def add_city(self, new_city:city):
        self.cities.append(new_city)

    def __repr__(self):
        return f"country objet {len(self.cities)}"

Japan = country(name="Japan")
x = []
y = []
places = []
for name in ["Tokyo", "Yokohama", "Osaka", "Nagoya", "Sapporo", "Kobe", "Kyoto", "Fukuoka", "Kawasaki", "Saitama"]:
    xaxis = random.randint(0, 100)
    yaxis = random.randint(0, 100)
    x.append(xaxis)
    y.append(yaxis)
    places.append(name)
    rand_loc = coordinate(x=xaxis, y=yaxis)
    ct = city(name=name, location=rand_loc)
    Japan.add_city(ct)

plt.scatter(x, y)
for i in range(10):
    plt.annotate(places[i], (x[i], y[i]))
plt.xlim(0, 100)
plt.ylim(0, 100)
plt.title("map")
plt.show()
```

And this is the results.
I use random for each coordinate, so everytime this map will change.
![](https://github.com/yutaro741/unit3/blob/main/pictures/%E3%82%B9%E3%82%AF%E3%83%AA%E3%83%BC%E3%83%B3%E3%82%B7%E3%83%A7%E3%83%83%E3%83%88%202023-02-06%2016.39.12.png)
