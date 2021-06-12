# Шумилишский ИУ8-22 Лабораторная 11

## Tutorial

```sh
$ cd ~
$ mkdir install
$ mkdir tmp
$ export HOME_PREFIX=`pwd`/install
$ echo $HOME_PREFIX
$ export USERNAME=`whoami`
```

```sh
$ cd tmp
```

Скачиваем библиотеку libevent, для работы с Libevent API  
Распаковываем архив  
Переходим в директорию с библиотекой  
Указываем директорию, в которую будет производится установка  
Устанавливаем

```sh
$ wget https://github.com/libevent/libevent/releases/download/release-2.1.8-stable/libevent-2.1.8-stable.tar.gz
$ tar -xvzf libevent-2.1.8-stable.tar.gz
$ cd libevent-2.1.8-stable
$ ./configure --prefix=${HOME_PREFIX}
$ make && make install
$ cd ..
```

То же самое, только с ncurses

```sh
$ wget http://invisible-island.net/datafiles/release/ncurses.tar.gz
$ tar -xvzf ncurses.tar.gz
$ cd ncurses-5.9
$ ./configure --prefix=${HOME_PREFIX}
$ make && make install
$ cd ..
```

То же самое, только с tmux

```sh
$ wget https://github.com/tmux/tmux/releases/download/2.5/tmux-2.5.tar.gz
$ tar -xvzf tmux-2.5.tar.gz
$ cd tmux-2.5
$ ./configure --prefix=${HOME_PREFIX} CFLAGS="-I${HOME_PREFIX}/include -I${HOME_PREFIX}/include/ncurses" LDFLAGS="-L${HOME_PREFIX}/lib"
$ make && make install
$ cd ..
```

Скачиваем ngrok  
Устанавливаем unzip  
Распаковываем архив  
Перемещаем директорию с ngrok в bin

```sh
$ wget https://bin.equinox.io/c/4VmDzA7iaHb/ngrok-stable-linux-amd64.zip
$ unizp ngrok-stable-linux-amd64.zip
$ mv ngrok ${HOME_PREFIX}/bin
```

Устанавливаем LD_LIBRARY_PATH   
Задаем окружения  
Запускаем tmux

```sh
$ export LD_LIBRARY_PATH=${HOME_PREFIX}/lib
$ export PATH="${HOME_PREFIX}/bin:${PATH}"
$ tmux
```

Удаляем tmp и install

```sh
$ cd ~
$ rm -rf tmp install
```

Альтернативный способ установки tmux и ngrok

```sh
$ brew install tmux ngrok # or use linuxbrew 🎉
```

Создаем новую сессию

```sh
$ tmux new -s session_with_group
```

Поднимаем вм, из прошлой лабы  
Регаемся на сайте Указываем токен в качестве аутентификационного токена   
Указываем порт, чтобы получить доступ по SSH

```sh
# Alisa:
$ open https://ngrok.com/signup
$ export NGROK_TOKEN=<токен>
$ ngrok authtoken ${NGROK_TOKEN}
$ ngrok tcp 22
<порт_ngrok_сервера>
```

Работаем в виртуальной машине   
Подключемся к созданной групповой сессии  
Вертикальное разделение консольного окна

```sh
# Bob:
$ ssh ${USERNAME}@0.tcp.ngrok.io -p<порт_ngrok_сервера>
<пароль_от_учетной_записи>
$ tmux a -t session_with_group
$ <C-B>"
```
