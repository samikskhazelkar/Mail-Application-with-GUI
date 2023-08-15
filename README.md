# Mail-Application-with-GUI
import tkinter as tk
from tkinter import messagebox
import smtplib

class EmailApp:
    def __init__(self, root):
        self.root = root
        self.root.title("Email Application")

        self.setup_gui()

    def setup_gui(self):
        self.to_label = tk.Label(self.root, text="To:")
        self.to_label.pack()
        self.to_entry = tk.Entry(self.root)
        self.to_entry.pack()

        self.subject_label = tk.Label(self.root, text="Subject:")
        self.subject_label.pack()
        self.subject_entry = tk.Entry(self.root)
        self.subject_entry.pack()

        self.message_label = tk.Label(self.root, text="Message:")
        self.message_label.pack()
        self.message_text = tk.Text(self.root)
        self.message_text.pack()

        self.send_button = tk.Button(self.root, text="Send", command=self.send_email)
        self.send_button.pack()

    def send_email(self):
        to_address = self.to_entry.get()
        subject = self.subject_entry.get()
        message = self.message_text.get("1.0", "end")

        try:
            # Replace with your email and app-specific password
            smtp_server = "smtp.gmail.com"
            port = 587
            sender_email = "your_email@gmail.com"
            password = "your_app_specific_password"

            with smtplib.SMTP(smtp_server, port) as server:
                server.starttls()
                server.login(sender_email, password)

                full_message = f"Subject: {subject}\n\n{message}"
                server.sendmail(sender_email, to_address, full_message)

            messagebox.showinfo("Success", "Email sent successfully!")
        except Exception as e:
            messagebox.showerror("Error", f"An error occurred:\n{str(e)}")

if __name__ == "__main__":
    root = tk.Tk()
    app = EmailApp(root)
    root.mainloop()
