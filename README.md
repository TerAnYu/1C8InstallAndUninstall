﻿# Установка и удаление дистрибутивов 1С:Предприятия 8 на локальных компьютерах
Прочитать статью по работе со скриптом и обсудить на сущие вопросы можно по адресу http://infostart.ru/public/299829/

Описание Скрипта: Данный скрипт удаляет и устанавливает дистрибутивы 1С из сетевого каталога и пишет логи установки

Автор: Dim

Версия: 0.2

Входные параметры:

* dd &mdash; Distribution Directory &mdash; путь до каталога с дистрибутивами платформы 1С 8
* dl &mdash; Directory Logs &mdash; путь до каталога, в который будут записываться логи установки и удаления
* ip &mdash; Install Parameters &mdash; параметры инсталляции, согласно которым будет работать скрипт
  * "no" &mdash; не производить установку 
  * "last" &mdash; установить последнею найденную версию в каталоге с дистрибутивами 1С 8
  * "8.3.5.1111" &mdash; установить конкретный дистрибутив платформы
* dp &mdash; Delet Parameters &mdash; параметры удаления соответствии с которыми будет работать скрипт
  * "no" &mdash; не производить удаление 
  * "ael" - удалить все версии, кроме последней (All Except Last)
  * "8.3.5.1111" &mdash; удалить конкретный дистрибутив платформы
  * "all" &mdash; удалить все дистрибутивы 1С:Предприятие 8 найденные на локальном компьютере
  * "ndini" &mdash; игнорировать параметр dp если параметр ip не отработал как нужно (Not Delet If Not Install)
* iod &mdash; Installation Options Distribution &mdash; параметры задаваемые при установке самой платформы, выглядят как строка "DESIGNERALLCLIENTS=1 THINCLIENT=0 THINCLIENTFILE=0"
  * "DESIGNERALLCLIENTS" &mdash; основной клиент и конфигуратор
  * "THINCLIENT" &mdash; тонкий клиент для клиент-серверного варианта работы
  * "THINCLIENTFILE" &mdash; тонкий клиент с возможностью работы с файловыми информационными базами
		
Тонкости работы:

1. Если по какой либо причине скрипт не сможет записать логи в указанный каталог, то запись будет произведена в файл 1C8InstallAndUninstall.log в локальный каталог пользователя, примерный путь: c:\Users\Vasa\AppData\Local\
2. Параметр "last" у ключа -ip установит последнюю версию из найденных в каталоге дистрибутивов.
3. Параметр "ael", у ключа -dp, удалит только те установленные версии, которые будут в каталоге с дистрибутивами.
4. Параметр "all", у ключа -dp, подавляет все другие параметры и является приоритетным, более того, он удалит всё установленное, похоже на платформу 1С:Предвриятие, несмотря на то, что лежит в каталоге с дистрибутивами.
5. В каталоге с дистрибутивами рассматриваются только папки вида "Х.Х.Х.Х", соответствующие версиям платформ в них находящихся. Все остальные папки и файлы игнорируются.

Пример:

`powershell "\\Server\1CDistr\1C8InstallAndUninstall.ps1" -dd '\\Server\1CDistr' -dl '\\Server\1CLog' -dp 'ael' -ip 'last' -iod 'DESIGNERALLCLIENTS=1 THINCLIENT=1 THINCLIENTFILE=1'`