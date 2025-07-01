# ⚙️ Дополнительные настройки

## 1. 📏 Ограничение ресурсов

В разделе `Container settings` укажите:
- `Memory limit: 4096M` (ограничение RAM)
- `CPU shares: 512` (приоритет CPU)

## 2. 🏷️ Настройка лейблов

Добавьте лейбл в `Jenkinsfile` для выбора агента:

```groovy
agent {
    label 'docker-agent'
}
```

<div class="navigation-buttons" style="display: flex; justify-content: space-between; margin-top: 40px;">
    <a href="/4_usage/basic/" class="md-button md-button--prev">
        <span class="twemoji">
            <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24"><path d="M20 11v2H8l5.5 5.5-1.42 1.42L4.16 12l7.92-7.92L13.5 5.5 8 11h12Z"></path></svg>
        </span> Базовые пайплайны
    </a>
    <a href="/../" class="md-button md-button--next md-button--primary">
        Главная <span class="twemoji">
            <path d="M4 11v2h12l-5.5 5.5 1.42 1.42L19.84 12l-7.92-7.92L10.5 5.5 16 11H4Z"></path></svg>
        </span>
    </a>
    <a href="/4_usage/troubleshooting/" class="md-button md-button--next md-button--primary">
        Решение проблем <span class="twemoji">
            <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24"><path d="M4 11v2h12l-5.5 5.5 1.42 1.42L19.84 12l-7.92-7.92L10.5 5.5 16 11H4Z"></path></svg>
        </span>
    </a>
</div>