# Linux/WSL memos

### How can you get systemd on your machine?

To get started, you will need to do these two things: – Ensure you are running the right version of WSL: Version 0.67.6 and above – Set the systemd flag set in your WSL distro settings
### Ensuring you are on the right WSL version

This change is only available in the Microsoft Store version of WSL version 0.67.6 and higher. You can check your version number by running `wsl --version`. If that command fails then you are running the in-Windows version of WSL and need to upgrade to the Store version.

This version of WSL is now available in the Microsoft Store to users on Windows Insiders build for initial testing, and then after a few weeks we will make it available to all users to ensure quality. You can run `wsl --update` to check for any WSL updates.

If you are not on Windows Insiders and want to use it immediately, you can download the latest release from the WSL release page.

### Set the systemd flag set in your WSL distro settings

You will need to edit the `wsl.conf` file to ensure systemd starts up on boot.

Add these lines to the `/etc/wsl.conf` (note you will need to run your editor with sudo privileges, e.g: sudo nano `/etc/wsl.conf`):

```
[boot]
systemd=true
```

And close out of the nano editor using `CTRL+O` to save and `CTRL+X` to exit.

### Final steps

With the above steps done, close your WSL distro Windows and `run wsl.exe --shutdown` from PowerShell to restart your WSL instances. Upon launch you should have systemd running. You can check this with the command `systemctl list-unit-files --type=service` which should show your services’ status.

---
# Отключение snapd в образе Ubuntu
Для использования дефолтной версии это действие не обязательно. Но если захотите поиграться с графикой (поддержка была в Window 11 и недавно появилась в Windows 10), то придеться удалять, чтоб сохранить психику.
Проверям, что пакеты snap не установлены.
```
sudo snap list
```
В выводе должно быть пусто.
Удаляем snapd.
```
sudo apt autoremove --purge snapd
```
Очищаем кэш.
```
sudo rm -rf /var/cache/snapd/
rm -rf ~/snap
```
---
# Автозавершение команд по TAB в Debian
В Debian WSL из коробки не активировано автозавершение команд по нажатию TAB. Для активации нужно выполнить следующее.
Необходимо установить пакет `bash-completion`:
```
sudo apt install bash-completion
```
---
# Изменение прав доступа
| Mode | Name | Описание |
| :------------: | :------------: | :------------: |
| r | read | чтение файла или содержимого каталога |
| w | write | запись в файл или в каталог |
| x | execute | выполнение файла или чтение содержимого каталога |
| X | special execute | выполнение, если файл является каталогом или уже имеет право на выполнение для какого-нибудь пользователя |
| s | setuid/gid | установленные атрибуты SUID или SGID позволяют запускать файл на выполнение с правами владельца файла или группы соответственно |
| t | sticky | устанавливая t-бит на каталог, мы меняем это правило таким образом, что удалить файл может только владелец этого файла |

| двоичная | восьмеричная | символьная | права на файл | права на каталог |
| :------------: | :------------: | :------------: | :------------: | :------------: |
| 000 | 0 | -\-\- | нет | нет |
| 001 | 1 | -\-x | выполнение | чтение свойств файлов |
| 010 | 2 | -w- | запись | нет |
| 011 | 3 | -wx | запись и выполнение | всё, кроме получения имени файлов |
| 100 | 4 | r-\- | чтение | чтение имён файлов |
| 101 | 5 | r-x | чтение и выполнение | доступ на чтение файлов/их свойств |
| 110 | 6 | rw- | чтение и запись | чтение имён файлов |
| 111 | 7 | rwx | все права | все права |

| Reference | Class | Описание |
| :------------: | :------------: | :------------: |
| u | user | Владелец файла |
| g | group | Пользователи, входящие в группу владельца файла |
| o | others | Остальные пользователи |
| a | all | Все пользователи (или ugo) |

