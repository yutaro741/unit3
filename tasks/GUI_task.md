#This is answer of GUI task.

```.py
from kivymd.app import MDApp

class converter(MDApp):
    def __init__(self, **kwargs):
        self.current = "USD"
        super().__init__(**kwargs)
        self.count = 0

    def built(self):
        return

    def set_counter(self):
        get = self.root.ids.user_start_x.text
        get = get.replace(" ", "")
        if get.isdecimal and get != "": #Until here removing strings.
            amount_set = float(get)
            if self.current == "USD":
                self.money = 1.09*amount_set #1.09 is the rate between USA and EUR
            else:
                self.money = 141.34*amount_set #141.34 is the rate between JPY and EUR
            self.money = ('{:.02f}'.format(self.money))
            self.root.ids.dol_label.text = f"{self.money} {self.current}"
        else: #if its not number, say it here.
            self.root.ids.dol_label.text = f"Please enter number"

    def change_current(self, name):
        self.current = name




test = converter()
test.run()
```


File name: converter.kv
```.py
Screen:
    size:500, 500

    MDBoxLayout:
        id:main_box
        orientation: "vertical"
        size_hint: 1, .7
        pos_hint: {"center_x": .5, "center_y":.5}

        MDLabel:
            id: title
            text: "Currency Converter"
            font_size: "56pt"
            orientation: "vertical"
            halign: "center"

        MDTextField:
            id:user_start_x
            hint_text: "Enter an amount in EUR"
            mode: "rectangle"
            size_hint: .99, .7
            pos_hint: {"center_x":.5}

        MDBoxLayout:
            orientation: "horizontal"
            pos_hint:{"center_x": 1.3}
            MDRaisedButton:
                id: USD
                text: "USD"
                pos_hint: {"center_y":.5}
                md_bg_color: "cyan"
                on_press: app.change_current("USD")

            MDRaisedButton:
                id: JPY
                text: "JPY"
                pos_hint: {"center_y":.5}
                md_bg_color: "#D62828"
                on_press: app.change_current("JPY")

        MDChip:
            id: btn
            text: "click to convert"
            pos_hint: {"center_y":.5}
            md_bg_color: "green"
            on_press: app.set_counter()

        MDLabel:
            id: dol_label
            text: ""
            halign: "center"
            font_size: "50pt"

```


![](https://github.com/yutaro741/unit3/blob/main/pictures/%E3%82%B9%E3%82%AF%E3%83%AA%E3%83%BC%E3%83%B3%E3%82%B7%E3%83%A7%E3%83%83%E3%83%88%202023-01-30%2017.45.33.png)
![](https://github.com/yutaro741/unit3/blob/main/pictures/%E3%82%B9%E3%82%AF%E3%83%AA%E3%83%BC%E3%83%B3%E3%82%B7%E3%83%A7%E3%83%83%E3%83%88%202023-01-30%2017.45.45.png)
![](https://github.com/yutaro741/unit3/blob/main/pictures/%E3%82%B9%E3%82%AF%E3%83%AA%E3%83%BC%E3%83%B3%E3%82%B7%E3%83%A7%E3%83%83%E3%83%88%202023-01-30%2017.46.01.png)
![](https://github.com/yutaro741/unit3/blob/main/pictures/%E3%82%B9%E3%82%AF%E3%83%AA%E3%83%BC%E3%83%B3%E3%82%B7%E3%83%A7%E3%83%83%E3%83%88%202023-01-30%2017.47.42.png)
