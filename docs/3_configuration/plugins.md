# 🔌 Установка плагинов

## 1. 🌐 Доступ к веб-интерфейсу

```bash
http://<IP_вашего_сервера>:8080 # (1)
```

1. !!! annotation "Объяснение команды"
    `http://<IP_вашего_сервера>:8080`: Открывает веб-интерфейс Jenkins для управления.

## 2. 🛠️ Установка необходимых плагинов

1. Перейдите в раздел: `Manage Jenkins > Plugins > Available plugins`.
2. В строке поиска найдите и установите следующие плагины:
    - `Docker Pipeline` (для работы с Docker-агентами)
    - `Docker API Plugin` (для доступа к Docker API)
    - `SSH Agent` (для безопасной работы с SSH-ключами)
3. Нажмите "Install without restart" и дождитесь завершения установки.

## 3. Настройка плагинов после установки

После установки плагинов:

1. Перейдите в Управление Jenkins > Настройка системы

2. Найдите раздел "Docker" и укажите:
    - Docker Host URI (обычно unix:///var/run/docker.sock)
    - Docker API Version

3. Сохраните изменения

## 4. Проверка работы плагинов

Создайте тестовый пайплайн:

```groovy
pipeline {
    agent {
        docker { image 'maven:3.8.6-jdk-11' }
    }
    stages {
        stage('Test') {
            steps {
                sh 'mvn --version'
            }
        }
    }
}
```

<div class="navigation-buttons" style="display: flex; justify-content: space-between; margin-top: 40px;">
    <a href="/3_configuration/security/" class="md-button md-button--prev">
        <span class="twemoji">
            <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24"><path d="M20 11v2H8l5.5 5.5-1.42 1.42L4.16 12l7.92-7.92L13.5 5.5 8 11h12Z"></path></svg>
        </span> Безопасность
    </a>
    <a href="/../" class="md-button md-button--next md-button--primary">
        Главная <span class="twemoji">
            <path d="M4 11v2h12l-5.5 5.5 1.42 1.42L19.84 12l-7.92-7.92L10.5 5.5 16 11H4Z"></path></svg>
        </span>
    </a>
    <a href="/3_configuration/docker_integration/" class="md-button md-button--next md-button--primary">
        Настройка Jenkins <span class="twemoji">
            <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24"><path d="M4 11v2h12l-5.5 5.5 1.42 1.42L19.84 12l-7.92-7.92L10.5 5.5 16 11H4Z"></path></svg>
        </span>
    </a>
</div>