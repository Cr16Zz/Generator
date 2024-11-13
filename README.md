import tkinter as tk
import random
import string


def generate_password(length, use_lowercase, use_digits, use_special):
    characters = ""

    if use_lowercase:
        characters += string.ascii_lowercase  # [a-z]
    if use_digits:
        characters += string.digits  # [0-9]
    if use_special:
        characters += "!@#$%"  # Специальные символы

    if characters:
        return ''.join(random.choice(characters) for _ in range(length))
    else:
        return "Выберите хотя бы один тип символов"


def on_generate():
    length = int(length_entry.get())
    use_lowercase = lowercase_var.get()
    use_digits = digits_var.get()
    use_special = special_var.get()

    password = generate_password(length, use_lowercase, use_digits, use_special)
    password_var.set(password)


# Создание основного окна
root = tk.Tk()
root.title("Ваш пароль")

# Переменные для хранения состояний чекбоксов
lowercase_var = tk.BooleanVar(value=True)
digits_var = tk.BooleanVar(value=True)
special_var = tk.BooleanVar(value=True)

# Виджеты интерфейса
length_label = tk.Label(root, text="Длина пароля:")
length_label.pack()

length_entry = tk.Entry(root)
length_entry.pack()
length_entry.insert(0, "8")  # Значение по умолчанию

lowercase_checkbox = tk.Checkbutton(root, text="добавить алфавит нижнего регистра [a-z]", variable=lowercase_var)
lowercase_checkbox.pack()


digits_checkbox = tk.Checkbutton(root, text="добавить цифры [0-9]", variable=digits_var)
digits_checkbox.pack()

special_checkbox = tk.Checkbutton(root, text="добавить спецсимволы [! @ # $ %]", variable=special_var)
special_checkbox.pack()

generate_button = tk.Button(root, text="Сгенерировать пароль", command=on_generate)
generate_button.pack()

password_label = tk.Label(root, text="Готовый пароль:")
password_label.pack()

password_var = tk.StringVar()
password_display = tk.Entry(root, textvariable=password_var, state='readonly', width=30)
password_display.pack()

# Запуск основного цикла
root.mainloop()
