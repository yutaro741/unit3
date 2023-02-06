This is answer of quiz39.
```.py
from kivymd.app import MDApp

class quiz39(MDApp):
    def __init__(self, **kwargs):
        self.count = 0
        super().__init__(**kwargs)

    def add(self): #Code to add number.
        self.count += 1
        self.root.ids.counting.text = f"Count {self.count}"

test = quiz39()
test.run()
```

This is kivy file.
```.py
Screen:
    size:500, 500

    MDBoxLayout:
        id:main_box
        size_hint:.7, .3
        pos_hint: {"center_x":0.5, "center_y":.5}
        orientation: "horizontal"

        MDLabel:
            id:counting
            text: "Count 0"
            color: "red"
            font_size: "34pt"
            size_hint: .5, 1
            md_bg_color: "#D3DEF1"
            pos_hint: {"center_x":.5, "center_y":.5}

        MDRaisedButton:
            id:add
            text: "add +1"
            color: "white"
            font_size: "34pt"
            size_hint: .5, 1
            md_bg_color: "#5AB9C1"
            on_press: app.add()
```

Below is the resulte.
![](https://github.com/yutaro741/unit3/blob/main/pictures/%E3%82%B9%E3%82%AF%E3%83%AA%E3%83%BC%E3%83%B3%E3%82%B7%E3%83%A7%E3%83%83%E3%83%88%202023-02-06%2016.44.03.png)

Each time you click, the number will increase one by one.
![](https://github.com/yutaro741/unit3/blob/main/pictures/%E3%82%B9%E3%82%AF%E3%83%AA%E3%83%BC%E3%83%B3%E3%82%B7%E3%83%A7%E3%83%83%E3%83%88%202023-02-06%2016.44.11.png)
