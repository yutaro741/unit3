This is the answer of quiz 42.

Python file.
```.py
from kivymd.app import MDApp
from kivymd.uix.screen import MDScreen

#Each time I press the messagen button, messeage will printed to the main page.
class MysterypageA(MDScreen):
    def message1(self):
        print("This is mystery page A you pressed the button")

class MysterypageB(MDScreen):
    def message2(self):
        print("This is mystery page B you pressed the button")

class quiz42(MDApp):
    def built(self):
        return

test = quiz42()
test.run()
```


kivy file:
```.py
ScreenManager:
    MysterypageA:
        name: "MysterypageA"
    MysterypageB:
        name: "MysterypageB"

<MysterypageA>:#MysterypageA screen. 

    MDLabel:
        id:page
        text:"mystery box page A"
        font_size: "64pt"
    MDBoxLayout:
        size_hint: 1, .2
        MDRaisedButton:
            id:button1
            text: "message"
            on_press:root.message1() #if pressed, message1() function will run.
            size_hint:.5, 1
        MDRaisedButton:
            id:gotoB
            text:"Go to B"
            on_press:root.parent.current = "MysterypageB" #If pressed, page will change to B.
            size_hint:.5, 1


<MysterypageB>:#Mostly same with A.
    MDLabel:
        id:page
        text:"mystery box page B"
        font_size: "64pt"
    MDBoxLayout:
        size_hint: 1, .2
        MDRaisedButton:
            id:button2
            text: "message"
            on_press:root.message2()
            size_hint:.5, 1
        MDRaisedButton:
            id:gotoA
            text:"Go to A"
            on_press:root.parent.current = "MysterypageA"
            size_hint:.5, 1
```
## Output:
Initial picture. If you press the message box, message "This is mystery page A you pressed the button" will appeare.
![](https://github.com/yutaro741/unit3/blob/main/pictures/Screen%20Shot%202023-03-26%20at%2015.06.22.png)
If you press Go to B button, it will change to this picture. If you press the message box, message "This is mystery page B you pressed the button" will appeare.
If you press the Go to A button, it screen will go back to top picture's one.
![](https://github.com/yutaro741/unit3/blob/main/pictures/Screen%20Shot%202023-03-26%20at%2015.06.39.png)
