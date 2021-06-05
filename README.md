# time-manager-rtk

Приложение для самостоятельного контроля рабочего времени. Контроль осуществляется путём заполнения ежедневника, на основе которого потом будут расчитываться другие показатели.

## Функционал приложения

1. [Список записей, отражающих, что было сделано в определенное время](###ежедневник)
    1. Просмотр записей
    2. Фильтрация по всем полям
    3. Сортировка по всем полям
    4. Экспорт записей в формате `JSON`
    5. Импорт записей в формате `JSON`
2. [Запись, отражающая, что было сделано в определенное время](###запись-ежедневника)
    1. Создание
    2. Удаление
    3. Редактирование
3. [Пользовательская сущность, которая не рассматривается, как таск но на которую может тратиться время](###пользовательская-сущность)
    1. Создание
    2. Удаление (только если нет записей с ней)
    3. Редактирование
4. [Данные в разрезе тасков](###краткая-сводка-по-таскам)
    1. Просмотр запсей
    2. Фильтрация по всем полям
    3. Сортировка по всем полям
    4. Переход к детализации по конкретному таску
5. [Данные в разрезе пользовательских сущностей](###краткая-сводка-по-пользовательским-сущностям)
    1. Просмотр записей
    2. Фильтрация по всем полям
    3. Сортировка по всем полям
    4. Переход к детализации по конкретной сущности
6. [Данные в разрезе затраченого времени](###краткая-сводка-по-времени)
    1. Просмотр записей
    2. Фильтрация по всем полям
    3. Сортировка по всем полям
    4. Переход к детализации по конкретному дню
    5. Экспорт записей в формате `JSON` за определенное время

## Детальное описание сущностей

### Ежедневник

Главный элемент приложения. Таблица, описывающая, что, в какой день и в какое время делал пользователь.

На основании данных ежедневника вычисляются

* [Краткая сводка по таскам](###краткая-сводка-по-таскам)
* [Краткая сводка по пользовательским сущностям](###краткая-сводка-по-пользовательским-сущностям)
* [Краткая сводка по времени](###краткая-сводка-по-времени)

Пояснения по функционалу

1. Экспорт записей в формате `JSON` - экспортируются стразу все данные. В основном надо для бэкапов
2. Импорт записей в формате `JSON` - при импорте данных все существующие данные будут заменены импортируемыми, поэтому если они нужны будут в дальнейшем, то надо будет сделать предварительный экспорт
3. Сортировка и фильтрация - параметры находятся в строке url, для упрощения создания ссылок на следующих страницах
    1. [Краткая сводка по таскам](###краткая-сводка-по-таскам)
    2. [Краткая сводка по пользовательским сущностям](###краткая-сводка-по-пользовательским-сущностям)
    3. [Краткая сводка по времени](###краткая-сводка-по-времени)

### Запись ежедневника

Элемент таблицы ежедневника, отражающий, какую работу произвёл пользователь приложения в определенное время и сколько времени на это потратил

#### Запись ежедневника содежит в себе следующую информацию

1. Номер таска или [пользовательская сущность](###пользовательская-сущность)
2. Дата и время начала действия
3. Дата и время конца действия
4. Сколько времени было потрачено на действие
5. Описание действия

#### Пояснения по функционалу

1. Создание - при создании записи, если дата и время пересекаются с другими записями, то пользователю должно быть предложено скорректировать время создаваемой записи или время уже существующих записей в удобном формате
2. Редактирование - при редактировании тоже надо подумать о том же, о чем и при создании

### Пользовательская сущность

Нужна для ведения действий, которые не включены в таск-трекер.

Состоит только из имени.

#### Пояснения по функционалу

1. Создание - доступно в следующие моменты
    1. При создании [записи ежедневника](###запись-ежедневника), если сущность с таким названием не была найдена
    2. Через отдельный интерфейс для манипуляций с пользовательскими сущностями
2. Удаление - доступно только если нет [записей ежедневника](###запись-ежедневника), привазанных к сущности
3. Редактирование - доступно через специальный интерфейс

### Краткая сводка по таскам

Содержит информацию об общем времени, которое было потрачено на каждый таск и можно посмотреть сколько времени было потрачено в определенный день. Также можно перейти по ссылке к ежеденевнику, где будут параметры фильтрации по этому таску.

#### Поля элемента сводки по таскам

1. Номер таска
2. Общее затраченое время
3. Время, затреченное в конкретный день

#### Пояснения по функционалу

1. Переход к детализации по конкретному таску - осуществляется через ссылку, которая прикреплена к одной из записей сводки

### Краткая сводка по пользовательским сущностям

Аналогично [краткой сводке по таскам](###краткая-сводка-по-таскам), но так же предосталяет интерфейс для добавления, редактирования, удаления.

### Краткая сводка по времени

Аналогично [краткой сводке по таскам](###краткая-сводка-по-таскам), но данные в разрезе дней

### Поля элемента сводки по времени

1. Дата
2. Кол-во рабочего времени

## Create-react-app

This project was bootstrapped with [Create React App](https://github.com/facebook/create-react-app), using the [Redux](https://redux.js.org/) and [Redux Toolkit](https://redux-toolkit.js.org/) template.

### Available Scripts

In the project directory, you can run:

#### `yarn start`

Runs the app in the development mode.<br />
Open [http://localhost:3000](http://localhost:3000) to view it in the browser.

The page will reload if you make edits.<br />
You will also see any lint errors in the console.

#### `yarn test`

Launches the test runner in the interactive watch mode.<br />
See the section about [running tests](https://facebook.github.io/create-react-app/docs/running-tests) for more information.

#### `yarn build`

Builds the app for production to the `build` folder.<br />
It correctly bundles React in production mode and optimizes the build for the best performance.

The build is minified and the filenames include the hashes.<br />
Your app is ready to be deployed!

See the section about [deployment](https://facebook.github.io/create-react-app/docs/deployment) for more information.

#### `yarn eject`

**Note: this is a one-way operation. Once you `eject`, you can’t go back!**

If you aren’t satisfied with the build tool and configuration choices, you can `eject` at any time. This command will remove the single build dependency from your project.

Instead, it will copy all the configuration files and the transitive dependencies (Webpack, Babel, ESLint, etc) right into your project so you have full control over them. All of the commands except `eject` will still work, but they will point to the copied scripts so you can tweak them. At this point you’re on your own.

You don’t have to ever use `eject`. The curated feature set is suitable for small and middle deployments, and you shouldn’t feel obligated to use this feature. However we understand that this tool wouldn’t be useful if you couldn’t customize it when you are ready for it.

### Learn More

You can learn more in the [Create React App documentation](https://facebook.github.io/create-react-app/docs/getting-started).

To learn React, check out the [React documentation](https://reactjs.org/).
