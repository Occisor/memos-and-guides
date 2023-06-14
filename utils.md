# Utils settings
Настройка утилит/приложений.
### Mcabber installation and use  
Полезные ссылки (отредактировать позже):  
https://mcabber.com/files/mcabber.1.html  
http://old.open-suse.ru/modules/smartsection/item.php?itemid=87  
https://wiki.mcabber.com/ru.html

---
### Pass installation and use
Установка:
```
apt install pass
```
Для дальнейшего использования `pass`, у вас должен быть GPG ключ, если у вас его нет, то необходимо [его создать](https://github.com/Occisor/memos-and-guides/blob/main/utils.md#gpg-key-installation-and-use "GPG-key установка"). Выберите вариант 1 (RSA и RSA) для типа ключа.  
Инициализируем шифрование по идентификатору ключа.
```
pass init 'идентификатор ключа'
```
В качестве идентификатора можно использовать, например D95BF1929075632D832183036AA43518EEB00A4A или example, из вывода `gpg --list-keys` ниже:
```
pub   rsa4096 2023-06-14 [SC]
      D95BF1929075632D832183036AA43518EEB00A4A
uid           [ultimate] example
sub   rsa4096 2023-06-14 [E]
```
Вносим новый пароль:
```
pass insert resource/name
```
Этой командой создадим пароль в ветке:
```
Password Store
└── resource
    └── name
```
Генерируем пароль:
```
pass generate resource/name
```
Выводим/отображаем пароль:
```
pass resource/name
```
Список имен сохраненных паролей:
```
pass
```
Удаляем пароль:
```
pass rm resource/name
```
---
### GPG-key installation and use
Сгенерируйте пару ключей, набрав в терминале:
```
gpg --full-gen-key
```
Выбираем тип ключа.
```
Please select what kind of key you want:
   (1) RSA and RSA (default)
   (2) DSA and Elgamal
   (3) DSA (sign only)
   (4) RSA (sign only)
  (14) Existing key from card
Your selection?
```
Выбираем длину ключа. Рекомендуется 4096.
```
RSA keys may be between 1024 and 4096 bits long.
What keysize do you want? (3072)
```
Определяем срок эксплуатации ключа.
```
Please specify how long the key should be valid.
         0 = key does not expire
      <n>  = key expires in n days
      <n>w = key expires in n weeks
      <n>m = key expires in n months
      <n>y = key expires in n years
Key is valid for? (0)
````
Вводим данные ключа. Достаточно указать `Real name:`
```
GnuPG needs to construct a user ID to identify your key.

Real name: example
Email address:
Comment:
```
Наличие пароля. Если дальнейшее применение ключа требует прозрачное использование, то оставляем пустым.
```
      ┌──────────────────────────────────────────────────────┐
      │ Please enter the passphrase to                       │
      │ protect your new key                                 │
      │                                                      │
      │ Passphrase: ________________________________________ │
      │                                                      │
      │       <OK>                              <Cancel>     │
      └──────────────────────────────────────────────────────┘
```
Завершаем установку. Созданные ключи хранятся в папке `.gnupg`, домашней дирректории.
Список установленных ключей:
```
gpg --list-keys
```
Удалить публичный и секретный ключи:
```
gpg --delete-secret-and-public-keys <идентификатор ключа>
```

---
### Tmux installation and use
Полезные ссылки (отредактировать позже):  
https://habr.com/ru/articles/327630/
