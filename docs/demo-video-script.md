# 🎬 Dämdi (Food Advisor) — сценарий демо-видео (≈ 6 минут)

Каждый снимает свою часть **отдельно**, Мирас потом склеивает всё в одно видео.
Текст для озвучки — **на английском** (жирным шрифтом в рамках), пояснения что делать на экране — на русском.
Говорите спокойно, не быстро: ~130 слов в минуту. Тексты уже подогнаны под это время.

**Слайды:** новая презентация в стиле Dämdi (7 слайдов, оливковая), ссылка у Мираса. Перед записью откройте её в режиме **Present** на весь экран. В заметках докладчика под каждым слайдом есть тот же текст, что ниже, и имя того, кто говорит. Можно скачать как PDF или PowerPoint: Share → Export.

---

## 0. Перед записью (всем)

1. Скачать последнюю версию (новый дизайн Dämdi), запустить приложение и **сбросить базу** к исходным данным, чтобы у всех было одинаково:
   ```bash
   git pull
   ```
   ```bash
   npm run db:setup
   ```
   ```bash
   npm start
   ```
2. Браузер: Chrome, масштаб 100 %, окно на весь экран, спрятать закладки (`Ctrl+Shift+B`), закрыть лишние вкладки.
3. Запись: 1920×1080, микрофон поближе, тишина вокруг. Удобно — OBS или встроенная запись экрана (Win: `Win+Alt+R`, Mac: `Cmd+Shift+5`).
4. Перед записью **один раз прогоните свою часть без записи**, чтобы знать куда кликать.
5. Проверить, что сайт **оливковый** и в шапке написано **Dämdi**. Если видно старый оранжевый дизайн, обновить страницу с очисткой кэша: `Cmd+Shift+R` (Mac) или `Ctrl+Shift+R` (Windows).
6. Пароль у всех демо-аккаунтов: `Password123` (на странице Login есть кнопки быстрого входа).
7. В начале и в конце каждого куска — 2 секунды тишины, так проще клеить.

| # | Время | Кто | Что |
|---|---|---|---|
| 1 | 0:00–0:30 | Мадина | Слайды 1–2: команда, цель, три роли |
| 2 | 0:30–1:15 | Мирас | Слайды 3–4: архитектура и технологии |
| 3 | 1:15–2:30 | Замира | Сайт: гость и покупатель (customer) |
| 4 | 2:30–3:45 | Мирас | Сайт: владелец ресторана (owner) |
| 5 | 3:45–5:00 | Ильяс | Сайт: админ + MySQL + тесты |
| 6 | 5:00–6:00 | Мадина | Слайды 5–7: структура кода, таблица вклада, Thank you |

---

## 1. Мадина — слайды 1–2 (0:00–0:30)

**Слайд 1 (обложка)** — логотип Dämdi, картинка юрты-чайханы, «Find your next favourite table.», четыре имени с ID.

> **Hello! We are Group 4 from CE 202, and this is our final demonstration for F28JC Web Programming. Our Food Advisor web application is called Dämdi — it means “tasty” in Kazakh.
> Our team is Madina Bazarbayeva, Zamira Nurmanova, Ilyas Sungatov and Miras Yernazarov.**

**Слайд 2 (Aim & Scope)** — «Helping people decide where to eat», три карточки ролей. Когда называешь роль, веди мышкой по карточке.

> **Our aim is to help people decide where to eat. Dämdi is one website to discover restaurants and dishes in Aktobe, Almaty and Astana, compare them by cuisine, location, rating and price, and read honest reviews.
> The site has three roles. Customers discover and review restaurants.
> Owners manage their own place — their restaurants, menus and replies to guests.
> And administrators keep the site trustworthy — they approve restaurants, manage users and remove bad reviews.
> Now Miras will explain how the system works.**

---

## 2. Мирас — слайды 3–4, архитектура и технологии (0:30–1:15)

**Слайд 3 (Architecture)** — «Three layers, talking JSON». Веди мышкой слева направо: Client → Server (выделен оливковой рамкой) → Data, задерживаясь на горчичных стрелках «JSON over HTTP» и «SQL with ? params».

