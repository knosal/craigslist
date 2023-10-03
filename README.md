# craigslist

Одностраничное приложение на JavaScript, которое будет работать в браузере — список объявлений о продаже товаров и модальное окно с подробной информацией о каждом товаре.

## Состояние по умолчанию

- По умолчанию объявления отображаются по популярности.
- Отображается 7 объявлений.
- В блоке с фильтрами выбрана категория «Все».

## Избранные

- Объявление попадает в список избранных, если пользователь кликнул на иконку с сердечком в этом объявлении (сердечко заполнено — лайк поставлен).
- Объявление удаляется из списка избранных при повторном клике на сердечко (сердечко пустое — лайка нет).
- При загрузке списка объявлений, надо привести избранные объявления в актуальное состояние. Если товар в избранном у пользователя, надо сделать иконку избранности в этом объявлении активной.
- Избранные хранятся в браузере пользователя и не синхронизируются с сервером. Способ хранения может быть на усмотрение разработчика: cookie, localStorage, что-нибудь ещё.
- Иконка избранного в модальном окне объявления должна синхронизироваться с иконкой в карточке.
- Если пользователь кликнул на сердечко в карточке объявления, при открытии модального окна сердечко тоже должно быть выбранным.
- И наоборот: если пользователь добавил объявление в избранные в режиме модального окна, то при открытии списка объявлений, у карточки тоже должно стоять выбранное сердечко.
- Переход в меню избранных объявлений происходит по клику на кнопку «Показать избранные». При повторном клике происходит выход из этого меню.
- Избранные товары не фильтруются и не сортируются. При показе избранных, блокируются фильтры и кнопки сортировок.
- Если было что-то выбрано в фильтрах — эти состояния блокируются. То есть нельзя что-то в них поменять, все контролы недоступны. Но выбранные состояния не сбрасываются.
- Когда пользователь выходит из меню избранных объявлений, сортировка и фильтры разблокируются в тех же состояниях, что были до захода в избранные, и снова становятся доступны.

## Сортировка

- Популярные. Порядок по умолчанию. Данные в том порядке, в котором они пришли с сервера.
- Сначала дешёвые. Объявления, отсортированные по возрастанию цены от меньшей к большей. При этом стоит учитывать диапазон цен, указанный в блоке с фильтрами — валидно для всех категорий товаров кроме «Все».
- Новые. Сортировка по дате публикации объявления. От недавних к поздним.

## Категории товаров

- Каждой категории подходят дополнительные контролы для фильтрации, уникальные для каждой категории. Они появляются после выбора категории.
- При отображении эти фильтры располагаются между выбором цены и кнопкой «Показать».
- Если была выбрана какая-то категория, а потом пользователь выбрал категорию «Все», дополнительные фильтры должны исчезнуть со страницы.

## Выбор цены

- Максимальная цена в диапазоне берётся из данных. Если выбрана категория «Все», берётся самая высокая цена среди всех товаров и отображается в рендже, в поле справа над ползунком.
- Аналогично для минимальной цены в диапазоне. Она берётся по самому дешёвому товару среди всех товаров. Отображается в поле слева над ползунком.
- Если юзер выбрал новую категорию, минимальная и максимальная цена пересчитываются для этой категории и в рендже отображаются новые значения.

## Фильтрация

- Отфильтрованные товары отображаются после клика по кнопке «Показать».
- У товара в объявлении может не быть данных для сортировки. Например, может быть такое, что сервер отдаёт объявление без цены или в поле с ценой указано '0'. Такие товары должны попадать во все списки при фильтрации, но указываться в самом конце. После всех товаров, которые попали в фильтрацию.

## Если не нашлось подходящих вариантов

- Если нет избранных товаров, в блоке, где должы были отображаться объявления, выводится текст «У вас пока нет избранных товаров. Чтобы отметить товар, кликните на сердечко в карточке объявления. Вы можете вернуться к списку всех товаров, кликнув ещё раз на „Показать избранные“».
- Если нет товаров, которые подходят под условия фильтрации, выводится текст «Мы не нашли товары по вашему запросу. Попробуйте поменять фильтры настройки объявлений в блоке слева».

## Карточка объявления

- Название товара является ссылкой, при клике на название открывается полное объявление этого товара в модальном окне.
- Цена со знаком рубля, миллионы и тысячи отделяются тонким пробелом (1 546, 5 000 000, 380 000).
- Клик по фотографии товара открывает попап с полным объявлением. По сути работает ссылкой так же, как и название товара в карточке.
- В карточке можно перелистывать фотографии товара. На блочке с фотографиями есть пагинация и индикатор, который показывает, на какой сейчас фотографии пользователь.
- Перелистывание работает при наведении. Вместе со сменой фотографии, подсвечивается таб из пагинации, подходящий этой фотографии (каждый таб соответствует номеру фотографии).
- Может быть, что фотографий товара больше, чем 5. Тогда последней фотографии в блочке добавляется тёмный полупрозрачный слой и текст «+ n фото». Вместо n подставляется число оставшихся фотографий товаров, которые не поместились в блочок.
- Если фотографий 5 или меньше, то у последней фотографии нет тёмного слоя и надписи.
- Адрес: город и улица (если указана в данных) без номера дома.
- Время размещения объявления. Меняется в зависимости от условий.
- Объявление было размещено в течение последних 24 часов: текст «n часов назад».
- Объявление было размещено в течение последних 7 дней: «n дней назад».
- Объявление было размещено в этом году: «n месяца» (5 июня, 20 марта).
- Объявление было размещено в прошлых годах, указываем год: «n месяца n года» (5 апреля 2005 года, 23 июня 2007 года).
- Часы, дни и названия месяцев должны склоняться.

## Полное объявление

- Полное объявление отображается в модальном окне над списком товаров. Пока открыто полное объявление, весь контент под объявлением неактивный.
- Название товара здесь уже не ссылка, а текст.
- Цена. Цена со знаком рубля, миллионы и тысячи отделяются тонким пробелом (1 546, 5 000 000, 380 000, 25 000).
- Для времени размещения объявления правила те же, что и для карточки.
- Адрес должен быть подробней, чем в карточке: город, улица, номер дома или название строения, если они указаны в данных. Пишутся через запятую. Например, Москва, Нахимовский проезд, дом 5.
- Рядом с адресом отображается интерактивная карта, по центру которой находится маркер, указывающий на адрес. Движок карты можно выбрать любой, на усмотрение разработчика.
- Галерея с фотографиями товара. При клике на миниатюру, меняется контент большой карточки на соответствующую фотографию.
- Описание товара берётся из данных и добавляется на страницу.
- Информация о продавце: имя продавца или название компании, рейтинг.
- Иконка с рейтингом продавца. У хорошего рейтинг от 4.8, у среднего от 4 до 4.8 (не включая это значение), ниже 4 — плохой продавец. Для продавцов каждого уровня с помощью стилей меняется отображение. Данные о рейтинге берутся с сервера и подставляются в разметку иконки.
- Если о какой-то характеристике товара нет информации в данных, эта характеристика не отображается в карточке.

## Данные

- Данные находятся по адресу https://mock.pages.academy/store/db.
