# AiDockerMetrics

AiDockerMetrics — это Spring Boot сервис для анализа тональности текста с помощью модели машинного обучения, развёрнутый в Docker и готовый к CI/CD через GitHub Actions.

## Возможности
- REST API для анализа тональности текста
- Использование кастомной ML-модели (JSON)
- Готовый Dockerfile для контейнеризации
- Автоматическая сборка и публикация Docker-образа в GitHub Container Registry

## Быстрый старт

### Локальный запуск

1. Склонируйте репозиторий:
   ```sh
   git clone https://github.com/<your-username>/AiDockerMetrics.git
   cd AiDockerMetrics
   ```
2. Соберите и запустите приложение:
   ```sh
   ./mvnw spring-boot:run
   ```

### Запуск в Docker

1. Соберите образ:
   ```sh
   docker build -t aidockermetrics:latest .
   ```
2. Запустите контейнер:
   ```sh
   docker run -p 8080:8080 aidockermetrics:latest
   ```

### CI/CD
- При пуше в ветку `main` автоматически собирается и публикуется Docker-образ в GitHub Container Registry (`ghcr.io`).
- Файл workflow: `.github/workflows/docker-image.yml`.

## API

- `POST /sentiment`
  - Тело запроса: `{ "text": "Ваш текст" }`
  - Ответ: `{ "sentiment": "positive|neutral|negative", "score": float }`

## Структура проекта
- `src/main/java/ru/mishazx/spring/services/aidockermetrics/` — основной код приложения
- `src/main/resources/model/sentiment-model.json` — ML-модель
- `Dockerfile` — описание контейнера
- `.github/workflows/docker-image.yml` — CI/CD
