# Проект "Работа с файлами"

Этот проект представляет собой простое приложение на Python с использованием библиотеки Tkinter для создания графического интерфейса. Приложение позволяет пользователю создавать текстовые файлы с случайными числами и читать эти файлы для вычисления среднего значения чисел.

## Основные функции:
1. **Создание файла с числами**:
   - Пользователь может создать текстовый файл, содержащий 10 случайных чисел в диапазоне от 1 до 100.
   - Файл сохраняется в указанное пользователем место.

2. **Чтение файла и вычисление среднего значения**:
   - Пользователь может выбрать текстовый файл для чтения.
   - Приложение читает числа из файла и вычисляет их среднее значение.
   - Результаты отображаются в интерфейсе приложения.

## Инструкция по запуску

1. **Установка необходимых библиотек**:
   - Убедитесь, что у вас установлен Python.
   - Библиотека Tkinter входит в стандартную поставку Python, поэтому дополнительная установка не требуется.

2. **Создание и запуск проекта**:
   - Создайте новый файл с расширением `.py` (например, `file_operations.py`).
   - Скопируйте и вставьте предоставленный код в этот файл.
   - Сохраните файл.
   - Откройте терминал или командную строку.
   - Перейдите в директорию, где находится ваш файл `file_operations.py`.
   - Запустите приложение, выполнив команду:
     ```sh
     python file_operations.py
     ```

3. **Использование приложения**:
   - После запуска приложения откроется окно с двумя кнопками:
     - **Создать файл с числами**: Нажмите эту кнопку, чтобы создать новый текстовый файл с 10 случайными числами. Выберите место для сохранения файла.
     - **Прочитать файл и вычислить среднее**: Нажмите эту кнопку, чтобы выбрать текстовый файл для чтения. Приложение прочитает числа из файла и вычислит их среднее значение, отобразив результаты в интерфейсе.

## Код проекта

```python
import tkinter as tk
from tkinter import filedialog
import random

def create_file():
    file_path = filedialog.asksaveasfilename(defaultextension=".txt", filetypes=[("Text Files", "*.txt")])

    if file_path:
        with open(file_path, "w") as file:
            numbers = [random.randint(1, 100) for _ in range(10)]
            for num in numbers:
                file.write(str(num) + "\n")

        label_file.config(text=f"Файл создан и сохранён: {file_path}")
    else:
        label_file.config(text="Ошибка: файл не был выбран для сохранения.")

def read_file_and_calculate():
    file_path = filedialog.askopenfilename(filetypes=[("Text Files", "*.txt")])

    if file_path:
        try:
            with open(file_path, "r") as file:
                numbers = [int(line.strip()) for line in file]

                if numbers:
                    avg = sum(numbers) / len(numbers)
                else:
                    avg = 0

                label_file.config(text=f"Содержимое файла:\n{numbers}")
                label_avg.config(text=f"Среднее значение: {avg:.2f}")
        except Exception as e:
            label_file.config(text=f"Ошибка при чтении файла: {e}")
    else:
        label_file.config(text="Ошибка: файл не был выбран для чтения.")

root = tk.Tk()
root.title("Работа с файлами")
root.geometry("400x300")
root.configure(bg='lightgrey')

font_style = ('Arial', 12)

create_file_btn = tk.Button(root, text="Создать файл с числами", command=create_file, bg='purple', fg='white', font=font_style)
create_file_btn.pack(pady=10)

read_file_btn = tk.Button(root, text="Прочитать файл и вычислить среднее", command=read_file_and_calculate, bg='turquoise', fg='white', font=font_style)
read_file_btn.pack(pady=10)

label_file = tk.Label(root, text="", bg='lightgrey', font=font_style)
label_file.pack(pady=10)

label_avg = tk.Label(root, text="", bg='lightgrey', font=font_style)
label_avg.pack(pady=10)

root.mainloop()
