# 🎬 Food Advisor — сценарий демо-видео (≈ 6 минут)

Каждый снимает свою часть **отдельно**, Мирас потом склеивает всё в одно видео.
Текст для озвучки — **на английском** (жирным шрифтом в рамках), пояснения что делать на экране — на русском.
Говорите спокойно, не быстро: ~130 слов в минуту. Тексты уже подогнаны под это время.

---

## 0. Перед записью (всем)

1. Запустить приложение и **сбросить базу** к исходным данным, чтобы у всех было одинаково:
   ```bash
   npm run db:setup
   ```
   ```bash
   npm start
   ```
2. Браузер: Chrome, масштаб 100 %, окно на весь экран, спрятать закладки (`Ctrl+Shift+B`), закрыть лишние вкладки.
3. Запись: 1920×1080, микрофон поближе, тишина вокруг. Удобно — OBS или встроенная запись экрана (Win: `Win+Alt+R`, Mac: `Cmd+Shift+5`).
4. Перед записью **один раз прогоните свою часть без записи**, чтобы знать куда кликать.
5. Пароль у всех демо-аккаунтов: `Password123` (на странице Login есть кнопки быстрого входа).
6. В начале и в конце каждого куска — 2 секунды тишины, так проще клеить.

| # | Время | Кто | Что |
|---|---|---|---|
| 1 | 0:00–0:30 | Мадина | Слайды 1–2: команда, цель, три роли |
| 2 | 0:30–1:15 | Мирас | Слайд 3: архитектура и безопасность |
| 3 | 1:15–2:30 | Замира | Сайт: гость и покупатель (customer) |
| 4 | 2:30–3:45 | Мирас | Сайт: владелец ресторана (owner) |
| 5 | 3:45–5:00 | Ильяс | Сайт: админ + MySQL + тесты |
| 6 | 5:00–6:00 | Мадина | Слайды 4–5: структура кода и таблица вклада |

---

## 1. Мадина — слайды 1–2 (0:00–0:30)

**Слайд 1** — название «Food Advisor», F28JC Web Programming, CW1.2, CE 202 Group 4, четыре имени.

> **Hello! We are Group 4 from CE 202, and this is our project for F28JC Web Programming — Food Advisor.
> Our team is Madina Bazarbayeva, Zamira Nurmanova, Ilyas Sungatov and Miras Yernazarov.**

**Слайд 2** — цель проекта + три иконки ролей: Customer, Restaurant owner, Administrator.

> **Food Advisor helps people find restaurants and dishes in Aktobe, Almaty and Astana.
> The site has three roles. Customers search, filter and review restaurants.
> Owners manage their own restaurants and menus. And administrators moderate users, restaurants and reviews.
> Now Miras will explain how the system works.**

---

## 2. Мирас — слайд 3, архитектура (0:30–1:15)

**Слайд 3** — схема из README (раздел 3): Browser → JSON API (Node.js + Express) → MySQL.
Пока говоришь, показывай мышкой по схеме слева направо.

> **Our application has three layers.
> In the browser we use HTML, CSS and jQuery. The pages talk to the server only with AJAX requests, and all data is sent as JSON.
> The back end is Node.js with Express. It is split into routes: auth, restaurants, dishes, reviews, profile, owner and admin.
> The data is stored in MySQL — nine tables with foreign keys and indexes.
> Security was important for us. Passwords are hashed with scrypt, every SQL query uses placeholders against SQL injection, and every owner and admin action is checked on the server by role. So even if someone changes the page, the server still says no.
> We also use Web Storage — for the login token, dark mode, favourites and recent searches.
> Now Zamira will show the site as a customer.**

---

## 3. Замира — гость и покупатель (1:15–2:30)

Начинаешь **не залогиненной**, на главной странице.

| На экране | Что говоришь |
|---|---|
| Главная → блок **«What should I eat today?»**: выбрать город, бюджет, настроение → крутить рулетку | **This is the home page. If you don't know what to eat, you can spin our roulette. I choose the city and budget — and it picks a dish for me.** |
| В поиске набрать `plov` — появятся подсказки | **The search gives live suggestions for restaurants, cuisines and dishes.** |
| **Explore restaurants** → фильтры: город, кухня, рейтинг, цена, **Open now** | **On the Explore page I can filter by city, cuisine, rating and price, or show only places that are open now. The filters are saved in the link, so I can share the results.** |
| Открыть ресторан → меню → нажать на блюдо → **See nutrition & details** | **This is the restaurant page with the menu. For every dish we show calories, protein, fat, carbs and allergens.** |
| Login → кнопка демо **Customer** | **Now I log in as a customer.** |
| В ресторане, где есть кнопка **Write a review** → оценка + текст → опубликовать (будет конфетти) → **Edit** → поменять оценку | **I write a review with a rating… publish it… and I can edit or delete my own review at any time. The average rating updates straight away.** |
| Нажать **Helpful** на чужом отзыве, сердечко ❤ на ресторане | **I can mark other reviews as helpful and save restaurants to my favourites.** |
| **Profile** → My reviews, Favourites, Browsing history | **In my profile I see my reviews, favourites, recently viewed restaurants and recent searches. The history is kept in the browser with localStorage.** |
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
| MySQL Workbench (или терминал `mysql`) → показать список таблиц и `SELECT * FROM restaurants LIMIT 5;` | **Here is our MySQL database: nine tables — users, sessions, cuisines, restaurants, dishes, reviews, votes, reports and favourites — connected with foreign keys.** |
| Терминал: `npm test` (сервер должен быть запущен) → показать что все **42 passing** | **Finally, our 42 automated tests check every functional requirement and the security rules — for example, that customers cannot open owner pages and that SQL injection does not work. All tests pass. Back to Madina.** |

---

## 6. Мадина — слайды 4–5 (5:00–6:00)

**Слайд 4** — структура кода (папки из README, раздел 3: `server.js`, `server/routes`, `server/middleware`, `database`, `public`, `tests`).

> **To sum up, here is how our code is organised.
> server.js starts the Express app. The server folder has the routes, the middleware for login and roles, and helper functions for validation and passwords.
> The database folder has the MySQL schema and the sample data. The public folder has all the HTML pages, the CSS and the jQuery scripts. And the tests folder has our automated tests.
> We used only the technologies from the course: HTML, CSS, JavaScript with jQuery, JSON, Node.js and MySQL.**

**Слайд 5** — Team Member Contribution Table (README, раздел 7 — **проверьте, что там правда, кто что делал!**).

> **This table shows what each of us did.
> I was the reporter — I did the documentation, the video and the submission.
> Zamira built the front end — the pages, the design and the responsive layout.
> Miras built the back end — the REST API, login, roles and security.
> And Ilyas designed the database and wrote the tests.
> Thank you for watching!**

---

## 7. Монтаж (Мирас)

- Порядок клипов: 1 → 2 → 3 → 4 → 5 → 6. Итог должен быть **не длиннее 6:00**.
- Если кусок длиннее своего времени — ускорить «скучные» места (ввод текста, загрузку) до 1.5×, а не сам голос.
- Между клипами — простой переход (cut или 0.3 с fade), на кадрах сайта можно добавить подпись «Customer / Owner / Admin».
- Громкость у всех выровнять (normalize audio).
- Экспорт: MP4, 1080p.
