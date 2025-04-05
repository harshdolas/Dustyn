import tkinter as tk
from tkinter import filedialog, messagebox

def reverse_characters(text):
    return text[::-1]

def reverse_words(text):
    return ' '.join(text.split()[::-1])

def save_to_file(content):
    filename = filedialog.asksaveasfilename(defaultextension=".txt",
                                             filetypes=[("Text Files", "*.txt")])
    if filename:
        with open(filename, 'w') as file:
            file.write(content)
        messagebox.showinfo("Success", "Reversed text saved successfully.")

# GUI Setup
def run_gui():
    def perform_action():
        input_text = entry.get("1.0", tk.END).strip()
        if not input_text:
            messagebox.showerror("Error", "Please enter some text.")
            return

        if choice.get() == "characters":
            result = reverse_characters(input_text)
        else:
            result = reverse_words(input_text)

        output.delete("1.0", tk.END)
        output.insert(tk.END, result)

    def save_output():
        content = output.get("1.0", tk.END).strip()
        if content:
            save_to_file(content)
        else:
            messagebox.showerror("Error", "No output to save.")

    window = tk.Tk()
    window.title("Text Reverser")

    tk.Label(window, text="Enter your text:").pack()
    entry = tk.Text(window, height=5, width=50)
    entry.pack()

    choice = tk.StringVar(value="characters")
    tk.Radiobutton(window, text="Reverse Characters", variable=choice, value="characters").pack()
    tk.Radiobutton(window, text="Reverse Words", variable=choice, value="words").pack()

    tk.Button(window, text="Reverse", command=perform_action).pack(pady=5)
    tk.Label(window, text="Reversed Output:").pack()
    output = tk.Text(window, height=5, width=50)
    output.pack()

    tk.Button(window, text="Save to File", command=save_output).pack(pady=5)

    window.mainloop()

# Run GUI
if __name__ == "__main__":
    run_gui()
