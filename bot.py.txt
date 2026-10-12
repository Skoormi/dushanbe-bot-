import os
import telebot
from telebot import types

# Токен берем с настроек хостинга, чтобы не светить
TOKEN = os.getenv("BOT_TOKEN")

bot = telebot.TeleBot(TOKEN)

menu = types.ReplyKeyboardMarkup(resize_keyboard=True)
menu.add("💰 Цены", "📍 Адрес")
menu.add("📦 Заказать")

@bot.message_handler(commands=['start'])
def start(m):
    bot.send_message(m.chat.id, "Салом! Я магазин Душанбе бот. Что показать?", reply_markup=menu)

@bot.message_handler(func=lambda m: "Цены" in m.text)
def price(m):
    bot.send_message(m.chat.id, "Все товары от 250 сомони. Доставка 15 сомони.")

@bot.message_handler(func=lambda m: "Адрес" in m.text)
def addr(m):
    bot.send_message(m.chat.id, "Душанбе, Рудаки 100")

@bot.message_handler(func=lambda m: "Заказать" in m.text)
def order(m):
    bot.send_message(m.chat.id, "Напиши что хочешь заказать и свой номер!")

print("Бот запущен на сервере!")
bot.infinity_polling()
