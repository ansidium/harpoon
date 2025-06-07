# Harpoon

Инструмент командной строки для OSINT и Threat Intel.

[![PyPI](https://img.shields.io/pypi/v/harpoon)](https://pypi.org/project/harpoon/) [![PyPI - Downloads](https://img.shields.io/pypi/dm/harpoon)](https://pypistats.org/packages/harpoon) [![PyPI - License](https://img.shields.io/pypi/l/harpoon)](LICENSE) [![GitHub issues](https://img.shields.io/github/issues/te-k/harpoon)](https://github.com/Te-k/harpoon/issues)

<img src="logo.png" width="100" height="100">

# Установка

## Требования

Перед установкой Harpoon необходимо установить зависимости [lxml](https://lxml.de/installation.html). На Debian/Ubuntu выполните: `sudo apt-get install libxml2-dev libxslt-dev python3-dev`. На Fedora: `sudo dnf install sqlite-devel automake bzip2 bzip2-devel bzip2-lib cython g++ gcc gcc-c++ kernel-devel libffi-devel libxlt libxml2 libxml2-devel libxslt libxslt-devel make openssl openssl-devel python3-dev python3-devel python3-lxml python-dev python-devel sqlite-devel`.

Также потребуется [geoipupdate](https://github.com/maxmind/geoipupdate), корректно настроенный для использования геолокации (убедитесь, что установлены базы `GeoLite2-Country GeoLite2-City GeoLite2-ASN`).

## Установка Harpoon

Установить пакет можно с [PyPI](https://pypi.org/project/harpoon/) командой `pip install harpoon`.

Если способ выше не сработал, соберите инструмент из исходников:

```
git clone https://github.com/Te-k/harpoon.git
cd harpoon
pip3 install .
```

Для дополнительного функционала можно установить [harpoontools](https://github.com/Te-k/harpoontools).

## Конфигурация

Запустите `harpoon config` и укажите необходимые API‑ключи. Затем выполните `harpoon update` для загрузки нужных файлов. Проверить активированные плагины можно командой `harpoon config -c`.

Подробнее см. в [wiki](https://github.com/Te-k/harpoon/wiki).

## Обновление Harpoon

Если Harpoon был установлен из [PyPI](https://pypi.org/project/harpoon/), обновите его командой `pip install -U harpoon`.

При установке из репозитория выполните:
```
git pull origin master
pip install .
```

# Использование

После настройки доступны следующие плагины (команда `harpoon`):

```
    asn                 Сбор информации об ASN
    binaryedge          Запрос к BinaryEdge API
    cache               Получение кешированной версии веб-страницы из разных источников
    censys              Запрос к базе Censys (https://censys.io/)
    certspotter         Получение сертификатов с https://sslmate.com/certspotter
    circl               Запрос к базе пассивного DNS CIRCL
    config              Настройка Harpoon
    crtsh               Поиск в https://crt.sh/ (Certificate Transparency)
    cybercure           Поиск в базе cybercure.ai
    dns                 Информация о DNS домена или IP
    dnsdb               Запросы к Farsight DNSDB
    email               Информация об электронной почте
    fullcontact         Запрос к Full Contact API (https://www.fullcontact.com/)
    github              Получение данных из GitHub API
    greynoise           Запрос к GreyNoise API (выберите Community или Enterprise через параметр api_type)
    hashlookup          Запрос к базе CIRCL Hash Lookup
    help                Справка по командам Harpoon
    hibp                Запрос к сервису Have I Been Pwned (https://haveibeenpwned.com/)
    hunter              Запрос к API hunter.io
    hybrid              Запрос к платформе Hybrid Analysis
    intel               Сбор информации о домене
    ip                  Сбор информации об IP-адресе
    ipinfo              Запрос к ipinfo.io
    ip2locationio       Запрос к IP2Location.io
    koodous             Запрос к Koodous API
    malshare            Запрос к базе MalShare
    misp                Получение данных из MISP через API
    numverify           Информация о телефонных номерах через NumVerify
    opencage            Обратное и прямое геокодирование через OpenCage
    otx                 Запрос к AlienVault OTX
    permacc             Запрос к Perma.cc
    pgp                 Поиск на PGP-ключевых серверах
    pt                  Запрос к Passive Total
    pulsedive           Запрос к PulseDive API
    quad9               Проверка домена в Quad9
    robtex              Поиск в Robtex API (https://www.robtex.com/api/)
    safebrowsing        Проверка домена через Google Safe Browsing
    save                Сохранение веб-страницы в кеш
    securitytrails      Запрос к SecurityTrails
    shodan              Запрос к Shodan API
    spyonweb            Поиск в SpyOnWeb через API
    subdomains          Поиск поддоменов домена
    telegram            Получение данных из Telegram API
    threatcrowd         Запрос к ThreatCrowd API
    threatgrid          Запрос к Threat Grid API
    threatminer         Запрос к базе ThreatMiner https://www.threatminer.org/
    tor                 Проверка IP в списке Tor exit-нод
    totalhash           Запрос к Total Hash API
    twitter             Запрос к Twitter API
    umbrella            Проверка домена в рейтинге Umbrella Top 1 Million
    update              Обновление данных Harpoon
    urlhaus             Запрос к urlhaus.abuse.ch
    urlscan             Поиск и отправка URL на urlscan.io
    vt                  Запрос к VirusTotal API
    xforce              Запрос к IBM Xforce Exchange API
    zetalytics          Поиск в базе Zetalytics
```

Получить справку по команде можно через `harpoon help COMMAND`.

## Ключи доступа

Список ссылок для получения API-ключей:
* [AlienVault OTX](https://otx.alienvault.com/)
* [BinaryEdge](https://www.binaryedge.io/)
* [Censys](https://censys.io/register)
* [CertSpotter](https://sslmate.com/certspotter/pricing) — оплата нужна для поиска по истёкшим сертификатам (чаще достаточно crtsh или censys). Для актуальных сертификатов аккаунт не обязателен.
* [CIRCL Passive DNS](https://www.circl.lu/services/passive-dns/)
* [Farsight Dnsdb](https://www.farsightsecurity.com/dnsdb-community-edition/)
* [FullContact](https://dashboard.fullcontact.com/register)
* [GreyNoise](https://viz.greynoise.io/account) — поддерживаются Community и Enterprise API. Параметр api_type задаёт тип API. В обоих случаях нужен ключ.
* [Have I Been Pwned](https://haveibeenpwned.com/)
* [Hunter](https://hunter.io/users/sign_up)
* [Hybrid Analysis](https://www.hybrid-analysis.com/apikeys/info)
* [IBM Xforce Exchange](https://exchange.xforce.ibmcloud.com/settings/api)
* [ipinfo.io](https://ipinfo.io/)
* [IP2Location.io](https://www.ip2location.io/)
* [Koodous](https://koodous.com/)
* [MalShare](https://malshare.com/register.php)
* [NumVerify](https://numverify.com/)
* [OpenCage](https://opencagedata.com/)
* [PassiveTotal](https://community.riskiq.com/registration)
* [Permacc](https://perma.cc/)
* [PulseDive](https://pulsedive.com/)
* [Security Trails](https://securitytrails.com/)
* [Shodan](https://account.shodan.io/register)
* [SpyOnWeb](https://api.spyonweb.com/)
* Telegram: [создание приложения](https://core.telegram.org/api/obtaining_api_id)
* [Total Hash](https://totalhash.cymru.com/contact-us/)
* [Twitter](https://developer.twitter.com/en/docs/ads/general/guides/getting-started)
* [UrlHaus](https://urlhaus.abuse.ch/api/#account)
* [UrlScan](https://urlscan.io/)
* VirusTotal: создайте учётную запись и получите ключ в [настройках](https://www.virustotal.com/#/settings/apikey)
* [Zetalytics](https://zetalytics.com/)

## Вклад

Благодарности всем, кто помогает улучшать Harpoon: [@jakubd](https://github.com/jakubd) [@marrouchi](https://github.com/marrouchi) [@grispan56](https://github.com/grispan56) [@christalib](https://github.com/christalib)

Логотип создан [@euphoricfall](https://twitter.com/euphoricfall) и командой [PulseDive](https://pulsedive.com/).

## Лицензия

Код распространяется по лицензии [GPLv3](LICENSE).