> **Our application has three layers that talk to each other with JSON.
> The client is the browser: HTML pages with CSS, and jQuery for events and AJAX calls.
> The server is Node.js with Express. It gives a REST API, checks the login token and the user's role, validates every input, hashes passwords with scrypt and limits login attempts.
> The data is stored in MySQL — ten tables with foreign keys, indexes for search, and CHECK and UNIQUE rules. Every SQL query uses question-mark parameters, so SQL injection does not work.**

**Слайд 4 (Tools, тёмный)** — «Course technologies, used together» (6 карточек). Говоришь быстро, ~15 секунд.

> **We used only the course technologies, all together: HTML and CSS for the layout and the light and dark theme, jQuery for interactivity, JSON between browser and server, Node.js for the server, MySQL for the data, and Web Storage for favourites, history and settings.
> Now Zamira will show the site as a customer.**

---

## 3. Замира — гость и покупатель (1:15–2:30)

Начинаешь **не залогиненной**, на главной странице.

| На экране | Что говоришь |
|---|---|
| Главная страница Dämdi (картинка с юртой) | **This is the home page of Dämdi.** |
| Блок **«What should I eat today?»**: выбрать город, бюджет, настроение → крутить рулетку | **If you don't know what to eat, you can spin our roulette. I choose the city and budget — and it picks a dish for me.** |
| В поиске набрать `plov` — появятся подсказки | **The search gives live suggestions for restaurants, cuisines and dishes.** |
| **Explore restaurants** → фильтры: город, кухня, рейтинг, цена, **Open now** | **On the Explore page I can filter by city, cuisine, rating and price, or show only places that are open now. The filters are saved in the link, so I can share the results.** |
| Открыть ресторан → меню → нажать на блюдо → **See nutrition & details** | **This is the restaurant page with the menu. For every dish we show calories, protein, fat, carbs and allergens.** |
| Login → кнопка демо **Customer** | **Now I log in as a customer.** |
| В ресторане, где есть кнопка **Write a review** → оценка + текст → опубликовать (будет конфетти) → **Edit** → поменять оценку | **I write a review with a rating… publish it… and I can edit or delete my own review at any time. The average rating updates straight away.** |
| Нажать **Helpful** на чужом отзыве, сердечко ❤ на ресторане | **I can mark other reviews as helpful and save restaurants to my favourites.** |
| **Profile** → My reviews, Favourites, Browsing history | **In my profile I see my reviews, favourites, recently viewed restaurants and recent searches. The history is kept in the browser with localStorage.** |
| (если успеваешь) нажать на луну 🌙 в шапке → тёмная тема | **Dämdi also has a dark theme, and the browser remembers my choice in localStorage.** |
| (если успеваешь) нажать на «Compare» у 2–3 ресторанов → страница сравнения | **I can also compare up to three restaurants side by side.** |

Последняя фраза:
> **Next, Miras will show the owner side.**

⚠️ Отзыв можно оставить только **один раз** на ресторан — выбирай ресторан, где ещё есть кнопка «Write a review».

---

## 4. Мирас — владелец ресторана (2:30–3:45)

Login → демо-кнопка **Owner** (Aidos Seitkali). У него рестораны: Dastarkhan House, Samarkand Plov Centre, Steppe Steakhouse и Baursak & Co (**Pending**).

| На экране | Что говоришь |
|---|---|
| **Dashboard** — графики по месяцам, разбивка оценок, последние отзывы | **Now I'm logged in as a restaurant owner. The dashboard shows the average rating, reviews per month and the rating breakdown. These numbers come from SQL queries with AVG, COUNT and GROUP BY.** |
| **My restaurants** → показать Baursak & Co со статусом **Pending** | **Here are my restaurants. A new restaurant starts as pending — it is not public until an admin approves it.** |
| Открыть **Edit** у Dastarkhan House → поменять, например, часы работы или описание → Save | **I can edit my own restaurant…** |
| **Menu** → **Add dish** (название, категория, цена, калории) → Save. Потом у другого блюда отметить **Sold out** | **…add a new dish with price and nutrition facts, and mark a dish as sold out. The same validation runs in the browser and on the server, so for example a negative price is rejected.** |
| (по желанию) ввести цену `-100` → показать ошибку | — |
| **Guest reviews** → нажать **Reply** → написать ответ → Save | **I can also reply to guest reviews, and the reply is shown publicly under the review.** |
| — | **An owner can only change their own restaurants. If another owner tries, the server returns 403 Forbidden — we check this in our tests. Now Ilyas will show the admin panel.** |

