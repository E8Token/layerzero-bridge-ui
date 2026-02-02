# Docker Setup for LayerZero Bridge UI

## Файлы конфигурации

- **Dockerfile** - Production build с multi-stage сборкой
- **Dockerfile.dev** - Development версия с hot reload
- **docker-compose.yml** - Конфигурация Docker Compose
- **.dockerignore** - Исключения для Docker build

## Использование

### Production режим

Запустить production build:

```bash
docker-compose up -d
```

Приложение будет доступно на `http://localhost:3000`

### Development режим

Запустить development версию с hot reload:

```bash
docker-compose --profile dev up app-dev
```

Приложение будет доступно на `http://localhost:3001`

## Переменные окружения

Создайте файл `.env` в корне проекта со следующими переменными:

```env
# Пример переменных окружения
NEXT_PUBLIC_THIRDWEB_CLIENT_ID=your_client_id
NEXT_PUBLIC_ENVIRONMENT=testnet
# Добавьте другие необходимые переменные
```

Затем обновите `docker-compose.yml` для загрузки этих переменных:

```yaml
environment:
  - NEXT_PUBLIC_THIRDWEB_CLIENT_ID=${NEXT_PUBLIC_THIRDWEB_CLIENT_ID}
  - NEXT_PUBLIC_ENVIRONMENT=${NEXT_PUBLIC_ENVIRONMENT}
```

## Команды Docker

### Сборка образов

```bash
# Production
docker-compose build

# Development
docker-compose build app-dev
```

### Просмотр логов

```bash
docker-compose logs -f app
```

### Остановка контейнеров

```bash
docker-compose down
```

### Пересборка и запуск

```bash
docker-compose up -d --build
```

## Примечания

- Production образ использует multi-stage build для оптимизации размера
- Для production требуется `output: "standalone"` в next.config.js (уже добавлено)
- Development образ монтирует исходный код для hot reload
- Используется pnpm в качестве пакетного менеджера
