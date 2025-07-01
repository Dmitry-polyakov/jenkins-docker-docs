# 🐳 Установка Docker и Docker Compose
### 1. 🔄 Обновление системы

```bash
# Обновление списка пакетов и установленных программ
sudo apt update && sudo apt upgrade -y # (1)
```

1. !!! annotation "Параметры команды"
	`sudo apt update && sudo apt upgrade -y`: Обновляет список пакетов и программы. Флаг -y автоматически подтверждает изменения.

```bash
# Перезагрузка для применения обновлений
sudo reboot # (1)
```

1. !!! annotation "Параметры команды"
	`sudo reboot`: Перезапускает систему для применения обновлений ядра.

### 2. 📦 Установка зависимостей Docker
```bash
# Установка необходимых пакетов для Docker
sudo apt install -y apt-transport-https ca-certificates curl software-properties-common # (1)
```

1. !!! annotation "Параметры команды" 
	- `sudo apt install -y ...`: Устанавливает пакеты для безопасного управления репозиториями.
	- `apt-transport-https`: Поддержка HTTPS для APT.
	- `ca-certificates`: Сертификаты SSL/TLS.
	- `curl`: Передача данных через URL.
	- `software-properties-common`: Управление репозиториями.

### 3. 🔑 Добавление репозитория Docker
```bash
# Добавление GPG-ключа Docker
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg # (1)
```

1. !!! annotation "Параметры команды"
	`curl -fsSL ... | sudo gpg --dearmor -o ...`: Скачивает и добавляет GPG-ключ Docker для проверки пакетов.

```bash
# Добавление репозитория Docker в источники APT
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null # (1)
```

1. !!! annotation "Параметры команды"
	`echo ... | sudo tee ...`: Настраивает репозиторий Docker для архитектуры системы и версии Ubuntu.

### 4. 🛠️ Установка Docker
```bash
# Обновление списка пакетов
sudo apt update # (1)
```

1. !!! annotation "Параметры команды"
	`sudo apt update`: Обновляет список пакетов с учетом нового репозитория.

```bash
# Установка компонентов Docker
sudo apt install -y docker-ce docker-ce-cli containerd.io # (1)
```

1. !!! annotation "Параметры команды"
	`sudo apt install -y ...`: Устанавливает Docker Engine, CLI и среду выполнения контейнеров.

```bash
# Проверка установки Docker
sudo docker --version # (1)
```

1. !!! annotation "Параметры команды"
	`sudo docker --version`: Выводит версию установленного Docker.


### 5. 👤 Настройка прав пользователя
```bash
# Добавление пользователя в группу docker
sudo usermod -aG docker $USER # (1)
```

1. !!! annotation "Параметры команды"
	`sudo usermod -aG docker $USER`: Дает пользователю права запускать Docker без sudo.

```bash
# Применение изменений группы
newgrp docker # (1)
```

1. !!! annotation "Параметры команды"
	`newgrp docker`: Активирует изменения группы без перезапуска сессии.

### 6. 📥 Установка Docker Compose
```bash
# Скачивание Docker Compose
sudo curl -L "https://github.com/docker/compose/releases/download/v2.23.0/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose # (1)
```

1. !!! annotation "Параметры команды"
	`sudo curl -L ... -o ...`: Скачивает бинарный файл Docker Compose для ОС и архитектуры системы.

```bash
# Назначение прав на выполнение
sudo chmod +x /usr/localTreasure/bin/docker-compose # (1)
```

1. !!! annotation "Параметры команды"
	`sudo chmod +x ...`: Делает файл Docker Compose исполняемым.

```bash
# Проверка установки
docker-compose --version # (1)
```

1. !!! annotation "Параметры команды"
	`docker-compose --version`: Подтверждает установленную версию Docker Compose.

<div class="navigation-buttons" style="display: flex; justify-content: space-between; margin-top: 40px;">
    <a href="/1_quickstart/" class="md-button md-button--prev">
        <span class="twemoji">
            <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24"><path d="M20 11v2H8l5.5 5.5-1.42 1.42L4.16 12l7.92-7.92L13.5 5.5 8 11h12Z"></path></svg>
        </span> Быстрый старт
    </a>
	<a href="/../" class="md-button md-button--next md-button--primary">
        Главная <span class="twemoji">
            <path d="M4 11v2h12l-5.5 5.5 1.42 1.42L19.84 12l-7.92-7.92L10.5 5.5 16 11H4Z"></path></svg>
        </span>
    </a>
    <a href="/2_installations/jenkins/" class="md-button md-button--next md-button--primary">
        Установка Jenkins <span class="twemoji">
            <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24"><path d="M4 11v2h12l-5.5 5.5 1.42 1.42L19.84 12l-7.92-7.92L10.5 5.5 16 11H4Z"></path></svg>
        </span>
    </a>
</div>