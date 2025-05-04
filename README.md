import telebot
from telebot import types
import os
from dotenv import load_dotenv

# Завантаження змінних з .env
load_dotenv()
BOT_TOKEN = os.getenv('BOT_TOKEN')

bot = telebot.TeleBot(BOT_TOKEN)

@bot.message_handler(commands=['start'])
def send_welcome(message):
    markup = types.ReplyKeyboardMarkup(resize_keyboard=True)
    markup.add("Про нас", "Послуги", "Зв'язок")
    bot.send_message(message.chat.id, "Вітаємо! Оберіть опцію з меню:", reply_markup=markup)

@bot.message_handler(func=lambda message: True)
def handle_message(message):
    if message.text == "Про нас":
        bot.send_message(message.chat.id, "Ми — команда професіоналів у сфері...")
    elif message.text == "Послуги":
        bot.send_message(message.chat.id, "Наші послуги: створення ботів, дизайн, маркетинг...")
    elif message.text == "Зв'язок":
        bot.send_message(message.chat.id, "Зв'яжіться з нами: @your_contact")
    else:
        bot.send_message(message.chat.id, "Будь ласка, виберіть опцію з меню.")

bot.polling(none_stop=True)

