# ⚡ Быстрый старт

Этот раздел поможет быстро запустить Jenkins с Docker Compose.

### 1. 📦 Установка Docker и Docker Compose

Подробные шаги смотрите в Установка Docker.

### 2. 📁 Создание директории и конфигурации Jenkins

```bash
mkdir ~/jenkins && cd ~/jenkins # (1)
nano docker-compose.yml # (2)
```

1.  !!! annotation "Параметры команды"
    `mkdir ~/jenkins && cd ~/jenkins`: Создает директорию jenkins и переходит в нее.

2.  !!! annotation "Параметры команды"
    `nano docker-compose.yml`: Открывает редактор для создания файла конфигурации.

### 3. 🛠️ Настройка docker-compose.yml

Вставьте следующий код в docker-compose.yml:

```yaml
version: '3.8'
services:
  jenkins:
    image: jenkins/jenkins:lts-jdk17
    container_name: jenkins
    user: root
    ports:
      - "8080:8080"
      - "50000:50000"
    volumes:
      - jenkins_data:/var/jenkins_home
      - /var/run/docker.sock:/var/run/docker.sock
    environment:
      - JAVA_OPTS=-Djenkins.install.runSetupWizard=false
    restart: unless-stopped
volumes:
  jenkins_data:
```

!!! tip "Совет для продакшена"
    Для продакшен-окружения задайте учетные данные администратора:
    `yaml environment: - JENKINS_ADMIN_ID=admin - JENKINS_ADMIN_PASSWORD=ваш_безопасный_пароль`

### 4. 🚀 Запуск Jenkins

```bash
docker-compose up -d # (1)
```

1.  !!! annotation "Параметры команды"
    `docker-compose up -d`: Запускает контейнеры в фоновом режиме.

### 5. 🔍 Проверка работы Jenkins

```bash
docker ps # (1)
curl http://localhost:8080 # (2)
```

1.  !!! annotation "Параметры команды"
    `docker ps`: Показывает список запущенных контейнеров, включая jenkins.

2.  !!! annotation "Параметры команды"
    `curl http://localhost:8080`: Проверяет доступность Jenkins (ожидается "403 Forbidden").

Перейдите к Начальной настройке для дальнейших шагов.

<div class="navigation-buttons" style="display: flex; justify-content: space-between; margin-top: 40px;">
    <a href="/../" class="md-button md-button--prev">
        <span class="twemoji">
            <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24"><path d="M20 11v2H8l5.5 5.5-1.42 1.42L4.16 12l7.92-7.92L13.5 5.5 8 11h12Z"></path></svg>
        </span> Главная
    </a>
    <a href="/2_installations/docker/" class="md-button md-button--next md-button--primary">
        Установка Docker <span class="twemoji">
            <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24"><path d="M4 11v2h12l-5.5 5.5 1.42 1.42L19.84 12l-7.92-7.92L10.5 5.5 16 11H4Z"></path></svg>
        </span>
    </a>
</div>