from tkinter import *
from tkinter.filedialog import asksaveasfilename, askopenfilename

# Create a window
root = Tk()
root.title("Notepad")

# Create a text area
text_area = Text(root, font=("Helvetica", 16))
text_area.pack(expand=True, fill=BOTH)

# Create a menu bar
menu_bar = Menu(root)

# Create a file menu
file_menu = Menu(menu_bar, tearoff=0)

# Add "New" option to file menu
def new_file():
    text_area.delete(1.0, END)
file_menu.add_command(label="New", command=new_file)

# Add "Open" option to file menu
def open_file():
    file_path = askopenfilename(defaultextension=".txt", filetypes=[("Text Files", "*.txt"), ("All Files", "*.*")])
    if file_path:
        text_area.delete(1.0, END)
        with open(file_path, "r") as file:
            text_area.insert(1.0, file.read())
file_menu.add_command(label="Open", command=open_file)

# Add "Save" option to file menu
def save_file():
    file_path = asksaveasfilename(defaultextension=".txt", filetypes=[("Text Files", "*.txt"), ("All Files", "*.*")])
    if file_path:
        with open(file_path, "w") as file:
            file.write(text_area.get(1.0, END))
file_menu.add_command(label="Save", command=save_file)

# Add "Exit" option to file menu
file_menu.add_separator()
file_menu.add_command(label="Exit", command=root.quit)

# Add file menu to menu bar
menu_bar.add_cascade(label="File", menu=file_menu)

# Add menu bar to window
root.config(menu=menu_bar)

# Run the window  
root.mainloop()
