# Тестовое задание DevOps

### Описание проекта
Развертывание простого веб-приложения на Python, работающего через реверс-прокси Nginx в Docker-контейнерах.

### Архитектура схемы
Взаимодействие компонентов организовано внутри изолированной Docker-сети
- **Nginx (порт 80)**: Принимает внешние HTTP-запросы и проксирует их на backend.
- **Backend (порт 8080)**: HTTP-сервер на Python, недоступен извне напрямую (только через Nginx).

**Схема взаимодействия:**
```
[ User ] --- (port 80) ---> [ Nginx Container ] --- (internal network) ---> [ Backend Container (port 8080) ]
```

## Технологический стек
- **Python 3.11-slim**: Базовый образ для минимизации размера.
- **Nginx: Официальный** стабильный образ.
- **Docker & Docker Compose**: Инструменты оркестрации.

## Как запустить проект
Убедитесь, что у вас установлены Docker и Docker Compose.
Склонируйте репозиторий:
```bash
git clone https://github.com/kirillgt33/DevOpsTestTask
cd dev_ops_test_task
```

Запустите сервисы в фоновом режиме:
```bash
docker-compose up -d
```
## Как проверить результат
Выполните запрос к локальному хосту:
```bash
curl http://localhost
```

Ожидаемый ответ:
Hello from Effective Mobile!

![image](https://github.com/user-attachments/assets/da2f4a11-a0d6-40b5-8bfe-b17cf1bb1ccb)

## Troubleshooting
- **Контейнеры не поднимаются:** Проверьте, не занят ли порт 80 другим процессом: `sudo lsof -i :80`.
- **Ошибка 502:** Убедитесь, что backend-контейнер прошел стадию Healthcheck (`docker ps`).
- **Просмотр логов в реальном времени:** `docker-compose logs -f`.