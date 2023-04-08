Домашняя работа № 25. LDAP

Установить FreeIPA;

Написать Ansible playbook для конфигурации клиента;

Firewall должен быть включен на сервере и на клиенте*

Ход работы.

Для установки необходимых пакетов на сервере и клиенте используем ansible

Поднимаем стенд:
```
vagrant up
```
После чего с помощью ansible завершаем настройку сервера и клиентов:
```
ansible-playbook -i hosts site.yaml
```
Проверяем на сервере работу ipa. Получаем билет для пользователя admin
```
[root@ipa ~]# kinit admin
Password for admin@OTUS.LAN:
[root@ipa ~]# klist
Ticket cache: KCM:0
Default principal: admin@OTUS.LAN

Valid starting     Expires            Service principal
04/08/23 09:31:47  04/09/23 09:31:38  krbtgt/OTUS.LAN@OTUS.LAN
```
Создаем нового пользователя на сервере IPA
```
[root@ipa ~]# ipa user-add otus-user --first=Otus --last=User --password
Password:
Введите Password ещё раз для проверки:
----------------------
Added user "otus-user"
----------------------
  User login: otus-user
  First name: Otus
  Last name: User
  Full name: Otus User
  Display name: Otus User
  Initials: OU
  Home directory: /home/otus-user
  GECOS: Otus User
  Login shell: /bin/sh
  Principal name: otus-user@OTUS.LAN
  Principal alias: otus-user@OTUS.LAN
  User password expiration: 20230408090442Z
  Email address: otus-user@otus.lan
  UID: 172000003
  GID: 172000003
  Password: True
  Member of groups: ipausers
  Kerberos keys available: True
```
На клиенте проверяем:
```
[root@client1 ~]# su - otus-user
Creating home directory for otus-user.
[otus-user@client1 ~]$ pwd
/home/otus-user

```
