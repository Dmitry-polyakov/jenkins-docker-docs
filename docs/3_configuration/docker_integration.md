# 🐳 Настройка Jenkins для работы с Docker

## 1. 🔑 Генерация SSH-ключей

```bash
ssh-keygen -t rsa -b 4096 -f ~/.ssh/jenkins_docker_key -N "" # (1)
```

1. !!! annotation "Объяснение команды"
    - `ssh-keygen ...`: Создает пару SSH-ключей для безопасного подключения.  
    - `-t rsa`: Тип ключа RSA.  
    - `-b 4096`: Длина ключа для безопасности.  
    - `-f ~/.ssh/jenkins_docker_key`: Путь для сохранения ключей.  
    - `-N ""`: Без фразы-пароля для автоматизации.

## 2. 📂 Создание директории для ключей

```bash
mkdir -p ~/.ssh # (1)
```

1. !!! annotation "Объяснение команды"
    `mkdir -p ~/.ssh`: Создает директорию `.ssh`, если она отсутствует.

## 3. 🔗 Добавление публичного ключа

```bash
cat ~/.ssh/jenkins_docker_key.pub >> ~/.ssh/authorized_keys # (1)
```

1. !!! annotation "Объяснение команды"
    `cat ... >> ...`: Добавляет публичный ключ в файл авторизации.

## 4. 🔍 Проверка ключа

```bash
cat ~/.ssh/authorized_keys # (1)
```

1. !!! annotation "Объяснение команды"
    `cat ~/.ssh/authorized_keys`: Проверяет содержимое файла, чтобы убедиться, что ключ добавлен.

## 5. 🔐 Настройка прав доступа

```bash
chmod 600 ~/.ssh/jenkins_docker_key* # (1)
chmod 700 ~/.ssh # (2)
```

1. !!! annotation "Объяснение команды"
    `chmod 600 ~/.ssh/jenkins_docker_key*`: Ограничивает доступ к ключам только владельцу.

2. !!! annotation "Объяснение команды"
    `chmod 700 ~/.ssh`: Ограничивает доступ к директории `.ssh`.

## 6. 📋 Проверка прав

```bash
ls -la ~/.ssh/ # (1)
```

1. !!! annotation "Объяснение команды"
    `ls -la ~/.ssh/`: Выводит список файлов с правами доступа для проверки.

## 7. 💾 Добавление учетных данных в Jenkins

1. Перейдите в: `Manage Jenkins > Credentials > System > Global credentials > Add credentials`.
2. Заполните поля:
   - Kind: `SSH Username with private key`
   - ID: `docker-host-key` (опционально)
   - Username: `ubuntu` (или ваш пользователь)
   - Private Key: Вставьте содержимое `cat ~/.ssh/jenkins_docker_key`
3. Сохраните.

## 8. ☁️ Настройка Docker Cloud

1. Перейдите в: `Manage Jenkins > Nodes and Clouds > Configure Clouds`.
2. Нажмите "Add a new cloud" и выберите "Docker".
3. Настройте Docker Host:
   - Name: `local-docker` (или любое имя)
   - Docker Host URI:
     - Локальный хост: `unix:///var/run/docker.sock`
     - Удаленный хост: `tcp://<IP>:2375` (рекомендуется TLS)
   - Credentials: Выберите `docker-host-key`
4. Нажмите "Test Connection" (должно отобразиться `Docker version XX.XX`).
5. Сохраните настройки.

<div class="navigation-buttons" style="display: flex; justify-content: space-between; margin-top: 40px;">
    <a href="/3_configuration/plugins/" class="md-button md-button--prev">
        <span class="twemoji">
            <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24"><path d="M20 11v2H8l5.5 5.5-1.42 1.42L4.16 12l7.92-7.92L13.5 5.5 8 11h12Z"></path></svg>
        </span> Плагины
    </a>
    <a href="/../" class="md-button md-button--next md-button--primary">
        Главная <span class="twemoji">
            <path d="M4 11v2h12l-5.5 5.5 1.42 1.42L19.84 12l-7.92-7.92L10.5 5.5 16 11H4Z"></path></svg>
        </span>
    </a>
    <a href="/4_usage/pipelines/basic/" class="md-button md-button--next md-button--primary">
        Базовые пайплайны <span class="twemoji">
            <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24"><path d="M4 11v2h12l-5.5 5.5 1.42 1.42L19.84 12l-7.92-7.92L10.5 5.5 16 11H4Z"></path></svg>
        </span>
    </a>
</div>