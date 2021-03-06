[![Build status](https://ci.appveyor.com/api/projects/status/i6saa94o0a6s6d9a?svg=true)](https://ci.appveyor.com/project/ADeoZ/ahj-diploma-frontend)

# Медиа Органайзер

## DEMO

[Ссылка на GitHub Pages](https://adeoz.github.io/Cats-Organizer/)  
Первичное ожидание от сервера Heroku может потребовать 5-30 секунд.

## Backend

[Репозиторий Backend](https://github.com/ADeoZ/Cats-Organizer-backend)  
  
Серверная часть (бэкенд) размещена через сервис Heroku, подразумевающий ограничения:
* сброс серверной части и базы данных спустя 30-60 минут
* время запуска после простоя и поступление первого ответа спустя 5-30 секунд после обращения
* закрытие канала WebSockets спустя 50-60 секунд бездействия

## Используемые технологии

* WebSockets
* Geolocation API
* MediaRecorder
* Webpack
* Appveyor (CI & Deployment)
* Node.js (Backend)

## Структура приложения
* Chaos.js – основной класс приложения. Отвечает за визуальный рендер.
* DOM.js – построение DOM-элементов.
* Request.js – логика общения с сервером через WebSockets
* SidePanel.js – боковая панель Органайзера - Хранилище и категории
* FileLoader.js – загрузка файлов, Drag & Drop
* MediaLoader.js – запись и обработка видео и аудио сообщений
* Geolocation.js – определение геолокации
* Favourites.js – работа с избранными сообщениями
* Pin.js – закрепление сообщения

## Описание
Сервис для хранения и сортировки текстовых данных, ссылок и медиафайлов

На данный момент обладает следующим функционалом:

1. Сохранение в истории текстовых сообщений
2. Сохранение в истории ссылок
3. Разметки ссылок в сообщениях
4. Сохранение в истории изображений
5. Сохранение в истории видео-файлов
6. Сохранение в истории аудио-файлов
7. Сохранении в истории любых файлов, не относящихся к вышеуказанным форматам, для последующего скачивания
8. Загрузка изображений и файлов с использованием Drag & Drop
9. «Ленивая» подгрузка. Постепенная подгрузка сообщений (по 10 сообщений) из истории по мере прокрутки ленты сообщений.
10. Синхронизация нескольких открытых Органайзеров между собой, в том числе между отдельными вкладками в рамках одного браузера, так и между отдельными браузерами и устройствами
11. Запись аудио-сообщений с помощью встроенного микрофона
12. Запись видео-сообщений с помощью встроенной веб-камеры
13. Воспроизведение аудио-сообщений
14. Воспроизведение видео-сообщений
15. Прикрепление к сообщению точки геолокации и просмотр отметки с помощью Яндекс.Карт
16. Закрепление сообщений. Сообщение закрепляется сверху ленты сообщений. Одновременно закреплено может быть только одно сообщение
17. Добавление сообщений в избранное и просмотр избранных сообщений
18. Автоматическая сортировка и просмотр сообщений по категориям «Избранное», «Ссылки», «Изображения», «Видео», «Аудио», «Файлы»
19. Удаление сообщений

## Инструкция по работе
* [Отправка сообщений](#messages)
* [Отправка ссылок](#links)
* [Отправка файлов](#files)
* [Запись аудио и видео](#media)
* [Добавление геолокации](#geo)
* [Дополнительное меню](#additional)
  * [Удаление сообщения](#delete)
  * [Закрепление сообщения](#pin)
  * [Добавление в избранное](#favourites)
* [Хранилище Органайзера](#storage)
  * [Просмотр сообщений из категории Хранилища](#view)
  * [Просмотр избранных сообщений](#favview)

### <a name="messages">Отправка сообщений</a>

Ввод текстовых сообщений производится с помощью поля, расположенного в нижней части листа сообщений. Отправка сообщения происходит по нажатию клавиши Enter. Отправление пустых сообщений запрещено.

![](https://github.com/ADeoZ/ahj-diploma-frontend/blob/master/readme_pic/1-sendtext.png)

Отправленное сообщение добавляется в базу данных Органайзера и появляется в ленте сообщений. При этом в сообщении отмечается дата и время отправки.

### <a name="links">Отправка ссылок</a>

Отправка ссылок в ленту сообщений происходит аналогично обычному текстовому сообщению. Ссылки распознаются, как ссылки при наличии указанного протокола http или https . В одном сообщении может быть указано сразу несколько ссылок.

![](https://github.com/ADeoZ/ahj-diploma-frontend/blob/master/readme_pic/2-links.png)

После отправки, распознанные ссылки также помещаются в раздел Хранилища — Ссылки отдельными элементами.

### <a name="files">Отправка файлов</a>

Для отправки файла необходимо выбрать соответствующую категорию в дополнительном меню формы отправки.

![](https://github.com/ADeoZ/ahj-diploma-frontend/blob/master/readme_pic/3-filemenu.png)

Отправка файла возможна, как через выбор файла на компьютере через нажатие кнопки в открывшейся форме, так и с помощью функции Drag & Drop, то есть перетаскиванием файла в область ленты сообщений Органайзера. Закрытие формы производится с помощью креста в левой части.

![](https://github.com/ADeoZ/ahj-diploma-frontend/blob/master/readme_pic/4-sendfile.png)

После выбора или перетаскивания файл будет автоматически отправлен в Органайзер, распознан и добавлен в ленту сообщений и в Хранилище.
При этом файлы изображений показываются в виде изображений, видео и аудио в виде проигрывателей, прочие файлы в виде ссылки на скачивание.

### <a name="media">Запись аудио и видео</a>

Для записи своих аудио и видео сообщений необходимо выбрать соответствующую категорию в дополнительном меню формы отправки. При этом необходимо предоставить соответствующие разрешения для браузера на использование микрофона и видеокамеры. Закрытие формы производится с помощью креста в левой части.

![](https://github.com/ADeoZ/ahj-diploma-frontend/blob/master/readme_pic/5-media.png)

Запись начинается при нажатии красного круга на открывшейся панели. После остановки записи сформированный файл автоматически отправляется в Органайзер, распознаётся и сортируется.

### <a name="geo">Добавление геолокации</a>

Для добавления метки геолокации к сообщению необходимо выбрать соответствующую категорию в дополнительном меню формы отправки. При этом необходимо предоставить соответствующие разрешения для браузера на распознование расположения.

![](https://github.com/ADeoZ/ahj-diploma-frontend/blob/master/readme_pic/6-geo.png)

Метка геолокации добавляется к сообщению для последующей отправки и отображается в левой верхней части формы отправки. Удаление метки производится нажатием креста возле координат.
При отправке файлов или записи своих аудио и видео сообщений геометку необходимо добавлять перед выбором файла или перед началом записи.

В ленте сообщения прикреплённая метка геолокации является ссылкой на Яндекс.Карты с отображением места по указанным координатам.

![](https://github.com/ADeoZ/ahj-diploma-frontend/blob/master/readme_pic/7-geolink.png)

### <a name="additional">Дополнительное меню</a>

При наведении курсора на сообщение в ленте сообщений Органайзера в правом верхнем его углу появляется интерактивная точка, по нажатию на которую открывается дополнительное меню для этого сообщения.

![](https://github.com/ADeoZ/ahj-diploma-frontend/blob/master/readme_pic/8-addmenu.png)

#### <a name="delete">Удаление сообщения</a>

Удаление сообщения производится путём нажатия на соответствующую кнопку в дополнительном меню сообщения.
Удаление производится из ленты и из категорий Хранилища. Если сообщение было закреплено, оно также снимается из закреплённого.

#### <a name="pin">Закрепление сообщения</a>

Закрепление сообщения производится путём нажатия на кнопку скрепки в дополнительном меню сообщения.
При этом копия сообщения помещается в верхнюю область ленты сообщений и остаётся там при прокрутке или обновлении страницы.

![](https://github.com/ADeoZ/ahj-diploma-frontend/blob/master/readme_pic/9-pinmessage.png)

Из области закреплённого сообщения доступно снятие закрепления через нажатие на кнопку крест в правой части закреплённого сообщения. А также отдельный просмотр выделенного сообщения через нажатие на кнопку стрелки.
Снятие сообщения из закреплённого производится также нажатием на появившуюся кнопку скрепки на сообщении, без захода в дополнительное меню.

#### <a name="favourites">Добавление в избранное</a>

Добавление сообщения в избранное производится путём нажатия на кнопку звезды в дополнительном меню сообщения.

![](https://github.com/ADeoZ/ahj-diploma-frontend/blob/master/readme_pic/10-favourites.png)

При этом сообщение заносится в категорию Хранилища — Избранное, откуда доступен просмотр всех избранных сообщений.
Удаление сообщения из избранного производится нажатием на появившуюся кнопку звезды на сообщении, без захода в дополнительное меню.

### <a name="storage">Хранилище Органайзера</a>

В Хранилище категоризируются и сохраняются отправленные сообщения.

![](https://github.com/ADeoZ/ahj-diploma-frontend/blob/master/readme_pic/11-storage.png)

Сообщения автоматически деляться по следующим категориям:
* Избранное
* Ссылки
* Изображения
* Видео
* Аудио
* Файлы

Каждая категория подразумевает возможность отдельного просмотра сообщений, определённых в ней.

#### <a name="view">Просмотр сообщений из категории Хранилища</a>

Для просмотра сообщений из категории Хранилища необходимо кликнуть на категории.
При этом в правой части Органайзера открывается список сообщений в данной категории. Просмотр отдельного сообщения в категории производится путём нажатия на стрелку слева от сообщения.

![](https://github.com/ADeoZ/ahj-diploma-frontend/blob/master/readme_pic/12-select.png)

Просмотр производится в левой части Органайзера, где открывается окно выбранного сообщения. Закрыть окно и вернуться к общей ленте сообщений можно через нажатие на кнопку креста в заголовке окна. Также окно автоматически закрывается при закрытии выбранной категории Хранилища.

#### <a name="favview">Просмотр избранных сообщений</a>

Просмотр избранных сообщений отличается от просмотра сообщений других категорий Хранилища. При выборе пункта Избранное в Хранилище все сообщения, отмеченные избранными, открываются единым списком вместо ленты сообщений в левой части Органайзера.

![](https://github.com/ADeoZ/ahj-diploma-frontend/blob/master/readme_pic/13-favouritesselect.png)

Закрытие ленты избранных сообщений производится аналогично закрытию категории Хранилища.
