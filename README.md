# 🛒 E-Commerce Platform with Telegram Bot

Полнофункциональная платформа интернет-магазина с Django админ-панелью и Telegram ботом для покупок. Включает каталог товаров, корзину, оформление заказов, автоматические Excel отчеты и систему подписок.

## 📋 Содержание

- [Обзор системы](#️-обзор-системы)
- [Особенности](#-особенности)
- [Технологии](#-технологии)
- [Архитектура](#️-архитектура)
- [Быстрый старт](#-быстрый-старт)
- [Конфигурация](#️-конфигурация)
- [Использование](#-использование)
- [Разработка](#-разработка)
- [Тестирование](#-тестирование)
- [Развертывание](#-развертывание)
- [Мониторинг](#-мониторинг)
- [Лицензия](#-лицензия)

## 🏗️ Обзор системы

Платформа состоит из двух основных компонентов:

### 🎛️ Django Admin Panel

Административная панель для управления:

- Товарами и категориями
- Заказами и пользователями
- FAQ и рассылками
- Медиафайлами

### 🤖 Telegram Bot

Интерактивный бот для клиентов с функциями:

- Просмотра каталога товаров
- Управления корзиной
- Оформления заказов
- Получения поддержки

## ✨ Особенности

### 🛍️ E-Commerce функционал

- **Каталог товаров**: Иерархические категории с подкатегориями
- **Корзина покупок**: Добавление, изменение количества, удаление товаров
- **Система заказов**: Полный цикл от оформления до обработки
- **Управление изображениями**: Загрузка и отображение фото товаров

### 📊 Отчетность и аналитика

- **Excel отчеты**: Автоматическая запись всех заказов
- **Статистика заказов**: Отслеживание продаж через админ-панель
- **Логирование**: Подробные логи всех операций

### 🔐 Безопасность и контроль

- **Система подписок**: Проверка подписки на каналы
- **Middleware защита**: Контроль доступа к функциям бота
- **Валидация данных**: Проверка всех пользовательских вводов

### 🎨 Пользовательский опыт

- **Интуитивная навигация**: Inline клавиатуры с пагинацией
- **FAQ система**: Часто задаваемые вопросы
- **Многоязычная поддержка**: Готовность к локализации

## 🛠 Технологии

### Backend

- **Django 5.2.3** - Web framework для админ-панели
- **Aiogram 3.20.0** - Telegram Bot framework
- **Python 3.13** - Основной язык программирования

### База данных

- **PostgreSQL** - Основная СУБД
- **SQLAlchemy 2.0.41** - ORM для Telegram бота
- **Django ORM** - ORM для админ-панели

### Архитектурные решения

- **Clean Architecture** - Разделение на слои (Domain/Application/Infrastructure)
- **Dependency Injection** - Dishka контейнер для управления зависимостями
- **Repository Pattern** - Абстракция доступа к данным

### Дополнительные технологии

- **Dynaconf 3.2.11** - Управление конфигурацией
- **OpenPyXL 3.1.5** - Генерация Excel отчетов
- **aiohttp 3.11.18** - HTTP клиент для изображений
- **Uvicorn 0.34.3** - ASGI сервер
- **WhiteNoise 6.9.0** - Обслуживание статических файлов

### Тестирование

- **pytest 8.4.1** - Фреймворк тестирования
- **pytest-asyncio** - Поддержка асинхронных тестов
- **E2E тесты** - Полное покрытие бизнес-логики

### DevOps

- **Docker & Docker Compose** - Контейнеризация
- **Volume mapping** - Персистентность данных
- **Multi-stage builds** - Оптимизация образов

## 🏗️ Архитектура

```text
E-Commerce Platform
├── 🎛️ Django Admin Panel (Port 8000)
│   ├── Management Interface
│   ├── Media Files Serving
│   └── Database Administration
│
├── 🤖 Telegram Bot
│   ├── Clean Architecture Layers
│   ├── DI Container (Dishka)
│   └── Excel Report Generation
│
├── 🗄️ Shared Database (PostgreSQL)
│   ├── Products & Categories
│   ├── Orders & Cart
│   ├── Users & Subscriptions
│   └── FAQ & Admin Data
│
└── 📁 Shared Volumes
    ├── /logs - Application logs
    ├── /reports - Excel reports
    └── /media - Product images
```

### Структура проекта

```text
test_task/
├── 📄 docker-compose.yaml       # Оркестрация сервисов
├── 📄 README.md                 # Документация
├── 📁 DjangoServer/             # Django админ-панель
│   ├── 📄 Dockerfile
│   ├── 📄 requirements.txt
│   ├── 📁 configs/              # Конфигурация
│   └── 📁 order_system/         # Django приложение
│       ├── 📁 admin/            # Настройки проекта
│       ├── 📁 management/       # Основное приложение
│       │   ├── admin.py         # Админ интерфейс
│       │   ├── models/          # Модели данных
│       │   └── tests/           # Тесты Django
│       └── 📁 static/           # Статические файлы
├── 📁 TelegramShop/             # Telegram бот
│   ├── 📄 Dockerfile
│   ├── 📄 requirements.txt
│   ├── 📄 pytest.ini
│   ├── 📁 configs/              # Конфигурация
│   ├── 📁 src/                  # Исходный код
│   │   ├── 📁 bootstrap/        # Инициализация и DI
│   │   ├── 📁 domain/           # Бизнес-логика
│   │   ├── 📁 application/      # Use Cases
│   │   ├── 📁 infrastructure/   # Внешние зависимости
│   │   └── 📁 presentation/     # Telegram интерфейс
│   └── 📁 tests/                # E2E тесты
│       └── 📁 e2e/
│           ├── routers/         # Тесты роутеров
│           ├── usecases/        # Тесты бизнес-логики
│           └── integration/     # Интеграционные тесты
└── 📁 logs/                     # Логи приложений
```

## 🚀 Быстрый старт

### Предварительные требования

- Docker и Docker Compose
- Git

### 1. Клонирование и настройка

```bash
# Клонирование репозитория
git clone <repository-url>
cd test_task

# Создание файлов конфигурации
cp DjangoServer/configs/config.toml DjangoServer/configs/secret.toml
cp TelegramShop/configs/config.toml TelegramShop/configs/secret.toml
```

### 2. Настройка секретов

Отредактируйте файлы `secret.toml` в обеих директориях:

**DjangoServer/configs/secret.toml:**
```toml

[default.database]
user = "shop_user"
password = "shop_password"
name = "shop_db"

[default.django]
secret_key = "your-django-secret-key-here"
```

**TelegramShop/configs/secret.toml:**

```toml
[default.database]
user = "shop_user"
password = "shop_password"
name = "shop_db"

[default.telegram]
token = "your_telegram_bot_token"
chats_id = ["@your_channel"]
```

### 3. Запуск платформы

```bash
# Запуск всех сервисов
docker compose up -d

# Применение миграций Django
docker compose exec django python manage.py migrate

# Создание суперпользователя
docker compose exec django python manage.py createsuperuser

# Сбор статических файлов
docker compose exec django python manage.py collectstatic --noinput
```

### 4. Проверка работы

- **Django Admin**: <http://localhost:8000/admin/>
- **Telegram Bot**: Найдите бота в Telegram и отправьте `/start`
- **Логи**: `docker compose logs -f`

## ⚙️ Конфигурация

### Переменные окружения

```bash
# Выбор окружения (default/production)
ENV_FOR_DYNACONF=production

# Настройки базы данных
POSTGRES_DB=shop_db
POSTGRES_USER=shop_user
POSTGRES_PASSWORD=shop_password
```

### Файлы конфигурации

Каждый сервис использует **Dynaconf** для управления настройками:

- `configs/config.toml` - основные настройки
- `configs/secret.toml` - секретные данные (не в git)

### Пример продакшн конфигурации

```toml
[production]
log_level = "WARNING"
debug = false

[production.database]
host = "postgres"
port = 5432
user = "shop_user"
password = "secure_password"
name = "shop_db"

[production.django]
secret_key = "production-secret-key"

[production.telegram]
token = "production_bot_token"
chats_id = ["@production_channel"]
```

## 📖 Использование

### Django Admin Panel

1. **Управление товарами**:
   - Создание категорий и подкатегорий
   - Добавление товаров с изображениями
   - Установка цен и описаний

2. **Обработка заказов**:
   - Просмотр всех заказов
   - Отслеживание статусов
   - Управление пользователями

3. **Контент-менеджмент**:
   - Редактирование FAQ
   - Создание рассылок
   - Управление подписками

### Telegram Bot

1. **Для пользователей**:

   ```
   /start - Регистрация и главное меню
   📦 Каталог - Просмотр товаров
   🛒 Корзина - Управление покупками
   ❓ FAQ - Получение помощи
   ```

2. **Процесс покупки**:
   - Выбор категории → товара
   - Добавление в корзину с указанием количества
   - Оформление заказа с контактными данными
   - Выбор способа оплаты
   - Автоматическое сохранение в БД и Excel

### Excel отчеты

Все заказы автоматически записываются в `./reports/orders.xlsx`:

| Дата | ID пользователя | ФИО | Адрес | Телефон | Способ оплаты | Товары | Сумма |
|------|----------------|-----|-------|---------|---------------|--------|-------|
| 2025-01-15 10:30 | 12345 | Иван Петров | ул. Ленина, 1 | +79001234567 | Карта | iPhone x1 | 999.99 |

## 🔧 Разработка

### Локальная разработка

```bash
# Django разработка
cd DjangoServer/order_system
python manage.py runserver

# Telegram Bot разработка
cd TelegramShop
python -m src.bootstrap.main
```

### Добавление новых функций

#### Django Admin:

1. Создайте модель в `management/models/`
2. Зарегистрируйте в `management/admin.py`
3. Создайте миграцию: `python manage.py makemigrations`
4. Примените: `python manage.py migrate`

#### Telegram Bot:

1. Создайте сущность в `domain/entities/`
2. Определите интерфейс репозитория в `domain/repositories/`
3. Реализуйте репозиторий в `infrastructure/database/repositories/`
4. Создайте Use Case в `application/usecases/`
5. Добавьте роутер в `presentation/telegram/routers/`
6. Зарегистрируйте в DI контейнере

### Архитектурные принципы

**Clean Architecture слои:**

- **Domain**: Бизнес-сущности и правила
- **Application**: Use Cases и интерфейсы
- **Infrastructure**: Внешние зависимости
- **Presentation**: Пользовательский интерфейс

**Dependency Injection:**

```python
class UseCasesProvider(Provider):
    @provide(scope=Scope.REQUEST)
    async def create_order_use_case(
        self, 
        cart_repo: CartRepositoryInterface,
        order_repo: OrderRepositoryInterface,
        excel_client: ExcelClientInterface
    ) -> CreateOrderUseCase:
        return CreateOrderUseCase(cart_repo, order_repo, excel_client)
```

## 🧪 Тестирование

### Django тесты

```bash
# Запуск всех тестов Django
docker compose exec django python manage.py test

# Тесты с покрытием
docker compose exec django coverage run --source='.' manage.py test
docker compose exec django coverage report
```

### Telegram Bot тесты

```bash
# E2E тесты
docker compose exec telegram-bot pytest

# Конкретные категории
docker compose exec telegram-bot pytest tests/e2e/usecases/
docker compose exec telegram-bot pytest tests/e2e/integration/

# С покрытием
docker compose exec telegram-bot pytest --cov=src
```

### Структура тестов

**Django:**

- Unit тесты моделей
- Тесты связей между моделями
- Тесты админ интерфейса

**Telegram Bot:**

- E2E тесты use cases
- Интеграционные тесты (Excel, БД)
- Тесты бизнес-логики

## 🚀 Развертывание

### Docker Compose (рекомендуется)

```yaml
version: '3.8'
services:
  postgres:
    image: postgres:15
    environment:
      POSTGRES_DB: shop_db
      POSTGRES_USER: shop_user
      POSTGRES_PASSWORD: shop_password
    volumes:
      - postgres_data:/var/lib/postgresql/data

  django:
    build: ./DjangoServer
    ports:
      - "8000:8000"
    depends_on:
      - postgres
    volumes:
      - ./logs:/app/logs
      - ./media:/app/order_system/media
    environment:
      - ENV_FOR_DYNACONF=production

  telegram-bot:
    build: ./TelegramShop
    depends_on:
      - postgres
      - django
    volumes:
      - ./logs:/app/logs
      - ./reports:/app/reports
    environment:
      - ENV_FOR_DYNACONF=production

volumes:
  postgres_data:
```

### Продакшн развертывание

1. **Настройка сервера**:

   ```bash
   # Установка Docker
   curl -fsSL https://get.docker.com -o get-docker.sh
   sh get-docker.sh
   
   # Установка Docker Compose
   sudo curl -L "https://github.com/docker/compose/releases/download/v2.20.0/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
   sudo chmod +x /usr/local/bin/docker-compose
   ```

2. **Настройка окружения**:

   ```bash
   # Создание продакшн конфигурации
   export ENV_FOR_DYNACONF=production
   
   # Настройка файрвола
   sudo ufw allow 8000/tcp
   sudo ufw enable
   ```

3. **Запуск в продакшн**:

   ```bash
   docker compose up -d
   ```

### Backup и восстановление

```bash
# Backup базы данных
docker compose exec postgres pg_dump -U shop_user shop_db > backup.sql

# Восстановление
docker compose exec -T postgres psql -U shop_user shop_db < backup.sql

# Backup файлов
tar -czf media_backup.tar.gz media/ reports/
```

## 📊 Мониторинг

### Логирование

```bash
# Просмотр логов всех сервисов
docker compose logs -f

# Логи конкретного сервиса
docker compose logs -f django
docker compose logs -f telegram-bot
docker compose logs -f postgres

# Логи с фильтрацией
docker compose logs --since="1h" django
```

### Мониторинг производительности

```bash
# Статистика контейнеров
docker stats

# Использование дискового пространства
docker system df

# Очистка неиспользуемых ресурсов
docker system prune -a
```

### Health checks

```bash
# Проверка статуса сервисов
docker compose ps

# Проверка доступности Django
curl -f http://localhost:8000/admin/ || echo "Django недоступен"

# Проверка базы данных
docker compose exec postgres pg_isready -U shop_user
```

### Метрики и алерты

Рекомендуется настроить:

- **Prometheus + Grafana** для метрик
- **ELK Stack** для централизованного логирования
- **Alertmanager** для уведомлений о проблемах

## 🔒 Безопасность

### Рекомендации по безопасности

1. **Секреты**:
   - Используйте сильные пароли
   - Регулярно меняйте токены
   - Не коммитьте `secret.toml` файлы

2. **Сеть**:
   - Используйте HTTPS в продакшн
   - Настройте файрвол
   - Ограничьте доступ к админ-панели

3. **База данных**:
   - Регулярные бэкапы
   - Шифрование соединений
   - Мониторинг подозрительной активности

4. **Контейнеры**:
   - Регулярные обновления образов
   - Сканирование на уязвимости
   - Минимальные привилегии

## 🤝 Вклад в проект

1. Fork репозитория
2. Создайте feature branch (`git checkout -b feature/amazing-feature`)
3. Commit изменения (`git commit -m 'Add amazing feature'`)
4. Push в branch (`git push origin feature/amazing-feature`)
5. Создайте Pull Request

### Стандарты кода

- **Python**: PEP 8, type hints
- **Django**: Django best practices
- **Тесты**: Обязательное покрытие новой функциональности
- **Документация**: Обновление README при изменениях API

## 📝 Лицензия

Этот проект лицензирован под MIT License - см. файл [LICENSE](LICENSE) для деталей.

---

## 📞 Поддержка

Если у вас есть вопросы или проблемы:

1. Проверьте [Issues](../../issues) на GitHub
2. Создайте новый Issue с подробным описанием
3. Приложите логи и конфигурацию (без секретов!)

**Полезные команды для диагностики:**

```bash
# Проверка статуса всех сервисов
docker compose ps

# Просмотр логов с ошибками
docker compose logs --tail=100 | grep -i error

# Проверка подключения к БД
docker compose exec postgres psql -U shop_user -d shop_db -c "SELECT version();"

# Тест Telegram бота
docker compose exec telegram-bot python -c "from src.config import config; print('Config loaded successfully')"
```
