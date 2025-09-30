
ОТОБРАЖЕНИЕ МЕНЮ ЗАГРУЗЧИКА.

для отображения меню загрузчика вносим изменения в файл /etc/default/grub. параметры:

#GRUB_TIMEOUT_STYLE=hidden
GRUB_TIMEOUT=20

по умолчанию GRUB_TIMEOUT_STYLE=hidden (скрыть показ меню) включен, а его таймаут GRUB_TIMEOUT равен 0.

sudo update-grub - для обновления конфигурации загрузчика после внесения изменений.

результат представлен в file_1.jpg.


ПОПАСТЬ В СИСТЕМУ БЕЗ ПАРОЛЯ.

1. через изменение параметров загрузки.

на экране выбора загрузчика нажать е. после этого отредактировать строку с параметрами загрузки ядра добавив в ее конец запись init=/bin/bash.


2. через recovery mode.

в меню загрузки выбрать Advanced options for Ubuntu --> длее recovery --> пункт root --> и ENTER.

это позволит попасть в консоль с правами root'a.

результат представлен в file_2.jpg.


ПЕРЕИМЕНОВАНИЕ VOLUME_GROUP:

переименовывать будем едиственную группу "ubuntu-vg" в "ubuntu-test".

konstantin@konstantin1:~$ sudo vgscan
  Found volume group "ubuntu-vg" using metadata type lvm2

konstantin@konstantin1:~$ sudo vgrename ubuntu-vg ubuntu-test
  Volume group "ubuntu-vg" successfully renamed to "ubuntu-test"

konstantin@konstantin1:~$ sudo vgscan
  Found volume group "ubuntu-test" using metadata type lvm2


далее для корректной загрузки правим /boot/grub/grub.cfg. поле menuentry и submenu.

linux   /vmlinuz-5.15.0-156-generic root=/dev/mapper/ubuntu--test-ubuntu--lv ro

результат представлен в file_3.jpg.

