Примеры.  
Изменить владельца и группу для папки или файла:  
```
chown john:users /var/www/html
```
Рекурсивно изменить владельца на текущего пользователя:  
```
chown -R $(whoami): /var/www/html
```
Установить права «rwxr-xr-x» (755) для файла:
```
chmod u=rwx,g=rx,o=rx filename
```
Рекурсивно изменить права доступа для папки:  
```
chmod -R 755 /var/www/html
```
Изменить права доступа только на файлах в папке (рукурсивно за счет `find`):  
```
find /var/www/html -type f -exec chmod 644 {} \;
```
Изменить права доступа только на папках в папке (рукурсивно за счет `find`):  
```
find /var/www/html -type d -exec chmod 755 {} \;
```
Изменить часть прав. Владельцу добавится rwx:
```
chmod u+rwx filename
```
Изменить часть прав. У группы удалится x:
```
chmod g-x filename

```

---
# `venv` в Python
Как использовать `venv` в Python — способ создавать изолированные виртуальные окружения.

### 1. Создание виртуального окружения

```bash
# Python 3 (рекомендуется)
python -m venv myenv

# Или явно python3, если у вас несколько версий
python3 -m venv myenv

# Популярные названия папки:
myenv        ← чаще всего
venv         ← очень популярно
.env         ← тоже встречается
env
```

После выполнения появится папка `myenv` со своей копией Python и pip.

### 2. Активация виртуального окружения

| ОС          | Команда для активации                          | Как деактивировать    |
|-------------|------------------------------------------------|-----------------------|
| Windows     | `myenv\Scripts\activate`                       | `deactivate`          |
|             | или в PowerShell: `myenv\Scripts\Activate.ps1` |                       |
| macOS/Linux | `source myenv/bin/activate`                    | `deactivate`          |
|             | или коротко: `. myenv/bin/activate`            |                       |
| Git Bash (Windows) | `source myenv/Scripts/activate`          | `deactivate`          |

После активации в терминале появится префикс:
```bash
(myenv) C:\your\project>
(myenv) user@macbook project %
```

### 3. Работа внутри venv

```bash
# Установка пакетов — они попадают только в это окружение
pip install requests django fastapi aiohttp

# Смотрим установленные пакеты
pip list
pip freeze

# Сохраняем зависимости в файл (очень важно!)
pip freeze > requirements.txt
```

### 4. Деактивация

Просто в любом месте:
```bash
deactivate
```
Префикс `(myenv)` исчезнет — вы снова в глобальном Python.

### 5. Полный пример реального проекта

```bash
# 1. Создаём проект
mkdir myproject
cd myproject

# 2. Создаём виртуальное окружение
python -m venv venv

# 3. Активируем
# Windows:
venv\Scripts\activate
# macOS/Linux:
source venv/bin/activate

# 4. Обновляем pip (всегда полезно)
pip install --upgrade pip

# 5. Устанавливаем нужные пакеты
pip install fastapi uvicorn python-dotenv

# 6. Сохраняем зависимости
pip freeze > requirements.txt

# 7. Добавляем в git (что нужно, а что нет)
```

### .gitignore — что НЕ коммитить

Создай файл `.gitignore` в корне проекта:
```
# Виртуальные окружения
venv/
env/
.env/
myenv/
ENV/

# Папки Python
__pycache__/
*.pyc
*.pyo
*.pyd
.Python
env.bak/
pip-delete-this-directory.txt

# IDE
.idea/
.vscode/
```

### 6. Как другие разработчики запустят твой проект

```bash
git clone https://github.com/tvoy/login/myproject.git
cd myproject

# Создадут своё окружение
python -m venv venv
source venv/bin/activate      # или venv\Scripts\activate на Windows

# Установят все зависимости одним махом
pip install -r requirements.txt

# Запустят проект
uvicorn main:app --reload
```

### Полезные трюки

```bash
# Создать и сразу активировать (macOS/Linux)
python -m venv venv && source venv/bin/activate

# Создать venv с доступом к глобальным пакетам (редко нужно)
python -m venv venv --system-site-packages

# Проверить, какой Python используется сейчас
which python      # Linux/macOS
where python      # Windows
python --version
```

Готово! Теперь ты используешь виртуальные окружения как профессионал.

Если часто работаешь с проектами — поставь себе привычку:
```bash
mkdir myproject && cd myproject && python -m venv venv && source venv/bin/activate && code .
```
— и ты всегда будешь в чистом, изолированном и воспроизводимом окружении.

---
