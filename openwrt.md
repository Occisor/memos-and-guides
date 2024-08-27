Установка OpenWRT x86
!(preview)!
https://downloads.openwrt.org/releases/23.05.4/targets/x86/64/
generic-ext4-combined.img.gz

1. Создать виртуальный диск через диспетчер дисков, размером 512 Mb VHD
2. Выполнить команду GET-CimInstance -query "SELECT * from Win32_DiskDrive" она выведет список дисков, найти свой созданный. Например: \\.\PhysicalDrive4
3. Закрыть WSL: wsl --shutdown
4. Примонтировать диск к wsl (только под Администратором): wsl --mount \\.\PhysicalDrive4
5. Зайти в wsl напрямую с любого установленного дистрибутива
6. Определяем диск, например с помощью команды: lsblk -o vendor,model,name,mountpoint,fstype,size,fsuse%,state,label,uuid,pttype
или sudo fdisk -l
7. Копироуем образ OpenWRT на виртуальный диск: sudo dd if=openwrt-23.05.4-x86-64-generic-ext4-combined.img bs=1M of=/dev/sdc
заядя в папку с образом и подменим переменные названия образа и диска на свои
8. Закрываем WSL и гасим его полностью wsl --shutdown
9. В диспетчере дисков отсоединяем диск
10. Создаем виртуальную машину. Сетевой интерфейс желательно внешний. Заходим на него и правим сетевой интерфейс на нужный, днс сервер.
https://openwrt.org/docs/guide-user/advanced/expand_root
https://v2raya.org/en/
