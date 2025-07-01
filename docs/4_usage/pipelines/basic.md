# 🚀 Проверка работоспособности

## 1. 📋 Создание тестового пайплайна

1. Перейдите в: `New Item > Pipeline`.
2. Вставьте следующий код:

```groovy
pipeline {
    agent any
    stages {
        stage('Test Docker') {
            steps {
                script {
                    sh 'docker --version'
                }
            }
        }
    }
}
```

3. Нажмите "Build Now" и проверьте логи для вывода версии Docker.

<div class="navigation-buttons" style="display: flex; justify-content: space-between; margin-top: 40px;">
    <a href="/3_configuration/docker_integration/" class="md-button md-button--prev">
        <span class="twemoji">
            <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24"><path d="M20 11v2H8l5.5 5.5-1.42 1.42L4.16 12l7.92-7.92L13.5 5.5 8 11h12Z"></path></svg>
        </span> Настройка Jenkins
    </a>
    <a href="/../" class="md-button md-button--next md-button--primary">
        Главная <span class="twemoji">
            <path d="M4 11v2h12l-5.5 5.5 1.42 1.42L19.84 12l-7.92-7.92L10.5 5.5 16 11H4Z"></path></svg>
        </span>
    </a>
    <a href="/4_usage/pipelines/advanced/" class="md-button md-button--next md-button--primary">
        Продвинутые пайплайны <span class="twemoji">
            <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24"><path d="M4 11v2h12l-5.5 5.5 1.42 1.42L19.84 12l-7.92-7.92L10.5 5.5 16 11H4Z"></path></svg>
        </span>
    </a>
</div>