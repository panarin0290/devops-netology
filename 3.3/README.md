# ДЗ 3.3

## 1.

chdir()

- Команда:

```
diff <(strace /bin/bash -c 'cd /tmp' 2>&1 | cut -d'(' -f 1 | sort | uniq) <(strace /bin/bash -c 'alias' 2>&1 | cut -d'(' -f 1 | sort | uniq)
```

- Вывод:

```
 4d3
< chdir
```
## 2.
```file``` ищет файлы ```magic.mgc``` и ```magic```:
- В /etc
- В домашней директории, скрыты

## 3.
- По pid процесса можно посмотреть его дескрипторы.
- В дескриптор направить пустую строку: ```echo '' > sudo /proc/13300/fd/3```

## 4.
Нет. Когда процесс завершается через exit, вся память и связанные с ним ресурсы освобождаются, чтобы их могли использовать другие процессы.

## 5.
- Команда:

```
(timeout -k 1 -s 9 1 strace opensnoop-bpfcc 2>&1 | grep -E '^open|Killed' | sed 's|openat.*, "||g; s|", .*||g' ) | sort | uniq -c | sort -h | wc -l
```

- Вывод:

```
304
```

304 различных путей — попытка найти файл в различных директориях

## 6.

 системный вызов uname()

- Цитата:

```
Part of the utsname information is also accessible  via  /proc/sys/kernel/{ostype, hostname, osrelease, version, domainname}
```
## 7.
- ```&&``` - условный оператор
- ```;``` - разделитель последовательных команд

- ```test -d /tmp/some_dir && echo Hi``` - в данном случае ```echo``` отработает только при успешном завершении команды ```test```
- ```&&``` вместе с ```set -e``` - не имеет смысла, так как при ошибке, выполнение команд прекратиться
## 8.
- ```-e``` - прерывает выполнение исполнения при ошибке любой команды кроме последней в последовательности 
- ```-u``` - незаданные/неустановленные параметры и переменные считаются как ошибки, с выводом в stderr текста ошибки и выполнит завершение не интерактивного вызова
- ```-x``` - вывод трейса простых команд 
- ```-o``` - ```pipefail``` возвращает код возврата последовательности команд, ненулевой при последней команды или 0 для успешного выполнения команд.

Для сценария, повышает детализацию вывода ошибок(логирования), и завершит сценарий при наличии ошибок, на любом этапе выполнения сценария, кроме последней завершающей команды
## 9.
- ```S*(S,S+,Ss,Ssl,Ss+)``` - Процессы ожидающие завершения (спящие с прерыванием "сна")
- ```I*(I,I<)``` - Бездействующие процессы ядра
