# PyBot-GUI-Chatbot
PyBot is a GUI-based chatbot built using Python and Tkinter. It responds to user queries like time, date, jokes, and basic greetings using simple keyword matching. This beginner-friendly project showcases interactive GUI design with no external libraries.
import tkinter as tk
import random
import datetime

# Function to get chatbot's response
def get_bot_response(user_input):
    user_input = user_input.lower()

    if "time" in user_input:
        return "🕒 The current time is " + datetime.datetime.now().strftime("%I:%M %p")

    elif "date" in user_input:
        return "📅 Today's date is " + datetime.datetime.now().strftime("%B %d, %Y")

    elif "joke" in user_input:
        jokes = [
            "Why do Python programmers wear glasses? Because they can't C.",
            "Why did the developer go broke? Because they used up all their cache.",
            "How many programmers does it take to change a light bulb? None. It’s a hardware problem.",
        ]
        return random.choice(jokes)

    elif "your name" in user_input:
        return "🤖 My name is PyBot — your GUI chatbot."

    elif "bye" in user_input:
        return "👋 Goodbye! Have a great day."

    else:
        return "🤖 I don't understand that. Try asking about time, date, or jokes!"

# Function to handle sending user input
def send_message():
    user_text = entry.get()
    if user_text.strip() == "":
        return

    chat_window.insert(tk.END, "You: " + user_text + "\n", "user")
    response = get_bot_response(user_text)
    chat_window.insert(tk.END, "PyBot: " + response + "\n", "bot")
    entry.delete(0, tk.END)

    if "bye" in user_text.lower():
        entry.config(state="disabled")
        send_button.config(state="disabled")

# GUI setup
root = tk.Tk()
root.title("PyBot - GUI ChatBot")
root.geometry("500x500")

chat_window = tk.Text(root, bg="white", fg="black", font=("Arial", 12))
chat_window.pack(padx=10, pady=10, fill=tk.BOTH, expand=True)
chat_window.tag_config("user", foreground="blue")
chat_window.tag_config("bot", foreground="green")
chat_window.config(state="normal")

entry_frame = tk.Frame(root)
entry_frame.pack(padx=10, pady=5, fill=tk.X)

entry = tk.Entry(entry_frame, font=("Arial", 12))
entry.pack(side=tk.LEFT, fill=tk.X, expand=True, padx=(0, 10))

send_button = tk.Button(entry_frame, text="Send", command=send_message, font=("Arial", 12))
send_button.pack(side=tk.RIGHT)

entry.bind("<Return>", lambda event: send_message())

# Start the GUI loop
root.mainloop()
