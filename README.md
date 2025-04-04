# Веб-ларёк
### Автор: Жагло Игорь Дмитриевич

Онлайн-платформа для веб-разработчиков с возможностью просмотра товаров, формирования корзины и оформления заказов.
## Общая концепция
В основе проекта лежит архитектурный подход MVP (Model-View-Presenter), обеспечивающий строгое разделение логики:

**Model** – отвечает за взаимодействие с API, хранение и обработку информации (как серверной, так и пользовательской).

**View** – визуализирует интерфейс, фиксирует действия пользователя и передаёт их в систему.

**EventEmitter** (в роли Presenter) – выступает связующим звеном: координирует обмен данными между Model и View при возникновении событий.

### Используемые технологии:
- HTML, SCSS, TypeScript, Webpack

### Организация проекта:
- `src/` – исходный код приложения
- `src/components/` – компоненты интерфейса
    - `src/components/base/` – базовые элементы системы
- `src/pages/index.html` – стартовая страница
- `src/types/index.ts` – типы данных
- `src/index.ts` – инициализация приложения
- `src/styles/styles.scss` – глобальные стили
- `src/utils/constants.ts` – постоянные значения
- `src/utils/utils.ts` – вспомогательные функции

## Базовые компоненты системы

### Класс `Api`
Обеспечивает коммуникацию с сервером.

**Ключевые методы:**
- `handleResponse(response: Response): Promise<object>` – парсинг ответа сервера.
- `get(uri: string)` – запрос данных по указанному эндпоинту.
- `post(uri: string, data: object, method: ApiPostMethods = 'POST')` – отправка данных (поддерживает POST, PUT, DELETE).

### Класс `EventEmitter`
Реализует паттерн Наблюдатель для управления событиями.

**Функционал:**
- `on` – регистрация обработчика события.
- `off` – удаление подписки.
- `emit` – оповещение подписчиков.
- `onAll` – глобальная подписка на все события.
- `offAll` – полный сброс подписок.
- `trigger` – генерация события с параметрами (используется для интеграции с внешними классами).

## Модели данных

### `ApiModel` (наследник `Api`)
Обрабатывает серверные данные:
- `getListProductCard` – загружает список товаров.
- `postOrderLot` – отправляет заказ на сервер.

### `BasketModel`
Управляет корзиной пользователя:
- `getCounter` – возвращает количество позиций.
- `getSumAllProducts` – вычисляет итоговую стоимость.
- `setSelectedСard` – добавление товара.
- `deleteCardToBasket` – удаление товара.
- `clearBasketProducts` – полная очистка корзины.

### `DataModel`
Хранит информацию о товарах:
- `setPreview` – сохраняет данные просматриваемой карточки.

### `FormModel`
Работает с пользовательскими данными:
- `setOrderAddress` – сохраняет адрес доставки.
- `validateOrder` – проверяет корректность адреса и оплаты.
- `setOrderData` – записывает контактные данные.
- `validateContacts` – валидирует email и телефон.
- `getOrderLot` – формирует объект заказа.

## Компоненты интерфейса

### `Basket`
Отображает состояние корзины:
- `renderHeaderBasketCounter` – обновляет счетчик в шапке.
- `renderSumAllProducts` – показывает общую сумму.

### `BasketItem`
Элемент корзины:
- `setPrice` – форматирует цену для отображения.

### `Card`
Карточка товара:
- `setText` – изменяет текст элемента.
- `cardCategory` – задаёт категорию через CSS-класс.
- `setPrice` – отображает цену.

### `CardPreview` (наследник `Card`)
Детальное описание товара:
- `notSale` – блокирует покупку, если цена отсутствует.

### `Order`
Оформление заказа:
- `paymentSelection` – визуально выделяет выбранный способ оплаты.

### `Contacts`
Ввод контактных данных.

### `Modal`
Управление модальными окнами:
- `open` – открытие окна.
- `close` – закрытие окна.

### `Success`
Отображение подтверждения успешного заказа.

## Инструкция по запуску

Установка зависимостей:
```bash
npm install  # или yarn
```

Запуск в режиме разработки:
```bash
npm run start  # или yarn start
```

Сборка проекта:
```bash
npm run build  # или yarn build
```