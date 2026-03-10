import tkinter as tk
from tkinter import messagebox
import csv
import os
from datetime import datetime
import matplotlib.pyplot as plt


class CoalMineSystem:

    def __init__(self):
        self.window = tk.Tk()
        self.window.title("Coal Mine Productivity and Safety Management System")

        self.username = "admin"
        self.password = "password"

        tk.Label(self.window, text="Login", font=("Arial",16)).pack(pady=10)

        tk.Label(self.window, text="Username").pack()
        self.username_entry = tk.Entry(self.window)
        self.username_entry.pack()

        tk.Label(self.window, text="Password").pack()
        self.password_entry = tk.Entry(self.window, show="*")
        self.password_entry.pack()

        tk.Button(self.window, text="Login",
                  command=self.check_credentials).pack(pady=10)

        self.window.mainloop()


    def check_credentials(self):
        if (self.username_entry.get() == self.username and
            self.password_entry.get() == self.password):

            self.window.destroy()
            self.main_window()

        else:
            messagebox.showerror("Error", "Invalid Credentials")


    def main_window(self):

        self.window = tk.Tk()
        self.window.title("Coal Mine Dashboard")

        tk.Label(self.window, text="Employee Name").pack()
        self.employee_entry = tk.Entry(self.window)
        self.employee_entry.pack()

        tk.Label(self.window, text="Mine Name").pack()
        self.mine_entry = tk.Entry(self.window)
        self.mine_entry.pack()

        tk.Label(self.window, text="Production Data").pack()
        self.production_entry = tk.Entry(self.window)
        self.production_entry.pack()

        tk.Label(self.window, text="Safety Incidents").pack()
        self.safety_entry = tk.Entry(self.window)
        self.safety_entry.pack()

        tk.Button(self.window, text="Submit Data",
                  command=self.save_data).pack(pady=5)

        tk.Button(self.window, text="Emergency Alert",
                  command=self.trigger_alert).pack(pady=5)

        tk.Button(self.window, text="Show Production Graph",
                  command=self.show_graph).pack(pady=5)

        tk.Button(self.window, text="Show Saved Data",
                  command=self.show_data).pack(pady=5)

        self.window.mainloop()


    def trigger_alert(self):
        messagebox.showwarning("Emergency", "Emergency Alert Triggered!")


    def save_data(self):

        employee = self.employee_entry.get()
        mine = self.mine_entry.get()
        production = self.production_entry.get()
        safety = self.safety_entry.get()
        time = datetime.now().strftime("%Y-%m-%d %H:%M:%S")

        if employee == "" or mine == "" or production == "" or safety == "":
            messagebox.showerror("Error", "All fields required")
            return

        file_exists = os.path.isfile("mine_data.csv")

        with open("mine_data.csv", "a", newline="") as file:
            writer = csv.writer(file)

            if not file_exists:
                writer.writerow(["Employee","Mine","Production","Safety","Time"])

            writer.writerow([employee, mine, production, safety, time])

        if int(safety) > 0:
            messagebox.showwarning("Safety Warning",
                                   "Safety incident reported!")

        messagebox.showinfo("Success", "Data Saved Successfully")

        self.employee_entry.delete(0, tk.END)
        self.mine_entry.delete(0, tk.END)
        self.production_entry.delete(0, tk.END)
        self.safety_entry.delete(0, tk.END)


    def show_graph(self):

        mines = []
        production = []

        try:
            with open("mine_data.csv","r") as file:
                reader = csv.reader(file)
                next(reader)

                for row in reader:
                    mines.append(row[1])
                    production.append(int(row[2]))

            plt.bar(mines, production)
            plt.title("Coal Mine Production")
            plt.xlabel("Mine")
            plt.ylabel("Production")
            plt.show()

        except:
            messagebox.showerror("Error", "No Data Available")


    def show_data(self):

        try:
            data_window = tk.Toplevel(self.window)
            data_window.title("Saved Mine Data")

            text_box = tk.Text(data_window, width=80, height=20)
            text_box.pack()

            with open("mine_data.csv","r") as file:
                reader = csv.reader(file)

                for row in reader:
                    line = " | ".join(row) + "\n"
                    text_box.insert(tk.END, line)

        except:
            messagebox.showerror("Error", "No Data Found")


if __name__ == "__main__":
    CoalMineSystem()