---

## 5. Ильяс — админ, база и тесты (3:45–5:00)

Login → демо-кнопка **Admin**.

| На экране | Что говоришь |
|---|---|
| **Admin overview** — графики | **This is the admin panel. The overview shows new reviews per month, users by role and the best rated restaurants.** |
| **Restaurants** → найти **Baursak & Co (pending)** → **Approve** | **New restaurants wait here for approval. I approve Baursak & Co, and now it is visible to everyone.** |
| **Reports** → отзыв от *Best Deals KZ* (spam) → **Hide review** | **Users can report bad reviews. This one is spam, so I hide it — and the restaurant's average rating is recalculated.** |
| **Users** → найти *Best Deals KZ* → **Block** | **Then I block the spammer. A blocked user is logged out immediately and cannot log in again.** |
| (коротко) **Cuisines**, **Site feedback** | **I can also manage cuisines and read feedback from testers.** |
| MySQL Workbench (или терминал `mysql`) → показать список таблиц и `SELECT * FROM restaurants LIMIT 5;` | **Here is our MySQL database: ten tables — users, sessions, cuisines, restaurants, dishes, reviews, votes, reports, favourites and feedback — connected with foreign keys.** |
| Терминал: `npm test` (сервер должен быть запущен) → показать что все **42 passing** | **Finally, our 42 automated tests check every functional requirement and the security rules — for example, that customers cannot open owner pages and that SQL injection does not work. All tests pass. Back to Madina.** |

---

## 6. Мадина — слайды 5–7 (5:00–6:00)

**Слайд 5 (Code structure)** — «Organised by responsibility» (таблица папок). Веди мышкой по строкам сверху вниз.

> **To sum up, here is how our code is organised — by responsibility.
> server.js and config.js start the Express app, add the security headers and handle errors.
> The routes folder has the REST API, split by area: auth, restaurants, dishes, reviews, owner and admin.
> The middleware checks the login and the user's role, and limits login attempts. The utils folder has validation, password hashing and shared SQL.
> The database folder has the schema, the sample data and a full MySQL dump. The public folder has the HTML pages, the jQuery scripts, the stylesheet and our illustrations. And the tests folder has 42 automated tests for every functional requirement.**

**Слайд 6 (Team)** — «Who did what». Текст совпадает со слайдом, чтобы не было расхождений. ⚠️ Перед записью проверьте, что таблица правдивая: учитель может проверить вклад каждого.

> **This table shows how we shared the work.
> I was the reporter — I did the planning, the documentation, the slides, the video and the Canvas submission.
> Zamira led the front end — the pages, the jQuery interactivity and the responsive layout.
> Miras led the back end — the routes, login, role checks, validation and security.
> And Ilyas led the database and testing — the MySQL schema, the sample data and the automated tests.**

**Слайд 7** — «Thank you.» (справа картинка «чай у окна»).

> **Thank you for watching!**

Для **видео** строку «Questions welcome» на слайде лучше убрать: вопросов к видео не будет. На **живой защите 2 декабря** её оставьте и после этого слайда начинайте Q&A.

---

## 7. Монтаж (Мирас)

- Порядок клипов: 1 → 2 → 3 → 4 → 5 → 6. Итог должен быть **не длиннее 6:00**.
- Если кусок длиннее своего времени — ускорить «скучные» места (ввод текста, загрузку) до 1.5×, а не сам голос.
- Между клипами — простой переход (cut или 0.3 с fade), на кадрах сайта можно добавить подпись «Customer / Owner / Admin».
- Громкость у всех выровнять (normalize audio).
- Экспорт: MP4, 1080p.
