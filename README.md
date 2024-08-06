# telegrambot

Этот проект представляет собой простого Telegram-бота, созданного с использованием библиотеки `python-telegram-bot`. Бот отвечает на команды `/start` и `/help`.

## Установка

1. Склонируйте репозиторий:
    ```bash
    git clone https://github.com/zolotarevinc/telegrambot.git
    ```

2. Перейдите в директорию проекта:
    ```bash
    cd telegrambot
    ```

3. Создайте виртуальное окружение и активируйте его:
    ```bash
    python -m venv venv
    source venv/bin/activate   # Для Windows используйте `venv\Scripts\activate`
    ```

4. Установите зависимости:
    ```bash
    pip install -r requirements.txt
    ```

## Настройка

1. Получите токен для вашего Telegram-бота у [BotFather](https://core.telegram.org/bots#6-botfather).

2. Создайте файл `.env` в корневой директории проекта и добавьте туда ваш токен:
    ```env
    TELEGRAM_TOKEN=your_telegram_bot_token
    ```

## Использование

1. Запустите бота:
    ```bash
    python bot.py
    ```

2. В Telegram найдите вашего бота и отправьте команду `/start` или `/help`.

## Команды

- `/start` - Начало работы с ботом. Отправляет приветственное сообщение.
- `/help` - Отправляет сообщение с помощью.

## Пример кода

**bot.py**:
```python
import logging
import os
from telegram import Update
from telegram.ext import Updater, CommandHandler, CallbackContext
from dotenv import load_dotenv

# Enable logging
logging.basicConfig(
    format='%(asctime)s - %(name)s - %(levelname)s - %(message)s', level=logging.INFO
)
logger = logging.getLogger(__name__)

# Load environment variables
load_dotenv()
TOKEN = os.getenv('TELEGRAM_TOKEN')

# Define a few command handlers
def start(update: Update, context: CallbackContext) -> None:
    """Send a message when the command /start is issued."""
    update.message.reply_text('Hi!')

def help_command(update: Update, context: CallbackContext) -> None:
    """Send a message when the command /help is issued."""
    update.message.reply_text('Help!')

def main() -> None:
    """Start the bot."""
    # Create the Updater and pass it your bot's token.
    updater = Updater(TOKEN)

    # Get the dispatcher to register handlers
    dispatcher = updater.dispatcher

    # on different commands - answer in Telegram
    dispatcher.add_handler(CommandHandler("start", start))
    dispatcher.add_handler(CommandHandler("help", help_command))

    # Start the Bot
    updater.start_polling()

    # Run the bot until you press Ctrl-C or the process receives SIGINT, SIGTERM or SIGABRT.
    updater.idle()

if __name__ == '__main__':
    main()
# telegrambot
