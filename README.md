# DiscordCardBot
Простенький бот, позволяющий коллекционировать карты участниками сервера.
## Описание
Участник дискорд сервера может при использовании команд этого бота:
 - **daikarty** : получить коллекционную карту 1 раз в 24 часа или просмотреть через сколько времени он ее сможет получить
 - **pokajimne** :просмотреть список и количество карт одного типа, которые он уже получил
 - **profile** : просмотреть статистику пользователя сервера по выпавшим картам 
 - **помощь** : получить справку о командах бота
## Новости
 **фича от 26.09.2021**
  - Добавлена команда **profile** [@UserMention]. Выводит профиль пользователя, содержащий информацию:
      - сколько карт всего выпало;
      - какое количество карт выпало определенного класса;
      - количество карт, которых пользователь еще не открыл;
      - карта, котороая больше всего раз выпала.
  - Добавлены поля для карт: **class**(класс карты), предназначенные для определения ценности/редкости карты.
![](https://media.discordapp.net/attachments/852679774128439386/891750797023531018/profile.png)

 **небольшое обновление от 04.08.2021**
 - При просмотре инвентаря теперь показывается не только текущая страница, но и сколько всего страниц доступно.
 - При истечении срока работы инвентаря все реакции, прикрепленные к сообщению удаляются.

 **фича от 31.07.2021**
 - Чтобы не превышать максимальное количество символов в сообщении для API Discord`а был введен "страничный" инвентарь:
после ввода команды о запросе показать инвентарь, бот показывает вам последнюю страницу инвентаря, в которой содержатся ваши недавно полученные коллекционные карты. Вы можете перелистывать страницы инвентаря при помощи реакций(⬅️ и ➡️) в сообщении с вашими картами. Учтите, бот не будет бесконечно ждать, когда вы соизволете пролистнуть страницу, через некоторое время он перестанет реагировать на новые реакции, и вам придется запросить инвентарь командой снова.
![](https://cdn.discordapp.com/attachments/852679774128439386/871084401600110632/3LfGjl6Rj4.gif)

 **фича от 11.06.2021**
- При получении одной и той же карты каждый 3й раз, участнику сервера дается возможность сразу же попытаться выбить еще одну карту.
- Теперь, когда человек будет использовать команду для получения карты, но 24 часа с момента прошлого получения еще не прошли, бот покажет через сколько времни выдача карты будет доступна.

## Настройка проекта
Требуется:
 - Node.js 10.0.0 или выше;

### Создание конфига
В корне проекта создайте конфигурационный файл **.env**
Пример файла .env :
```
TOKEN = "токен вашего бота"
PREFIX = '!' 
PAGE_SIZE = 7
INVENTORY_TIME = 60000
RARE_CLASS_NUMBER = 5
CLASS_SYMBOL_FILL = ":star:"
CLASS_SYMBOL_OF_VOID = ":small_orange_diamond:"
```

PAGE_SIZE - количество элементов, которые будут умещаться на одной странице инвентаря при показе
INVENTORY_TIME - время бездействия инвентаря, после которого бот перестает листать страницы, указывается в миллисекундах

RARE_CLASS_NUMBER - количество классов редкости/ценности
CLASS_SYMBOL_FILL - Discord emoji для заполнения шкалы редкости/ценности
CLASS_SYMBOL_OF_VOID - Discord emoji для заполнения пустоты шкалы редкости/ценности

Иллюстрация ниже чтобы понять суть 3х последних параметров:
![](https://media.discordapp.net/attachments/852679774128439386/891748889118511134/env_decr.png)


### Подготовка контента
Откройте файл /storage/db.json
```
{
	"users": [], // Ссодержит данные участников сервера и их инвентарь 
	"cards": [] // Содержит данные о картах, которые могут выпасть на сервере
}
```

Данные о пользователях сервера **будут автоматически добавляться** по мере использования команд бота.
Данные о картах вам **придется заполнить самостоятельно**. 
Пример добавления карты в **db.json**
```
cards: [
    {
        "name": "test_card", // Название карты
        "class": 1, // ценность карты, определяется от 1 до RARE_CLASS_NUMBER включительно
        "active": true, // Флаг, определяющий, может ли катра вывпасть участникам сервера
        "url": "url_string.png"  // Ссылка на изображение карты
    }, 
]
```

### Подгрузка зависимостей
Откройте терминал в корне проекта, далее пропишите следующие команды:
```
npm i 
```

### Запуск проекта
```
npm start 
```