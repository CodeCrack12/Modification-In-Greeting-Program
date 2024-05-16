import tkinter as tk
import webbrowser
from time import strftime
from math import ceil, floor


def get_greeting():
    current_time = strftime("%H:%M:%S")
    if current_time >= "21:00:00":
        return "Good Night."
    elif current_time >= "18:30:00":
        return "Good Evening."
    elif current_time >= "12:00:00":
        return "Good Afternoon."
    elif current_time >= "05:00:00":
        return "Good Morning."
    else:
        return "Good Night."


def display_greeting():
    greeting = get_greeting()
    label.config(text=greeting)


def display_date():
    current_date = strftime("%B %d, %Y (%A)")
    date_label.config(text=current_date)


def display_time():
    current_time = strftime("%H:%M:%S")
    time_label.config(text=current_time)


def open_url(url):
    webbrowser.open(url)


def open_notes():
    notes_window = tk.Toplevel(root)
    notes_window.title("Malicious Scripts.")
    notes_text = """

    Every Kind of Malicious Script Available.
    """
    notes_label = tk.Label(notes_window, text=notes_text, font=("Helvetica", 12), justify=tk.LEFT)
    notes_label.pack()


def open_calculator():
    calculator_window = tk.Toplevel(root)
    calculator_window.title("Calculator")

    def calculate():
        operation = operation_var.get()
        if operation in [1, 2, 3, 4, 5, 6, 7]:
            n1 = int(entry_num1.get())
            n2 = int(entry_num2.get())
            if operation == 1:
                result_label.config(text="Addition: " + str(n1 + n2))
            elif operation == 2:
                result_label.config(text="Subtraction: " + str(n1 - n2))
            elif operation == 3:
                result_label.config(text="Division: " + str(n1 / n2))
            elif operation == 4:
                result_label.config(text="Multiplication: " + str(n1 * n2))
            elif operation == 5:
                result_label.config(text="Floor Division: " + str(n1 // n2))
            elif operation == 6:
                result_label.config(text="Exponent: " + str(n1 ** n2))
            elif operation == 7:
                result_label.config(text="Modulus: " + str(n1 % n2))
        elif operation in [8, 9, 10]:
            number = float(entry_num1.get())
            if operation == 8:
                result_label.config(text="Absolute: " + str(abs(number)))
            elif operation == 9:
                result_label.config(text="Ceil: " + str(ceil(number)))
            elif operation == 10:
                result_label.config(text="Floor: " + str(floor(number)))
        else:
            result_label.config(text="Error.")

    operation_var = tk.IntVar()

    tk.Label(calculator_window, text="Select Operation: ").pack()
    operations = [
        ("Addition", 1), ("Subtraction", 2), ("Division", 3), ("Multiplication", 4),
        ("Floor Division", 5), ("Exponent", 6), ("Modulus", 7), ("Absolute", 8),
        ("Ceil", 9), ("Floor", 10)
    ]
    for text, value in operations:
        tk.Radiobutton(calculator_window, text=text, variable=operation_var, value=value).pack()

    entry_num1 = tk.Entry(calculator_window)
    entry_num1.pack()

    entry_num2 = tk.Entry(calculator_window)
    entry_num2.pack()

    tk.Button(calculator_window, text="Calculate", command=calculate).pack()

    result_label = tk.Label(calculator_window, text="")
    result_label.pack()


# Create the main window
root = tk.Tk()
root.title("Time Greeting App")
root.geometry("400x300")  # Set the window size
root.configure(bg="#f0f0f0")  # Set background color

# Add a friendly hand sticker
hand_sticker = tk.Label(root, text="👋", font=("Arial", 24), bg="#f0f0f0")
hand_sticker.pack(pady=10)

# Create a label for the greeting
label = tk.Label(root, font=("Helvetica", 16), bg="#f0f0f0")
label.pack()

# Create a label for the date
date_label = tk.Label(root, font=("Helvetica", 12), bg="#f0f0f0")
date_label.pack()

# Create a label for the current time
time_label = tk.Label(root, font=("Helvetica", 12), bg="#f0f0f0")
time_label.pack()


# Update the greeting, date, and time every second
def update_labels():
    display_greeting()
    display_date()
    display_time()
    root.after(1000, update_labels)


update_labels()

# Add clickable labels for social media apps
social_media_apps = {
    "Google Chrome": "https://www.google.com",
    "Facebook": "https://www.facebook.com",
    "GitHub": "https://www.github.com",
    "Instagram": "https://www.instagram.com",
    # Add more social media apps here...
}

for app, url in social_media_apps.items():
    link = tk.Label(root, text=app, font=("Helvetica", 12), fg="blue", cursor="hand2", bg="#f0f0f0")
    link.pack(side=tk.LEFT, anchor=tk.W, padx=5, pady=5)
    link.bind("<Button-1>", lambda e, url=url: open_url(url))

# Add a label for the Notes tab
notes_label = tk.Label(root, text="Notes", font=("Helvetica", 12), fg="blue", cursor="hand2", bg="#f0f0f0")
notes_label.pack(side=tk.LEFT, anchor=tk.W, padx=5, pady=5)
notes_label.bind("<Button-1>", lambda e: open_notes())

# Add a label for the Calculator tab
calculator_label = tk.Label(root, text="Calculator", font=("Helvetica", 12), fg="blue", cursor="hand2", bg="#f0f0f0")
calculator_label.pack(side=tk.LEFT, anchor=tk.W, padx=5, pady=5)
calculator_label.bind("<Button-1>", lambda e: open_calculator())

# Run the GUI event loop
root.mainloop()
