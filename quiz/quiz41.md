# This is the answer of quiz41. I put so much effort on this quiz, so I hope I can get additional score/advice from here.


## Standard quiz - GUI, decision of victory or defeat

Kivy code-
```.py
Screen:
    size:500, 500
    MDBoxLayout:
        id:main_box
        orientation: "vertical"
        size_hint: .7, .8
        pos_hint: {"center_x": .5, "center_y":.5}

        MDLabel:
            id: title
            text: "Yellow's turn"
            halign: "center"
            valign: "top"
            size_hint:1, .2
            font_size: 60

        MDBoxLayout:
            #The 9 boxes is made by 3box horiozntally × 3 box vertically.
            #Each box has an id named boxN (N=0,1,2,...8), and each time they pressed, the number of the button is send to python program.
            id:top_box
            orientation: "horizontal"
            pos_hint: {"center_x": .5, "center_y":.5}

            MDRaisedButton:
                id:box0
                text:""
                md_bg_color: "#DDFFDD"
                size_hint: .3, 1
                on_press: app.changecolor(0)
            MDRaisedButton:
                id:box1
                text:""
                md_bg_color: "#DDFFDD"
                size_hint: .3, 1
                on_press: app.changecolor(1)
            MDRaisedButton:
                id:box2
                text:""
                md_bg_color: "#DDFFDD"
                size_hint: .3, 1
                on_press: app.changecolor(2)
        MDBoxLayout:
            MDRaisedButton:
                id:box3
                text:""
                md_bg_color: "#DDFFDD"
                size_hint: .3, 1
                on_press: app.changecolor(3)
            MDRaisedButton:
                id:box4
                text:""
                md_bg_color: "#DDFFDD"
                size_hint: .3, 1
                on_press: app.changecolor(4)
            MDRaisedButton:
                id:box5
                text:""
                md_bg_color: "#DDFFDD"
                size_hint: .3, 1
                on_press: app.changecolor(5)
        MDBoxLayout:
            MDRaisedButton:
                id:box6
                text:""
                md_bg_color: "#DDFFDD"
                size_hint: .3, 1
                on_press: app.changecolor(6)
            MDRaisedButton:
                id:box7
                text:""
                md_bg_color: "#DDFFDD"
                size_hint: .3, 1
                on_press: app.changecolor(7)
            MDRaisedButton:
                id:box8
                text:""
                md_bg_color: "#DDFFDD"
                size_hint: .3, 1
                on_press: app.changecolor(8)

    MDBoxLayout:#The button that can do the best hand in that situation.
        MDRaisedButton:
            id:cheating
            text:"Best Hand"
            on_press: app.AIhand()
        MDRaisedButton:#The button to reset everything.
            id:reset
            text:"reset"
            on_press: app.reset()
```

python code-
```.py
from kivymd.app import MDApp
import random


boxes = ["box0", "box1", "box2", "box3", "box4", "box5", "box6", "box7", "box8"]
counts = ["0", "×"]
color = ["yellow", "red"]
textcolor = ["black", "white"]
text = ["Red's turn", "Yellow's turn"]

class quiz41(MDApp):
    def __init__(self, **kwargs):
        super().__init__(**kwargs)
        self.count = 0 #This count will find out which turn it is.
        self.state = True #This will find out the game is set/over or doing yet.

    def built(self):
        return

    def changecolor(self, num): #This function runs when the grid is selected
        if self.root.ids[boxes[num]].text == "" and self.state:#Runs only when grid is not selected yet and game is not set.
            self.root.ids[boxes[num]].text = counts[self.count]#Change the text on the grid selected.
            self.root.ids[boxes[num]].md_bg_color = color[self.count]
            self.root.ids[boxes[num]].text_color = textcolor[self.count]#Change the color on the grid selected.
            self.root.ids.title.text = text[self.count]#Change the title to tell which turn it is.
            self.count = (self.count + 1) % 2 #Change the turn to the next place.
            self.winner()

    def winner(self):#Find out the game is over or not each time grid selected.
        a = []
        for i in boxes:
            side = self.root.ids[i].text
            if side == "":
                a.append(0)
            if side == "0":
                a.append(1)
            if side == "×":
                a.append(-1)
        #Make the list of the data. yellow side = 1, red side = -1, and blank = 0.
        horizontal = [[a[0], a[1], a[2]], [a[3], a[4], a[5]], [a[6], a[7], a[8]]]
        vertical = [[a[0], a[3], a[6]], [a[1], a[4], a[7]], [a[2], a[5], a[8]]]
        diagonal = [[a[0], a[4], a[8]], [a[2], a[4], a[6]]]
        for j in [horizontal, vertical, diagonal]:
            for i in range(len(j)):
                if sum(j[i]) == 3:
                    print("Winner ○")
                    self.state = False
                    self.root.ids.title.text = "Winner Yellow"
                    return 1
                elif sum(j[i]) == -3:
                    print("Winner ×")
                    self.state = False
                    self.root.ids.title.text = "Winner Red"
                    return -1
        #If there are three consecutive rows of the same color, determine the winner, change the text, and make sure that it cannot be selected again.
        if a.count(0) == 0:
            self.state = False
            self.root.ids.title.text = "Draw"
            return 0
        #If the grid is all selected, show the text as draw.

        state = True
        for j in [horizontal, vertical, diagonal]:
            for i in j:
                if i.count(0) == 2:
                    state = False
                num0 = 0
                numpm = 0
                for l in i:
                    num0 += abs(l)
                    numpm += l
                if num0 == 0 or numpm == -2 or numpm == 2:
                    state = False
        if state:
            print("draw")
            self.root.ids.title.text = "Draw"
            return
        #If the game is absolutely tied even if it continues in the future, only text is displayed to allow the game to continue.

    def reset(self):#This will happen when reset button is pressed.
        for i in boxes:
            self.root.ids[i].text = ""
            self.root.ids[i].md_bg_color = "#DDFFDD"
            #Reset all of the text and color.
        self.count = 0
        self.state = True#Let it play again.
        self.root.ids.title.text = "Yellow's turn"
        
test = quiz41()
test.run()
```

