
---

# Установка Semaphore с использованием Ansible и Postgres

## Описание

Этот Ansible-плейбук предназначен для автоматической установки и настройки [Semaphore](https://github.com/semaphoreui/semaphore) — веб-интерфейса для управления Ansible-скриптами. Semaphore будет работать в связке с базой данных PostgreSQL.

## Требования

Перед использованием плейбука убедитесь, что:

1. У вас установлен Ansible версии 2.16.3 или выше.
2. У вас есть доступ к серверам (или виртуальным машинам) с установленной операционной системой Ubuntu 20.04 (используемая ОС для проекта в репозитории)
3. На целевых серверах настроен доступ по SSH.
4. У вас есть права sudo на целевых серверах (или root-доступ).

## Подготовка

1. Склонируйте репозиторий с плейбуком:
  

```
   git clone 
   cd ansible_practice
```
   

2. Настройте файл hosts.ini, указав IP-адреса или доменные имена целевых серверов. Пример:
  

```
   [semaphore_server]
   192.168.1.10 ansible_user=your_user
```

3. Настройте переменные в vars/vars.yml:

- Данные для подключения к PostgreSQL:
```
     postgres_user: "semaphore"
     postgres_password: "password"
     db_name: "semaphore"
     postgres_server_ip: "127.0.0.1"
     postgres_port: 5432
```

- Параметры Semaphore:
```
     semaphore_version: "2.8.77"
     semaphore_user: "semaphore"
     semaphore_group: "semaphore"
     semaphore_dir: "/opt/semaphore"
     semaphore_bin: "/usr/local/bin/semaphore"
```

4. Проверьте настройки в ansible.cfg
```
     [defaults]
     inventory = ./hosts.ini
     private_key_file =  #путь до ssh ключа на локальной машине
     remote_user =  #пользователь, от имени которого будет установлено ssh соединение
     host_key_checking = False
```
     

## Установка

Запустите плейбук, используя следующую команду:

`ansible-playbook playbook.yml`


## Результат

После успешного выполнения плейбука:
1. Semaphore будет установлен и доступен по HTTP/HTTPS на указанном сервере.
2. PostgreSQL будет настроен для работы с Semaphore.
3. Учетные данные пользователя (определенные в переменных) будут созданы.

