# git-commands
git commands memo


### Настройка имени пользователя и адреса электронной почты.
```
git config --global user.name "Name"
git config --global user.email email@example.com
```

### Создание нового ключа SSH
```
ssh-keygen -t ed25519 -C "your_email@example.com"
```
Добавить ключ в гит через форму https://github.com/settings/keys


### Получить изменения с репозитория на локальный хост
Выполнять из локальнйо папки репозитория
```
git pull
```

### Отправить изменения с хоста в репозиторий
Выполнять из локальной папки репозиотрия
```
git add -A
git status
git commit -m "Commit text"
git push
```
1. `git add -A`: добавляет все измененные, удаленные и новые файлы в индекс Git.
2. `git status`: показывает список всех измененных файлов, которые готовы к коммиту.
3. `git commit -m "Commit text"`: коммитит изменения с сообщением, которое содержит краткое описание изменений.
4. `git push`: отправляет коммиты в удаленный репозиторий Git.

### .gitignore
https://www.freecodecamp.org/news/gitignore-file-how-to-ignore-files-and-folders-in-git/
