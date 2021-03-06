---
layout: page
codeType: analysis
title: Скачивание и установка
menuitem: Скачивание и установка
ref: installation
lang: ru
permalink: /installation-ru/
category: help
priority: 1
---

Есть несколько способов установки Слимкоина. Слимкоин работает под Windows, Linux и Mac OS X.

## Скачивание

### Инсталлятор (Windows и Mac OS)

Вы можете скачать текущий релиз на [странице релизов](https://github.com/slimcoin-project/Slimcoin/releases).

Распакуйте файл и поместите содержимое в папку по своему выбору где вы можете запустить установку. Следуйте инструкциям в секции _Базовая установка_ ниже.

### Исходники (релизы)

Скачайте текущий релиз на [странице релизов](https://github.com/slimcoin-project/Slimcoin/releases).

Распакуйте исходный код в папку (назвав ее _Slimcoin_ для удобства), запустите терминал и _cd_ в нем.

#### Компиляция

Компиляция обычно представляет из себя довольно простой процесс если у вас установлены зависимости. Проверьте текущие зависимости в файле README. Также обратите внимание на необходимость установки пакета разработчика.

Для графического клиента, вбейте:

<div class="highlighter-rouge">
make
</div>

Если вы хотите скомпилировать только daemon: в подпапке _src_ находятся несколько makefiles под вашу систему (например _makefile.unix_). Выберете подходящий makefile и вбейте:

<div class="highlighter-rouge">
cd src make -f YOUR_MAKEFILE
</div>

После успешной компиляции исполняемый файл (_slimcoin-qt_) графического клиента будет доступен в основной папке, а daemon executable будет находиться в подпапке _src_. Вы можете переместить их куда захотите.

### Исходный код (git, экспериментальный)

Вам понадобится _git_ версия управляющей системы для этого метода работы.

Просто склонируйте Slimcoin репозиторий в любую папку:

<div class="highlighter-rouge">
git clone https://github.com/slimcoin-project/Slimcoin.git
</div>

Это создаст подпапку с названием _Slimcoin_. Переключитесь на нее:

<div class="highlighter-rouge">
cd Slimcoin
</div>

По умолчанию код будет в ветке _slimcoin_, которая является стабильной, но не новейшей. Если вы хотите самый новый код вы должны переключиться на ветку _master_ :

<div class="highlighter-rouge">
git checkout master
</div>

Затем скомпилируйте Слимкоин следуя указаниям выше.

## Базовая установка

Для базовой установки вы сначала должны узнать, что Слимкоин хранит все данные (блокчейн, кошелек, логи и файл конфигурации) в папке под названием **datadir**.

Дефолтное размещение:

*   **Windows:** `C:\Users\YOUR_USERNAME\Appdata\Roaming\Slimcoin` (Windows Vista/7 and later)
*   **Linux/Unix:** `/home/YOUR_USERNAME/.slimcoin` or simply `~/.slimcoin`
*   **Mac OS:** `~/Library/Application Support/Slimcoin/`

**Заметьте:** Для быстрого доступа datadir под Windows просто запустите _Run_ из меню Старт и вбейте следующее: `%APPDATA%/Slimcoin`

Рекомендуется создать в этой папке файл конфигурации **slimcoin.conf**. Вы можете задать в нем большую часть опций командной строки клиента Слимкоин Slimcoin client предложений (смотрите ниже). Просто создайте файл любым текстовым редактором.

Если вы хотите использовать программу daemon/CLI _slimcoind_, файл конфигурации **необходим** поскольку в нем будут заданы ваши логин и пароль. Создайте файл

<div class="highlighter-rouge">
rpcuser=USERNAME
rpcpassword=PASSWORD
</div>

Внесите следующую строку в него если вы хотите использовать его как daemon (запущенный в фоновом режиме) по умолчанию:

<div class="highlighter-rouge">
daemon=1
</div>

## Запуск Слимкоина

Итак, вы готовы запустить Слимкоин:

*   Для запуска графического клиента зайдите в папку, которую вы для него выбрали, дважды кликнув на исполняемый файл или запустите его командой **slimcoin-qt** в терминале.
*   Для daemon, вбейте **slimcoind**.

Вы можете найти опции командной строки вбив **slimcoind –help** или **slimcoin-qt –help**. Они по большей части совпадают с опциями, которые предлагает Биткоин. Референсы находятся тут: [Руководство по опциям командной строки Биткона](https://en.bitcoin.it/wiki/Running_Bitcoin). Заметьте, что не все команды Биткоина доступны для Слимкоина, но доступные будут работать так, как вы от них ожидаете.
