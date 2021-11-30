# DiscordCardBot
Простенький бот, позволяющий коллекционировать карты участниками сервера.
## Описание
Участник дискорд сервера может при использовании команд этого бота:
 - **daikarty** : получить коллекционную карту 1 раз в 24 часа или просмотреть через сколько времени он ее сможет получить
 - **pokajimne** :просмотреть список и количество карт одного типа, которые он уже получил
 - **profile** : просмотреть статистику пользователя сервера по выпавшим картам 
 - **помощь** : получить справку о командах бота
 - **undiscovered** : узнать количество карт, которых не выпало ни одному из участников сервера на данный момент

 [Настройка проекта](#Настройка-проекта)
## Новости
 **обновление от 30.11.2021**
 - В названии карт встроены ссылки, что позволяет использовать url любой длинны без порчи вида сообщения.
 - Исправлен баг, при котором не отображалась ценность(**class**) карт символами/эмодзи в **pokajimne**.
 - Убрано отображение url в profile (теперь ссылка в названии карты).
 - Изменен внешний вид для **daikarty**.

![](https://media.discordapp.net/attachments/852679774128439386/915276541347381268/drop.png)

 - Изменен внешний вид для **pokajimne**.

![](https://media.discordapp.net/attachments/852679774128439386/915276541573881896/pokajimne.png)

 - Добавлена возможность просматривать чужой инвентарь(**pokajimne @UserMention**), при условии если данная функция разрешена(параметром в конфиге **INVENTORY_PUBLIC_ACCESS = 1**).

![](https://media.discordapp.net/attachments/852679774128439386/915276541942988840/pokajimne_someone_public.png)
![](https://media.discordapp.net/attachments/852679774128439386/915276542152699954/pokajimne_someone_private.png)


 **небольшое обновление от 21.11.2021**
  - Добавлены тестовые карты в **db.json** для примера их добавления. 

  ![](https://cdn.discordapp.com/attachments/852679774128439386/911969469914574939/unknown.png)

  - Добавлено отображение количества карт каждого класса при просмотре профиля(**profile**).

  ![](https://cdn.discordapp.com/attachments/852679774128439386/911967665906651166/unknown.png)

 **фича от 06.10.2021**
  - Добавлена команда **undiscovered**. Выводит количество карт, которых на сервере еще никому не удавалось получить.

![](https://cdn.discordapp.com/attachments/852679774128439386/895117207615471666/unknown.png)

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
1. **Склонируйте проект.**

2. **Убедитесь, что у вас установлено:**
 - ![Node.js](https://nodejs.org/en/) 10.0.0 или выше.

3. **Создайте конфигигурационный файл и занесите в него необходимую информацию.**

### Создание конфига
В корне проекта создайте конфигурационный файл **.env**
Пример файла .env :
```
TOKEN = "токен вашего бота"
PREFIX = '!' 
PAGE_SIZE = 7
INVENTORY_TIME = 60000
INVENTORY_PUBLIC_ACCESS = 1
RARE_CLASS_NUMBER = 5
CLASS_SYMBOL_FILL = ":star:"
CLASS_SYMBOL_OF_VOID = ":small_orange_diamond:"
```

**PAGE_SIZE** - количество элементов, которые будут умещаться на одной странице инвентаря при показе
**INVENTORY_TIME** - время бездействия инвентаря, после которого бот перестает листать страницы, указывается в миллисекундах
**INVENTORY_PUBLIC_ACCESS** - доступ вызова инвентаря другого пользователя **1 - можете использовать pokajimne @UserMention, 0 - другие пользователи могут только сами демонстрировать свой инвентарь в чате**

**RARE_CLASS_NUMBER** - количество классов редкости/ценности

**CLASS_SYMBOL_FILL** - Discord emoji для заполнения шкалы редкости/ценности

**CLASS_SYMBOL_OF_VOID** - Discord emoji для заполнения пустоты шкалы редкости/ценности


Иллюстрация ниже чтобы понять суть 3х последних параметров:
<br />
![](https://media.discordapp.net/attachments/852679774128439386/891748889118511134/env_decr.png)

4. **Добавьте необходимый контент для вашего сервера.**

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

Если вы только склонировали проект, то вы можете обнаружить что в **db.json** уже есть информация о тестовых картах с редкостью от 1 до 6 где карты с **class от 1 до 5 - стандартные** и та, что с **class 6 - нестандартная**(Что значит ее ценность не будет отображаться при помощи **CLASS_SYMBOL_FILL** и **CLASS_SYMBOL_OF_VOID**, учтите это, если же вы хотите как то отметить ее ценность символами/эмодзи, можете прописать их в поле названия карты, как в **db.json** репозитория).  

5. **Скачайте необходимые модули для работы проекта.**

### Подгрузка зависимостей
Откройте терминал в корне проекта, далее пропишите следующие команды:
```
npm i 
```
6. **После всех успешно проделанных шагов, вы можете запустить бота, прописав команду в терминале.**
### Запуск проекта
```
npm start 
```