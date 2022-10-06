
    1 Установлен Oracle VirtualBox.
    
    sudo apt install virtualbox

    2 Установлен  Hashicorp Vagrant.
     sudo apt-get install vagrant

    3 Подготовлен терминал.
    
    4 Запущен Ubuntu 20.04 в VirtualBox посредством Vagrant     

    5 Ознакомьтесь с графическим интерфейсом VirtualBox, посмотрите как выглядит виртуальная машина, которую создал для вас 

Vagrant, какие аппаратные ресурсы ей выделены. Какие ресурсы выделены по-умолчанию?
    Решение:

    выполнено:
    RAM:2024mb
    CPU:2 cpu
    HDD:28gb
    video:8mb

   6 Ознакомьтесь с возможностями конфигурации VirtualBox через Vagrantfile: документация. Как добавить оперативной памяти или 

ресурсов процессора виртуальной машине?
    Решение:

    добавлением комманд в VagrantFile:
    короткие линки
      v.memory = 2024
      v.cpus = 2
    или командами ВМ
       config.vm.provider "virtualbox" do |vb|
         vb.memory = "2024"
         vb.cpu = "2"
       end
      

    7 Выполнил vagrant ssh, и  оказался внутри виртуальной машины. 
        

    8 Ознакомиться с разделами man bash, почитать о настройках самого bash:
    Решение: какой переменной можно задать длину журнала history, и на какой строчке manual это описывается?

    1. HISTFILESIZE - максимальное число строк в файле истории для сохранения,строка 1155
    2. HISTSIZE - число команд для сохранения,  строка 1178

    что делает директива ignoreboth в bash?

        ignoreboth это сокращение для 2х директив ignorespace and ignoredups, 
        ignorespace - не сохранять команды начинающиеся с пробела, 
        ignoredups - не сохранять команду, если такая уже имеется в истории

    9 В каких сценариях использования применимы скобки {} и на какой строчке man bash это описано?
    

    {} - зарезервированные слова, список, в т.ч. список команд команд в отличии от "(...)" исполнятся в текущем инстансе, 
    используется в различных условных циклах, условных операторах, или ограничивает тело функции, 
    В командах выполняет подстановку элементов из списка , если упрощенно то  цикличное выполнение команд с подстановкой 
    например mkdir ./DIR_{A..Z} - создаст каталоги сименами DIR_A, DIR_B и т.д. до DIR_Z
    

    10 Основываясь на предыдущем вопросе, как создать однократным вызовом touch 100000 файлов? А получилось ли создать 300000?
    
    touch {000001..100000}.txt - создаст в текущей директории соответсвющее число фалов

    300000 - создать не удасться, это слишком дилинный список аргументов, максимальное число получил экспериментально - 110188

    11 В man bash поищите по /\[\[. Что делает конструкция [[ -d /tmp ]]
    

    проверяет условие у -d /tmp и возвращает ее статус (0 или 1), наличие катаолга /tmp

    
   12 Основываясь на знаниях о просмотре текущих (например, PATH) и установке новых переменных; командах, которые мы 

рассматривали, добейтесь в выводе type -a bash в виртуальной машине наличия первым пунктом в списке:
    

    vagrant@vagrant:~$ mkdir /tmp/new_path_dir/
    vagrant@vagrant:~$ cp /bin/bash /tmp/new_path_dir/
    vagrant@vagrant:~$ type -a bash
    bash is /usr/bin/bash
    bash is /bin/bash
    vagrant@vagrant:~$ PATH=/tmp/new_path_dir/:$PATH
    vagrant@vagrant:~$ type -a bash
    bash is /tmp/new_path_dir/bash
    bash is /usr/bin/bash
    bash is /bin/bash
      
        

   13 Чем отличается планирование команд с помощью batch и at?
    

    at - команда запускается в указанное время (в параметре)
    batch - запускается когда уровень загрузки системы снизится ниже 1.5.
    

   14 Pавершите работу виртуальной машины чтобы не расходовать ресурсы компьютера и/или батарею ноутбука.
    
     vagrant suspend

