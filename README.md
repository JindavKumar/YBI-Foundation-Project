# YBI-Foundation-Project


import datetime
import os
import tkinter as tk

def create_directory(directory_name):
    if not os.path.exists(directory_name):
        os.mkdir(directory_name)

def save_entry():
    current_date_time = datetime.datetime.now()
    directory_name = current_date_time.strftime('%Y-%m-%d')
    create_directory(directory_name)  # Ensure directory exists
    
    file_name = current_date_time.strftime('%H-%M-%S') + '.txt'  # Just time to avoid long filenames
    file_path = os.path.join(directory_name, file_name)

    entry = text_entry.get('1.0', 'end-1c')
    with open(file_path, 'w', encoding='utf-8') as file:
        file.write(entry)

# GUI setup
root = tk.Tk()
root.title('Diary')

text_entry = tk.Text(root, height=20, width=50)
text_entry.pack(padx=10, pady=10)

save_button = tk.Button(root, text='Save', command=save_entry)
save_button.pack(pady=(0, 5))

quit_button = tk.Button(root, text='Quit', command=root.quit)
quit_button.pack()

# Create today's directory at startup
today = datetime.date.today().strftime('%Y-%m-%d')
create_directory(today)

root.mainloop()
