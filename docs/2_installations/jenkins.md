# 🐳 Развертывание Jenkins через Docker Compose

## 1. 📁 Создание директории Jenkins

```bash
mkdir ~/jenkins && cd ~/jenkins # (1)
```

1. !!! annotation "Параметры команды"
    `mkdir ~/jenkins && cd ~/jenkins`: Создает директорию `jenkins` в домашней папке и сразу переходит в нее.

## 2. 🛠️ Создание файла `docker-compose.yml`

```bash
nano docker-compose.yml # (1)
```

1. !!! annotation "Параметры команды"
    `nano docker-compose.yml`: Открывает текстовый редактор `nano` для создания файла конфигурации.

Вставьте следующее содержимое:

```yaml
version: '3.8' 
services:
  jenkins:
    image: jenkins/jenkins:lts-jdk17  # (1)
    container_name: jenkins
    user: root  # (2)
    ports:
      - "8080:8080"  # (3)
      - "50000:50000"  # (4)
    volumes: # (5)
      - jenkins_data:/var/jenkins_home
      - /var/run/docker.sock:/var/run/docker.sock
    environment:
      - JAVA_OPTS=-Djenkins.install.runSetupWizard=false  # (6)
    restart: unless-stopped  # (7)
volumes:
  jenkins_data:  # (8)
```

1. !!! annotation "Параметры команды"
    `image: jenkins/jenkins:lts-jdk17`: Указывает образ Docker, который будет использован для запуска контейнера. `jenkins jenkins:lts-jdk17` — это официальный образ Jenkins с долгосрочной поддержкой (LTS) и предустановленной Java 17.

2. !!! annotation "Параметры команды"
    `user: root`: Указывает, что контейнер будет запускаться от имени пользователя `root`. Это помогает избежать проблем с правами доступа, особенно при работе с хостовым Docker или файлами.

3. !!! annotation "Параметры команды"
    `8080:8080`: Перенаправляет порт 8080 хоста на порт 8080 контейнера, где работает веб-интерфейс Jenkins.

4. !!! annotation "Параметры команды"
    `50000:50000`: Открывает порт 50000 для подключения агентов Jenkins.

5. !!! annotation "Параметры команды"
    `volumes`: Определяет тома для хранения данных и доступа к хосту.

    `jenkins_data:/var/jenkins_home`: Создает именованный том `jenkins_data` для сохранения данных Jenkins (настройки, задания) в `/var/jenkins_home` внутри контейнера.
    `/var/run/docker.sock:/var/run/docker.sock`: Монтирует сокет Docker хоста, позволяя контейнеру взаимодействовать с Docker на хост-системе (например, для создания контейнеров внутри Jenkins).

6. !!! annotation "Параметры команды"
    `environment`: Устанавливает переменные окружения для контейнера.
    `JAVA_OPTS=-Djenkins.install.runSetupWizard=false`: Отключает встроенный мастер настройки Jenkins при первом запуске, что позволяет настроить систему вручную или через предустановленные параметры.

7. !!! annotation "Параметры команды"
    `restart: unless-stopped`: Политика перезапуска контейнера. Контейнер будет автоматически перезапускаться при сбоях или перезагрузке хоста, пока не будет явно остановлен командой docker stop.

8. !!! annotation "Параметры команды"
    `volumes`: Определяет именованные тома, используемые в сервисе. jenkins_data будет создан Docker автоматически и привязан к `/var/jenkins_home` внутри контейнера для сохранения данных.

!!! tip "Совет для продакшена"
    Для продакшен-окружения замените `JAVA_OPTS` на:
    ```yaml
    environment:
      - JENKINS_ADMIN_ID=admin
      - JENKINS_ADMIN_PASSWORD=ваш_безопасный_пароль
    ```

## 3. 🚀 Запуск Jenkins

```bash
docker-compose up -d # (1)
```

1. !!! annotation "Параметры команды"
    `docker-compose up -d`: Запускает контейнеры в фоновом режиме. Флаг `-d` отделяет процесс от терминала.

## 4. 🔍 Проверка работы Jenkins

```bash
docker ps # (1)
```

1. !!! annotation "Параметры команды"
    `docker ps`: Показывает список запущенных контейнеров, включая `jenkins`.

```bash
curl http://localhost:8080 # (1)
```

2. !!! annotation "Параметры команды"
    `curl http://localhost:8080`: Проверяет доступность Jenkins. Ожидаемый ответ — "403 Forbidden", что указывает на запуск с требованием аутентификации.

<div class="navigation-buttons" style="display: flex; justify-content: space-between; margin-top: 40px;">
    <a href="/2_installations/docker/" class="md-button md-button--prev">
        <span class="twemoji">
            <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24"><path d="M20 11v2H8l5.5 5.5-1.42 1.42L4.16 12l7.92-7.92L13.5 5.5 8 11h12Z"></path></svg>
        </span> Установка Docker
    </a>
    <a href="/../" class="md-button md-button--next md-button--primary">
        Главная <span class="twemoji">
            <path d="M4 11v2h12l-5.5 5.5 1.42 1.42L19.84 12l-7.92-7.92L10.5 5.5 16 11H4Z"></path></svg>
        </span>
    </a>
    <a href="/3_configuration/security/" class="md-button md-button--next md-button--primary">
        Безопасность <span class="twemoji">
            <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24"><path d="M4 11v2h12l-5.5 5.5 1.42 1.42L19.84 12l-7.92-7.92L10.5 5.5 16 11H4Z"></path></svg>
        </span>
    </a>
</div>