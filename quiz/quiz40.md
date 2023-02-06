This is answer of quiz40

```.py
from kivymd.app import MDApp

class quiz40kv(MDApp):
    def __init__(self, **kwargs):
        self.black = 0
        super().__init__(**kwargs)

    def change_color(self): #Getting dark mode
        if self.root.ids.button.text == "Dark mode":
            self.root.ids.title.color = "#FFFFFF"
            self.root.ids.main_box.md_bg_color = "#000000"
            self.root.ids.button.text = "Light mode"
            self.root.ids.button.md_bg_color = "red"
        else: #Getting white mode
            self.root.ids.title.color = "#000000"
            self.root.ids.main_box.md_bg_color = "#FFFFFF"
            self.root.ids.button.text = "Dark mode"
            self.root.ids.button.md_bg_color = "blue"

text = quiz40kv()
text.run()
```

This is kivy file.
```.py
MDScreen:
    size:500, 500

    MDBoxLayout:
        id:main_box
        orientation: "vertical"
        size_hint: 1, .8
        pos_hint: {"center_x": .5, "center_y":.5}
        md_bg_color: "#FFFFFF"

        MDLabel:
            id: title
            text: "YUTARO"
            font_size: "100pt"
            orientation: "vertical"
            halign: "center"
            color:"red"

        MDRaisedButton:
            id: button
            text: "Dark mode"
            pos_hint: {"center_y":.5}
            md_bg_color: "blue"
            on_press: app.change_color()
```

Below is the results.
![](https://github.com/yutaro741/unit3/blob/main/pictures/%E3%82%B9%E3%82%AF%E3%83%AA%E3%83%BC%E3%83%B3%E3%82%B7%E3%83%A7%E3%83%83%E3%83%88%202023-02-06%2016.49.53.png)
If you press the button, all of the color will reverses.
![](https://github.com/yutaro741/unit3/blob/main/pictures/%E3%82%B9%E3%82%AF%E3%83%AA%E3%83%BC%E3%83%B3%E3%82%B7%E3%83%A7%E3%83%83%E3%83%88%202023-02-06%2016.49.55.png)
You can get back the color every time.
![](https://github.com/yutaro741/unit3/blob/main/pictures/%E3%82%B9%E3%82%AF%E3%83%AA%E3%83%BC%E3%83%B3%E3%82%B7%E3%83%A7%E3%83%83%E3%83%88%202023-02-06%2016.50.02.png)
