import tkinter as tk
from tkinter import messagebox

root = tk.Tk()
root.title("Calculator")
root.geometry("400x500")

display = tk.Entry(root, font=('Arial', 20), borderwidth=5, relief='ridge')
display.grid(row=0, column=0, columnspan=4, padx=10, pady=10)

def button_click(value):
    current_text = display.get()
    display.delete(0, tk.END)
    display.insert(0, current_text + value)

def clear_display():
    display.delete(0, tk.END)

def calculate():
    try:
        result = eval(display.get())
        display.delete(0, tk.END)
        display.insert(0, str(result))
    except Exception as e:
        messagebox.showerror("Error", "Invalid Input")
        clear_display()

button_texts = [
    '7', '8', '9', '/', 
    '4', '5', '6', '*', 
    '1', '2', '3', '-', 
    '0', '.', '=', '+'
]

row = 1
col = 0

for text in button_texts:
    if text == '=':
        button = tk.Button(root, text=text, font=('Arial', 20), command=calculate)
    else:
        button = tk.Button(root, text=text, font=('Arial', 20), command=lambda t=text: button_click(t))

    button.grid(row=row, column=col, ipadx=10, ipady=10, sticky='nsew')
    col += 1
    if col > 3:
        col = 0
        row += 1

root.mainloop()
