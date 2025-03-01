# Telegram Bot с оплатой криптовалютой

Этот проект представляет собой Telegram-бота для онлайн-магазина, который позволяет пользователям просматривать товары, добавлять их в корзину и оплачивать заказы с помощью криптовалюты. Бот использует библиотеку `aiogram` для взаимодействия с Telegram API и `aiosend` для обработки криптоплатежей.

---

## Оглавление
1. [Установка и настройка](#установка-и-настройка)
2. [Структура проекта](#структура-проекта)
3. [Запуск бота](#запуск-бота)
4. [Функциональность](#функциональность)
5. [База данных](#база-данных)
6. [Конфигурация](#конфигурация)
7. [Лицензия](#лицензия)

---

## Установка и настройка

### Требования
- Python 3.8 или выше.
- Установленные зависимости (см. ниже).
- Токен бота от [BotFather](https://core.telegram.org/bots#botfather).
- Токен для работы с криптоплатежами (например, от [CryptoBot](https://t.me/CryptoBot)).

### Установка зависимостей
1. Клонируйте репозиторий:
   ```bash
   git clone https://github.com/B0doChKa/aiosend
   cd ваш-репозиторий
   ```
2. Установите зависимости:
   ```bash
   pip install aiogram aiosend python-dotenv sqlite3
   ```

---

## Структура проекта

- **`config.py`** — хранит название базы данных и токены
- **`database.py`** — отвечает за работу с базой данных (SQLite).
- **`keyboards.py`** — содержит клавиатуры для бота.
- **`handlers.py`** — содержит хендлеры для обработки команд и callback-запросов.
- **`main.py`** — основной файл для запуска бота.

---

## Запуск бота

1. Замените все данные в **`config.py`**

2. Запустите бота:
   ```bash
   python main.py
   ```

---

## Функциональность

### Основные команды
- **`/start`** — запуск бота и отображение главного меню.
- **Каталог товаров** — просмотр доступных товаров.
- **Корзина** — просмотр и управление товарами в корзине.
- **Оплата** — создание счета и оплата криптовалютой.

### Как это работает
1. Пользователь запускает бота командой `/start`.
2. Выбирает товары из каталога и добавляет их в корзину.
3. Переходит в корзину и оформляет заказ.
4. Оплачивает заказ криптовалютой через предоставленную ссылку.
5. После успешной оплаты бот уведомляет пользователя.

---

## База данных

Проект использует SQLite для хранения данных. База данных состоит из двух таблиц:
1. **`products`** — информация о товарах.
2. **`carts`** — корзины пользователей.

### Инициализация базы данных
При первом запуске бота база данных автоматически создается и заполняется тестовыми данными.

### Пример запросов
- Получить все товары:
  ```sql
  SELECT id, name, price FROM products;
  ```
- Получить корзину пользователя:
  ```sql
  SELECT p.id, p.name, p.price, c.quantity
  FROM carts c
  JOIN products p ON c.product_id = p.id
  WHERE c.user_id = ?;
  ```

---

## Конфигурация

### Файл `config.py`
- **`BOT_TOKEN`** — токен вашего Telegram-бота.
- **`CRYPTO_PAY_TOKEN`** — токен для работы с криптоплатежами.
- **`DATABASE_NAME`** — имя файла базы данных (по умолчанию `shop_bot.db`).

---

## Лицензия

Этот проект распространяется под лицензией [MIT](https://choosealicense.com/licenses/mit/). Вы можете свободно использовать, изменять и распространять код.

---

## Возможности для улучшения
- Добавление поддержки других платежных систем.
- Интеграция с реальным API для работы с товарами.
- Расширение функционала (например, история заказов, скидки).
