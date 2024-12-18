# Лабораторная работа 5
##  Задание 1

1) В директории .git/hooks/ создаю новый файл pre-commit и начинаю его редактирование

```
#!/bin/bash

# Устанавливаем права на исполнение
chmod +x "$0"

# Проверка, что есть хотя бы один .txt файл в staging area
txt_files=$(git diff --cached --name-only --diff-filter=ACM | grep '\.txt$')
if [ -z "$txt_files" ]; then
  echo "No .txt files found in the commit. Continuing..."
  exit 0 #Выход с кодом 0, т.к. ошибка отсутствия файлов не критична.
fi

# Проверка каждого .txt файла на наличие не-пробельных символов
for file in $txt_files; do
  if ! grep -q '[^[:space:]]' "$file"; then
    echo "Error: File '$file' is empty or contains only whitespace. Commit aborted." >&2
    exit 1
  fi
done

echo "All .txt files are valid. Commit proceeding..."
exit 0
```

2) Создаем пустые текстовые файлы:
 ![изображение](https://github.com/user-attachments/assets/79e7cf0a-02cf-42e3-9da0-10abcc85c10d)

3) очищаю staging area, чтобы Git не выдавал ошибку старых файлов перед коммитом новых и добавляю "правильный" файл:
![изображение](https://github.com/user-attachments/assets/ab06e77b-163c-4250-85be-65965ebb65d1)

4) Все супер

## Задание 2 

1. проверяю, что Git Flow установлен на локальной машине:

![image](https://github.com/user-attachments/assets/88d44fc0-7193-43e0-b750-2e5502deae6a)


2. В корне репозитория выполняю инициализацию Git Flow.

![image](https://github.com/user-attachments/assets/1cd28ffd-ed15-456b-a3a1-c443f87288d1)


3. Создаю ветку для новой функциональности, допустим она называется "task-management":

![image](https://github.com/user-attachments/assets/1c8ffb37-b297-4ec0-8075-11169ce57b20)


4. Вношу изменения в код для добавления функционала управления задачами:

![image](https://github.com/user-attachments/assets/0f8c7d46-99b8-4ec7-932d-5e77856c4930)

```bash
def create_task(title, description):
    # Логика создания задачи
    print(f"Создана новая задача: {title}")
```

Выполняю коммит изменения по мере разработки:

![image](https://github.com/user-attachments/assets/d7195bf0-6258-452e-9cc9-e1f321170afa)

5. После завершения разработки функции завершаю фичу и объединяю ее с основной веткой:

![image](https://github.com/user-attachments/assets/36d1b813-7192-4604-b3d2-27f2d5ea9c6d)

Git Flow автоматически переключится на ветку develop и выполнит слияние. Если есть конфликты, их нужно разрешить.

6. Начинаю создание релиза:

![image](https://github.com/user-attachments/assets/d4cabf4a-40cc-4a2c-ab1c-a8e7e3f128cb)

7. Вношу изменения, связанные с релизом (обновляю версию в файле version.txt):

![image](https://github.com/user-attachments/assets/83abe05b-53dd-44f5-8e65-a04d64eb1cb5)

8. Завершаю релиз и объединяю его с ветками "develop" и "main":

![image](https://github.com/user-attachments/assets/f43a0ce2-dabe-42a0-b4f7-d24933a3523a)

9. Если в процессе использования выявлена критическая ошибка, создам hotfix (у нас конечно же ошибки никакой не возникнет, но hotfix все равно создаем):

![image](https://github.com/user-attachments/assets/25ab9a86-e853-4d3d-99a5-15674920ce9f)

10. Вношу изменения для исправления ошибки и коммичу:

![image](https://github.com/user-attachments/assets/1bf7550d-40d4-479c-879c-a55cfaea5fa3)

11. Завершаю hotfix и объединяю его с ветками "develop" и "main":

![image](https://github.com/user-attachments/assets/6288f32e-d154-4ec3-9c2b-aade198a17b7)

12. Завершение работы и отправка изменений на удаленный репозиторий. Отправляю изменения на удаленный репозиторий:

```bash
git push origin develop
git push origin main

```















    
     
    
