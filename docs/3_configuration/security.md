# 🔐 Первоначальная настройка Jenkins

## 1. 🔑 Получение пароля администратора

```bash
docker logs jenkins 2>&1 | grep "Please use the following password" -A 2 # (1)
```

1. !!! annotation "Объяснение команды"
    `docker logs jenkins 2>&1 | grep ...`: Извлекает начальный пароль администратора из логов контейнера.  
    - `2>&1`: Перенаправляет ошибки в стандартный вывод.  
    - `-A 2`: Показывает две строки после совпадения.

## 2. 📦 Установка стандартных плагинов

1. Перейдите по адресу в браузере:

```bash
http://<IP_вашего_сервера>:8080 # (1)
```

1. !!! annotation "Объяснение команды"
    `http://<IP_вашего_сервера>:8080`: Открывает веб-интерфейс Jenkins.

2. Введите полученный пароль.
3. Выберите "Install suggested plugins" для установки базовых плагинов (Git, Pipeline и др.).

## 3. 👤 Создание администратора

- Укажите имя пользователя и пароль (или пропустите, если они заданы в `docker-compose.yml` как `JENKINS_ADMIN_ID` и `JENKINS_ADMIN_PASSWORD`).

## 4. 🌐 Настройка URL

- Оставьте значение по умолчанию (`http://<IP_вашего_сервера>:8080`) или укажите свой URL (рекомендуется использовать домен с HTTPS в продакшене).

<div class="navigation-buttons" style="display: flex; justify-content: space-between; margin-top: 40px;">
    <a href="/2_installations/jenkins/" class="md-button md-button--prev">
        <span class="twemoji">
            <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24"><path d="M20 11v2H8l5.5 5.5-1.42 1.42L4.16 12l7.92-7.92L13.5 5.5 8 11h12Z"></path></svg>
        </span> Установка Jenkins
    </a>
    <a href="/../" class="md-button md-button--next md-button--primary">
        Главная <span class="twemoji">
            <path d="M4 11v2h12l-5.5 5.5 1.42 1.42L19.84 12l-7.92-7.92L10.5 5.5 16 11H4Z"></path></svg>
        </span>
    </a>
    <a href="/3_configuration/plugins/" class="md-button md-button--next md-button--primary">
        Плагины <span class="twemoji">
            <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24"><path d="M4 11v2h12l-5.5 5.5 1.42 1.42L19.84 12l-7.92-7.92L10.5 5.5 16 11H4Z"></path></svg>
        </span>
    </a>
</div>