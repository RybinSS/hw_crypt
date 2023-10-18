# hw_crypt
### Задание 1
Что нужно сделать:

1.  Установите eCryptfs.
  sudo apt install ecryptfs-utils  
3.  Добавьте пользователя cryptouser.
  sudo adduser --encrypt-home cryptouser  
5.  Зашифруйте домашний каталог пользователя с помощью eCryptfs.
  su cryptouser
  touch 123, 456
  exit
  sudo ls /home/cryptouser
  "Access-Your-Private-Data.desktop README.txt"

<img src = "img/cryptouser.png" width = 100%>  

### Задание 2

1. Установите поддержку LUKS.
   sudo apt-get install cryptsetup  
3. Создайте небольшой раздел, например, 100 Мб.
  "через gparted"
5. Зашифруйте созданный раздел с помощью LUKS.
  Подготовка раздела (luksFormat):  
    user@user:~$ sudo cryptsetup -y -v --type luks2 luksFormat /dev/sdb1  
  Монтирование раздела:  
    user@user:~$ sudo cryptsetup luksOpen /dev/sdb1 disk  
    user@user:~$ ls /dev/mapper/disk  
  Форматирование раздела:  
    user@user:~$ sudo dd if=/dev/zero of=/dev/mapper/disk   
    user@user:~$ sudo mkfs.ext4 /dev/mapper/disk  
   Монтирование «открытого» раздела:  
    user@user:~$ mkdir .secret  
    user@user:~$ sudo mount /dev/mapper/disk .secret/  
  Завершение работы:  
    user@user:~$ sudo umount .secret  
    user@user:~$ sudo cryptsetup luksClose disk  
   
<img src = "img/luks.png" width = 100%>  
<img src = "img/luks2.png" width = 100%>  
