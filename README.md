# Calculator-Using-Tinker-
from tkinter import *

# Create window
root = Tk()
root.title("Python Calculator")
root.geometry("350x500")
root.resizable(False, False)

# Display
expression = ""

entry = Entry(root, font=("Arial", 24), bd=10, relief=RIDGE, justify=RIGHT)
entry.pack(fill=BOTH, ipadx=8, ipady=15, padx=10, pady=10)

# Functions
def press(key):
    global expression
    expression += str(key)
    entry.delete(0, END)
    entry.insert(END, expression)

def clear():
    global expression
    expression = ""
    entry.delete(0, END)

def equal():
    global expression
    try:
        result = str(eval(expression))
        entry.delete(0, END)
        entry.insert(END, result)
        expression = result
    except:
        entry.delete(0, END)
        entry.insert(END, "Error")
        expression = ""

# Buttons
buttons = [
    ('7',1,0), ('8',1,1), ('9',1,2), ('/',1,3),
    ('4',2,0), ('5',2,1), ('6',2,2), ('*',2,3),
    ('1',3,0), ('2',3,1), ('3',3,2), ('-',3,3),
    ('0',4,0), ('.',4,1), ('=',4,2), ('+',4,3),
]

frame = Frame(root)
frame.pack()

for (text, row, col) in buttons:
    if text == "=":
        btn = Button(frame, text=text, width=8, height=3,
                     font=("Arial", 16), command=equal)
    else:
        btn = Button(frame, text=text, width=8, height=3,
                     font=("Arial", 16),
                     command=lambda t=text: press(t))
    btn.grid(row=row, column=col, padx=5, pady=5)

clear_btn = Button(root, text="Clear", font=("Arial",16),
                   command=clear)
clear_btn.pack(fill=BOTH, padx=10, pady=10)

root.mainloop()
