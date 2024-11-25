---
---

# X-Road

Что это? Зарубежная opensource EDI система. Изначально разрабатывалась в Эстонии 🇪🇪 и Финляндии 🇫🇮 для собственных нужд, далее выложили в opensource для развивающихся стран.

Репозиторий: https://github.com/nordic-institute/X-Road

Исходный код написан на языке [Java](https://ru.wikipedia.org/wiki/Java)

Используемые протоколы: [ACME](https://en.wikipedia.org/wiki/Automatic_Certificate_Management_Environment), [OCSP](https://ru.wikipedia.org/wiki/OCSP),[TSP](https://en.wikipedia.org/wiki/Time_stamp_protocol)

Аппаратные возможности: [HSM](https://en.wikipedia.org/wiki/Hardware_security_module), [SSCD](https://en.wikipedia.org/wiki/Secure_signature_creation_device)

Установка тестовой среды через LXD:

```shell
snap install lxd
lxd init
sudo apt install ansible
git clone https://github.com/nordic-institute/X-Road.git
cd X-Road/ansible
ansible-playbook -i hosts/lxd_hosts.txt xroad_init.yml
```

Установка тестовой среды через Docker:

```shell
git clone https://github.com/nordic-institute/X-Road.git
cd Docker/xrd-dev-stack
XROAD_HOME=/home/a/X-Road
./local-dev-run.sh --initialize
```
 
В самой минимальной конфигурации должны быть контейнеры (названия могут отличаться):

```
xroad-lxd-ca - Central Server, test CA with OCSP and TSA
xroad-lxd-cs - management Security Server
xroad-lxd-ss1 - Security Server
```

## Возможные проекты

Сделать вывод в xml у [pydifact](https://github.com/nerdocs/pydifact). Критерий приёмки - сравнить с выводом любой библиотеки на другом языке программирования (например, [php-edifact](https://github.com/php-edifact/edifact) или перловая [XML::Edifact](https://metacpan.org/pod/XML::Edifact)). Можно сделать отдельной задачей упаковку этих двух библиотек в docker, чтоб легче было тестировать в пайплайнах (ℹ️ Python,Linux)

[Собрать docker контейнер с сервисом X-Road-Metrics](https://github.com/nordic-institute/X-Road-Metrics/issues/126) (ℹ️ Python,Docker)

Добавить новые [тестовые данные в pydifact](https://github.com/nerdocs/pydifact/tree/master/tests/data), содержащие сообщения EDI-типов PRICAT, ORDRSP, DESADV, RECADV, RETANN (). Файлы поискать в интернете (ℹ️ Git,Python)

Купить VDS сервер, развернуть X-Road в облаке на Docker. Сделать сервер прерываемый, так чтобы он потреблял минимум ресурсов при простое (ℹ️ Linux)

[Добавить зарезервированные коды в XRoad](https://github.com/nordic-institute/X-Road/issues/1363) (ℹ️ Java)

Создать документацию для docker-образа [intecbf/edifact2xml] (ℹ️ Java+Spring)

*Под тегом ℹ️Linux понимается также Docker и Bash*