The initial screen is like this.
![](https://github.com/yutaro741/unit3/blob/main/pictures/Screen%20Shot%202023-03-25%20at%201.43.42.png)
Each time people touch the grid, the color and text will chahge. Title will change as "" turn. 
Nothing will happen when same place is choosed.
![](https://github.com/yutaro741/unit3/blob/main/pictures/Screen%20Shot%202023-03-25%20at%201.43.57.png)
If Vertical, horizontal or diagonal is get into same color, title shows winner "" and be unale to change other grid anymore.
![](https://github.com/yutaro741/unit3/blob/main/pictures/Screen%20Shot%202023-03-25%20at%201.44.05.png)
If reset button is pressed, everything will be reseted.
![](https://github.com/yutaro741/unit3/blob/main/pictures/Screen%20Shot%202023-03-25%20at%201.43.42.png)


## Advanced things-The best move
Those things are the basic things that is requred in the quiz. I did some of the advanced things, that do the best move in each situation. 
The below is the python code.
Because I am used to Japanese English, "One more to go" is expressed as "reach".
```.py
    def AIhand(self):
        if self.state:
            hand = self.besthand()
            self.changecolor(hand)

    def besthand(self):
        turn = self.count
        all = []
        for i in boxes:
            side = self.root.ids[i].text
            if side == "":
                all.append(0)
            if side == "0":
                if turn == 0:
                    all.append(1)
                else:
                    all.append(-1)
            if side == "×":
                if turn == 0:
                    all.append(-1)
                else:
                    all.append(1)
        #Make the list that shows my grid=1, opponent's grid=-1, and free grid = 0
        a1, a2, a3, b1, b2, b3, c1, c2, c3 = all[0],all[1],all[2],all[3],all[4],all[5],all[6],all[7],all[8]
        #Make it a1, a2, ... to just be easy to do codings.
        num = 9 - all.count(0)  #num will show the number that is filled.

        #---
        #This is how to play a hand in a special state. If the board is not in a special state, it moves to the following state.
        if num == 0 or (num == 1 and b2 == 0):
            return 4
        if num == 1 and b2 != 0:
            return random.choice([0, 2, 6, 8])
        if num == 2 and b2 == 1 and a1 + a3 + c1 + c3 == -1:
            return random.choice([1, 3, 5, 7])
        if num == 2 and a2==b1==b3==c2==0:
            if a1==c3==0 or a3==c1==0:
                return [a1, 3, a3, 3, 3, 3, c1, 3, c3].index(0)
            else:
                a = all.index(-1)
                b = all.index(1)
                blist = [[(b // 3) * 3 + (b + 1) % 3, (b // 3) * 3 + (b + 2) % 3], [(b + 3) % 9, (b + 6) % 9]]
                for j in blist:
                    for k in range(2):
                        i=j[k]
                        if (i==1 or i==3 or i==5 or i==7) and j[(k+1)%2] != a:
                            return i
        if num == 2 and a1+a3+c1+c3 == -1 and a2+b1+b3+c2 == 1 and [a1+a2+a3, a3+b3+c3, c1+c2+c3, a1+b1+c1].count(0) == 1:
            a = all.index(-1)
            b = all.index(1)
            for i in [(a//3)*3+(a+1)%3, (a//3)*3+(a+2)%3, (a+3)%9, (a+6)%9]:
                for j in [(b//3)*3+(b+1)%3, (b//3)*3+(b+2)%3, (b+3)%9, (b+6)%9]:
                    if i == j and (i == 0 or i == 2 or i == 6 or i == 8):
                        return i
        #---
        #The things below is the program that If you have a reach, complete a row; otherwise if your opponent has a reach, fill it.

        horizontal = [[a1, a2, a3], [b1, b2, b3], [c1, c2, c3]]
        vertical = [[a1, b1, c1], [a2, b2, c2], [a3, b3, c3]]
        diagonal = [[a1, b2, c3], [a3, b2, c1]]
        for i in range(len(horizontal)):
            if sum(horizontal[i]) == 2:
                return 3 * i + horizontal[i].index(0)
        for i in range(len(vertical)):
            if sum(vertical[i]) == 2:
                return vertical[i].index(0)*3 + i
        for i in range(len(diagonal)):
            if sum(diagonal[i]) == 2:
                if i == 0:
                    return diagonal[i].index(0)*4
                else:
                    return diagonal[i].index(0)*2 + 2
        for i in range(len(horizontal)):
            if sum((horizontal[i])) == -2:
                return 3 * i + horizontal[i].index(0)
        for i in range(len(vertical)):
            if sum((vertical[i])) == -2:
                return vertical[i].index(0)*3 + i
        for i in range(len(diagonal)):
            if sum((diagonal[i])) == -2:
                if i == 0:
                    return diagonal[i].index(0)*4
                else:
                    return diagonal[i].index(0)*2 + 2
        #---
        #If you are in a position to double reach, you will reach. If not, it prevents the place from becoming double reach.

        score = [0, 0, 0, 0, 0, 0, 0, 0, 0]
        for i in range(len(horizontal)):
            if sum(horizontal[i]) == 1 and horizontal[i].count(0) != 0:
                for j in range(3):
                    if horizontal[i][j] == 0:
                        score[3 * i + j] += 1
        for i in range(len(vertical)):
            if sum(vertical[i]) == 1 and vertical[i].count(0) != 0:
                for j in range(3):
                    if vertical[i][j] == 0:
                        score[i + 3 * j] += 1
        for i in range(len(diagonal)):
            if sum(diagonal[i]) == 1 and diagonal[i].count(0) != 0:
                if i == 0:
                    for j in range(3):
                        if diagonal[i][j] == 0:
                            score[j * 4] += 1
                else:
                    for j in range(3):
                        if diagonal[i][j] == 0:
                            score[j * 2 + 2] += 1

        if score.count(2) > 0:
            return score.index(2)


        n_score = [0,0,0,0,0,0,0,0,0]
        for i in range(len(horizontal)):
            if sum(horizontal[i]) == -1 and horizontal[i].count(0) != 0:
                for j in range(3):
                    if horizontal[i][j] == 0:
                        n_score[3 * i + j] += 1
        for i in range(len(vertical)):
            if sum(vertical[i]) == -1 and vertical[i].count(0) != 0:
                for j in range(3):
                    if vertical[i][j] == 0:
                        n_score[i + 3 * j] += 1
        for i in range(len(diagonal)):
            if sum(diagonal[i]) == -1 and diagonal[i].count(0) != 0:
                if i == 0:
                    for j in range(3):
                        if diagonal[i][j] == 0:
                            n_score[j*4] += 1
                else:
                    for j in range(3):
                        if diagonal[i][j] == 0:
                            n_score[j*2+2] += 1
        if n_score[4] == 2:
            return 4
        if n_score.count(2) > 0:
            return n_score.index(2)

        #---
        #If none of them can double reach or be double reach'd, the hand that will be reach'd is chosen at random.

        point = [0,0,0,0,0,0,0,0,0]
        for i in range(len(horizontal)):
            if sum(horizontal[i]) == 1 and horizontal[i].count(0) != 0:
                point[3*i+horizontal[i].index(0)] += 1
        for i in range(len(vertical)):
            if sum(vertical[i]) == 1 and vertical[i].count(0) != 0:
                point[vertical[i].index(0)*3 + i] += 1
        for i in range(len(diagonal)):
            if sum(diagonal[i]) == 1 and diagonal[i].count(0) != 0:
                if i == 0:
                    point[diagonal[i].index(0)*4] += 1
                else:
                    point[diagonal[i].index(0)*2 + 2] += 1

        if b2 == 0:
            return 4

        if point.count(0) != 9:
            return random.choice([i for i, x in enumerate(point) if x == max(point)])

        #---
        #If there is no hand to reach, the player chooses one of the empty squares.

        empty = []
        for i in range(9):
            if all[i] == 0:
                empty.append(i)
        return random.choice(empty)
```

Basic move-In order of priority.
①If I am reaching, program will just go to win.
![](https://github.com/yutaro741/unit3/blob/main/pictures/Screen%20Shot%202023-03-25%20at%202.18.43.png)
Best hand button will move as following.
![](https://github.com/yutaro741/unit3/blob/main/pictures/Screen%20Shot%202023-03-25%20at%202.18.53.png)

②If opponent are reaching program will just go to block.
--Photos omitted.

③If I am able to let double reach, just do that.
![](https://github.com/yutaro741/unit3/blob/main/pictures/Screen%20Shot%202023-03-25%20at%202.22.55.png)
Best hand button will move as following. There is double reach(bottom row and diagonal) so you can defenetly win in next turn.
![](https://github.com/yutaro741/unit3/blob/main/pictures/Screen%20Shot%202023-03-25%20at%202.23.22.png)
