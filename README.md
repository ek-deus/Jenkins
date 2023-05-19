По требованиям к виртуалке: 2-4 гига оперативки, 1 проц, 2 ядра, диск вместе с системой на 100 гигов (thin). Если не хватит, добавить. Все зависит от задач. А еще можно почитать системные требования вот туть

Поехали.

Сначала ставим комплект Oracle JDK 11.
# проверим версию
java -version

# если у нас уже есть 11 версия, переходим к следующему шагу.
# если нет, апдейтим пакеты
sudo apt update

sudo apt install default-jre default-jdk
Дальше тут можно глянуть, как ставить Oracle JDK. Чуть позже добавлю сюда.

Ставим Jenkins.
# В уюунте обычно древняя версия. Ставим поновее.
# Добавим реп
wget -q -O - https://pkg.jenkins.io/debian-stable/jenkins.io.key | sudo apt-key add -
sudo sh -c 'echo deb http://pkg.jenkins.io/debian-stable binary/ \
> /etc/apt/sources.list.d/jenkins.list'

# Апдейтим
sudo apt update

# Ставим Jenkins
sudo apt install jenkins
# Запускаем
sudo systemctl start jenkins

# И проверяем, как стартовал
sudo systemctl status jenkins

# Все ок.
Включаем и даем доступ через Firewall.
sudo ufw allow 8080
sudo ufw allow OpenSSH
sudo ufw enable
sudo ufw status
Настраиваем через веб-морду.
Идем на http://your_server_ip_or_domain:8080

Теперь нам нужно достать пароль для входа в админку. Копируем выделенное красным 

sudo cat /var/lib/jenkins/secrets/initialAdminPassword
Скопируем 32-символьный пароль из командной строки и вставьте его в поле Administrator password, после чего нажмите Continue

На следующем экране отображаются рекомендуемые для установки плагины и предоставляется возможность выбора конкретных плагинов. Не паримся и выбираем Install suggested plugins (Установить рекомендованные плагины), после чего сразу же будет запущен процесс установки.

После завершения установки будет предложено настроить первого пользователя с правами администратора. Настраиваем по своему вкусу. и жмем далее.

Далее мы видим страницу Instance Configuration (Конфигурация экземпляра), где нужно будет подтвердить предпочитаемый URL для вашего экземпляра Jenkins. Подтвердите доменное имя вашего сервера или IP-адрес вашего сервера.

После подтверждения соответствующей информации нажмите Save and Finish (Сохранить и завершить). Вы увидите страницу с подтверждением «Jenkins is Ready!»

Тадаам... Все!

PS: Если что, то конфиг Jenkins лежит тут /etc/default/jenkins

Сылки по теме:

How To Configure Jenkins with SSL Using an Nginx Reverse Proxy on Ubuntu 20.04

How To Set Up Continuous Integration Pipelines in Jenkins on Ubuntu 16.04

CI / CD для jenkins + maven + gitlab + harbor + k8s

Groovy за 15 минут – краткий обзор

И вообще вот официальный ман по дженкинсу

И первый pipeline
