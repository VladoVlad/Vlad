import tkinter as tk
from tkinter import ttk
import time
import re
import tkinter.messagebox as msg



def is_valid_input(input_str):
    return all(re.match(r'^-?\d*\.?\d*$', x) for x in input_str.split(','))


def validate_input(new_value):
    if new_value == "":
        return True
    try:
        parts = new_value.split(",")
        for part in parts:
            part = part.strip()
            if part and not re.match(r'^-?\d*\.?\d*$', part):
                return False
        return True
    except Exception:
        return False


def sort_sequence():
    try:
        sequence = entry.get()
        if not validate_input(sequence):
            raise ValueError("Неверный формат ввода")
        sequence_parts = sequence.split(",")
        sorted_sequence = []
        for part in sequence_parts:
            part = part.strip()
            if part:
                if '.' in part:
                    sorted_sequence.append(float(part))
                else:
                    sorted_sequence.append(int(part))
        start_time = time.time()
        if sort_combobox.get() == "По возрастанию":
            sorted_sequence.sort()
        elif sort_combobox.get() == "По убыванию":
            sorted_sequence.sort(reverse=True)
        end_time = time.time()
        result_text.delete(1.0, tk.END)
        result_text.insert(tk.END, "Отсортированная последовательность: " + ', '.join(map(str, sorted_sequence)))
        time_taken = end_time - start_time  # время в секундах
        time_label.config(text="Время сортировки: " + "{:.6f}".format(time_taken) + " секунд")
        original_sequence_label.config(text="Введенные цифры: " + entry.get())

        choice = msg.askquestion("Повторить сортировку", "Хотите повторить сортировку?")
        if choice == 'yes':
            entry.delete(0, tk.END)  # очистить поле ввода
        else:
            root.destroy()

    except ValueError as e:
        result_text.delete(1.0, tk.END)
        result_text.insert(tk.END, "Ошибка: " + str(e))
    except Exception as e:
        result_text.delete(1.0, tk.END)
        result_text.insert(tk.END, "Произошла ошибка")


root = tk.Tk()
root.title("Программа сортировки")
root.geometry("1000x1000")

default_font = ("Arial", 24)
root.option_add("*Font", default_font)

note_label = tk.Label(root, text="Введите цифры через запятую:")
note_label.pack()

entry = tk.Entry(root)
entry.pack()

entry['validate'] = 'key'
vcmd = (entry.register(validate_input), '%P')
entry['validatecommand'] = vcmd

sort_combobox = ttk.Combobox(root, values=["По возрастанию", "По убыванию"], state="readonly")
sort_combobox.current(0)
sort_combobox.pack()

start_button = ttk.Button(root, text="Start", command=sort_sequence)
start_button.pack()

result_label = tk.Label(root, text="Результирующий список:")
result_label.pack()

result_text = tk.Text(root, height=5, width=50, wrap="word")
result_text.pack()

time_label = tk.Label(root, text="Время сортировки: ")
time_label.pack()

original_sequence_label = tk.Label(root, text="Введенные цифры: ")
original_sequence_label.pack()

root.mainloop()
