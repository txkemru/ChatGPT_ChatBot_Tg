# Инструкция по установке ChatGPT Telegram Бота

## Предварительные требования

1. **Docker и Docker Compose** - должны быть установлены на вашей системе
2. **Telegram Bot Token** - получите у [@BotFather](https://t.me/BotFather)
3. **OpenAI API Key** - получите на [platform.openai.com](https://platform.openai.com/api-keys)

## Пошаговая установка

### 1. Клонирование репозитория
```bash
git clone <ваш-репозиторий>
cd chatgpt_telegram_bot-main
```

### 2. Настройка конфигурации

#### Создание файлов конфигурации:
```bash
cp config/config.example.yml config/config.yml
cp config/config.example.env config/config.env
```

#### Редактирование config/config.yml:
Откройте файл `config/config.yml` и заполните следующие поля:

```yaml
# Токен вашего Telegram бота
telegram_token: "YOUR_TELEGRAM_BOT_TOKEN"

# Ключ API OpenAI
openai_api_key: "YOUR_OPENAI_API_KEY"

# Остальные настройки можно оставить по умолчанию
```

#### Редактирование config/config.env (опционально):
Если нужно изменить настройки MongoDB или Mongo Express:

```env
# Локальный путь для хранения MongoDB
MONGODB_PATH=./mongodb

# Порт MongoDB
MONGODB_PORT=27017

# Порт Mongo Express (веб-интерфейс для MongoDB)
MONGO_EXPRESS_PORT=8081

# Учетные данные для Mongo Express
MONGO_EXPRESS_USERNAME=admin
MONGO_EXPRESS_PASSWORD=your_secure_password
```

### 3. Запуск бота

#### Первый запуск:
```bash
docker-compose --env-file config/config.env up --build
```

#### Последующие запуски:
```bash
docker-compose --env-file config/config.env up
```

#### Запуск в фоновом режиме:
```bash
docker-compose --env-file config/config.env up -d
```

### 4. Проверка работы

1. Найдите вашего бота в Telegram по имени
2. Отправьте команду `/start`
3. Бот должен ответить приветственным сообщением

## Управление ботом

### Основные команды:
- `/start` - Начать работу с ботом
- `/help` - Показать справку
- `/new` - Начать новый диалог
- `/mode` - Выбрать режим чата
- `/settings` - Настройки модели
- `/balance` - Показать баланс использования
- `/retry` - Перегенерировать последний ответ
- `/cancel` - Отменить текущую операцию

### Режимы чата:
- 👩🏼‍🎓 **Общий Ассистент** - для общих вопросов
- 👩🏼‍💻 **Помощник по коду** - для программирования
- 👩‍🎨 **Художник** - для генерации изображений
- 🇬🇧 **Английский Репетитор** - для изучения английского
- 💡 **Генератор Идей Стартапов** - для бизнес-идей
- 📝 **Улучшитель Текста** - для улучшения текстов
- 🧠 **Психолог** - для психологической поддержки
- 🚀 **Илон Маск** - для разговоров в стиле Илона Маска
- 🌟 **Мотиватор** - для мотивации
- 💰 **Заработок Денег** - для бизнес-советов
- 📊 **SQL Помощник** - для работы с базами данных
- 🧳 **Путеводитель** - для туристических советов
- 🥒 **Рик Санчез** - для разговоров в стиле Рика и Морти
- 🧮 **Бухгалтер** - для финансовых вопросов
- 🎬 **Эксперт по Фильмам** - для рекомендаций фильмов

## Мониторинг и администрирование

### Просмотр логов:
```bash
docker-compose logs -f chatgpt_telegram_bot
```

### Остановка бота:
```bash
docker-compose down
```

### Перезапуск бота:
```bash
docker-compose restart chatgpt_telegram_bot
```

### Доступ к MongoDB через веб-интерфейс:
Если настроен Mongo Express, откройте в браузере:
```
http://localhost:8081
```

## Безопасность

### Ограничение доступа:
В файле `config/config.yml` можно ограничить доступ к боту:

```yaml
allowed_telegram_usernames: 
  - "your_username"
  - 123456789  # ID пользователя
  - -987654321  # ID группы (отрицательное число)
```

### Смена паролей:
Обязательно смените пароли по умолчанию в `config/config.env`.

## Устранение неполадок

### Бот не отвечает:
1. Проверьте правильность токена Telegram бота
2. Убедитесь, что OpenAI API ключ действителен
3. Проверьте логи: `docker-compose logs chatgpt_telegram_bot`

### Ошибки Docker:
1. Убедитесь, что Docker запущен
2. Проверьте, что порты не заняты другими приложениями
3. Попробуйте пересобрать образы: `docker-compose build --no-cache`

### Проблемы с API:
1. Проверьте баланс на OpenAI
2. Убедитесь, что API ключ имеет необходимые разрешения
3. Проверьте лимиты API

## Обновление бота

```bash
git pull
docker-compose --env-file config/config.env up --build -d
```

## Поддержка

При возникновении проблем:
1. Проверьте логи бота
2. Убедитесь в правильности конфигурации
3. Проверьте статус OpenAI API
4. Создайте issue в репозитории с описанием проблемы 