# codsoft_taskno1
import tkinter as tk
from tkinter import messagebox, simpledialog
from tkinter import scrolledtext
class ToDoList:
    def __init__(self, root):
        self.root = root
        self.root.title("To-Do List Application")
        self.tasks = []
        self.task_label = tk.Label(root, text="Task:")
        self.task_label.grid(row=0, column=0)
        self.task_entry = tk.Entry(root)
        self.task_entry.grid(row=0, column=1)
        self.add_button = tk.Button(root, text="Add Task", command=self.add_task)
        self.add_button.grid(row=1, column=0, columnspan=2)
        self.view_button = tk.Button(root, text="View Tasks", command=self.view_tasks)
        self.view_button.grid(row=2, column=0, columnspan=2)
        self.update_button = tk.Button(root, text="Update Task", command=self.update_task)
        self.update_button.grid(row=3, column=0, columnspan=2)
        self.delete_button = tk.Button(root, text="Delete Task", command=self.delete_task)
        self.delete_button.grid(row=4, column=0, columnspan=2)
    def add_task(self):
        task = self.task_entry.get()
        if task:
            self.tasks.append(task)
            self.task_entry.delete(0, tk.END)
            messagebox.showinfo("Success", "Task added successfully!")
        else:
            messagebox.showerror("Error", "Task cannot be empty.")
    def view_tasks(self):
        if self.tasks:
            view_window = tk.Toplevel(self.root)
            view_window.title("View Tasks")
            view_text = scrolledtext.ScrolledText(view_window, width=40, height=10)
            view_text.pack()
            for task in self.tasks:
                view_text.insert(tk.END, task + '\n')
        else:
            messagebox.showinfo("Info", "No tasks to display.")
    def update_task(self):
        if self.tasks:
            task_to_update = simpledialog.askstring("Update Task", "Enter the task to update:")
            if task_to_update in self.tasks:
                new_task = simpledialog.askstring("Update Task", "Enter the new task:")
                if new_task:
                    index = self.tasks.index(task_to_update)
                    self.tasks[index] = new_task
                    messagebox.showinfo("Success", "Task updated successfully!")
            else:
                messagebox.showerror("Error", "Task not found.")
    def delete_task(self):
        if self.tasks:
            task_to_delete = simpledialog.askstring("Delete Task", "Enter the task to delete:")
            if task_to_delete in self.tasks:
                self.tasks.remove(task_to_delete)
                messagebox.showinfo("Success", "Task deleted successfully!")
            else:
                messagebox.showerror("Error", "Task not found.")
root = tk.Tk()
app = ToDoList(root)
root.mainloop()
