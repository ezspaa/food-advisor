# 🎤 Dämdi — шпаргалка к Q&A (защита 2 декабря, Room 121)

Ответы — **на английском** (так их и говорить), пояснения — на русском.
Учитель спрашивает **каждого** про приложение и **про его собственный вклад**. Учите в первую очередь свой раздел, потом общий.

---

## Как отвечать

- **Коротко: 1–3 предложения**, потом можно показать в коде или на сайте («Let me show you…»).
- Не знаешь — не выдумывай. Скажи честно и передай тому, кто знает:
  > **"I'm not sure about that detail — Miras worked on the server part, he can explain it better."**
- Вопрос «что именно ты сделал?» — говори **только правду**, своими словами, с примером (файл, страница, что проверял). Учитель предупредил, что вклад проверяют.
- Держите сайт открытым и VS Code с проектом под рукой: показать файл — сильнее любого ответа.

---

## 👥 Общие вопросы (знать всем)

**What is Dämdi?**
> Dämdi is our Food Advisor web application. People can find restaurants and dishes in Aktobe, Almaty and Astana, filter them and read reviews. Owners manage their restaurants, and admins moderate the site. "Dämdi" means "tasty" in Kazakh.

**What are the three roles?**
> Customer — searches, reviews and saves favourites. Owner — manages their own restaurants, menus and replies. Admin — approves restaurants, blocks users and removes bad reviews.

**Which technologies did you use?**
> Only the course technologies: HTML and CSS, JavaScript with jQuery, JSON, Node.js with Express, MySQL and Web Storage. No React and no extra libraries apart from Express and the MySQL driver.

**How does the front end talk to the back end?**
> With AJAX calls from jQuery to our REST API under /api. The data is sent as JSON in both directions.

**How do you run the project?**
> Install Node.js and MySQL, then run `npm run go`. It installs the packages, creates the database with sample data and opens the browser. The demo password for all accounts is Password123.

**What would you improve with more time?**
> Real photo uploads instead of image links, email password reset, and a map view of restaurants.

**Did you use AI tools?** — отвечайте **честно**, как было на самом деле. Если использовали, скажите это прямо и добавьте, что понимаете код и можете объяснить его. Скрывать хуже, чем сказать.

---

## 🟢 Мадина — Reporter (intro, code structure, contribution table)

Твоя зона: организация работы, документация, видео, сдача, общая картина проекта.

**How did you organise the team work?**
> We split the work by role: front end, back end, database and testing, and documentation. We kept the code in one GitHub repository, and I collected everything for the README, the slides, the video and the Canvas submission.

**What is in the README?**
> How to install and run the project, the demo accounts, the tools we used, an architecture diagram, a table that maps every functional requirement to pages, API and database, and the team contribution table.

**How is the code organised?** (слайд 5)
> By responsibility. server.js starts Express. server/routes holds the REST API, one file per area. server/middleware checks login and roles. server/utils has validation and password hashing. database has the schema, sample data and a full MySQL dump. public has the pages, CSS and jQuery scripts. tests has 42 automated tests.

**Does the app meet the functional requirements from CW1.1?**
> Yes, all thirteen. For example: registration and login, search and filters, reviews you can edit and delete, owner menus, and admin moderation. The README has a table that shows where each one is done.

**Why is it called Dämdi and not Food Advisor?**
> Dämdi is the brand name of our Food Advisor app. We wanted a local Kazakh name, and the functionality is exactly what we proposed in CW1.1.

**What did you personally do?** — расскажи правду своими словами. Опирайся на то, что реально делала (планирование, README, слайды, видео, сдача).

---

## 🔵 Замира — Front-end (customer features)

Где код: `public/*.html` (страницы), `public/css/style.css` (дизайн), `public/js/*.js` (jQuery: `core.js` — общее, `explore.js` — поиск и фильтры, `restaurant.js` — страница ресторана).

**How did you use jQuery?**
> For DOM changes, events and AJAX. For example, when you change a filter on the Explore page, jQuery sends an AJAX request to the API and redraws the list of restaurants without reloading the page.

**What is AJAX and where do you use it?**
> AJAX means loading data from the server in the background. All our pages do it — for example search suggestions, filters, writing a review and saving favourites. All requests go through one helper function, FA.api in core.js.

**What do you keep in Web Storage?**
> In localStorage: the login token, the dark or light theme, guest favourites, recently viewed restaurants, recent searches and the compare list. In sessionStorage: the review draft, so you don't lose your text if you leave the page.

**What is the difference between localStorage and sessionStorage?**
> localStorage stays after you close the browser. sessionStorage is cleared when you close the tab.

**What happens to favourites if a guest logs in?**
> A guest's favourites are saved in localStorage. When they log in, we send them to the server and save them in the database, so they are not lost.

**How is the site responsive?**
> We use CSS grid and flexbox with media queries. On a phone, the menu collapses and the filters open in a drawer.

**How do you validate forms?**
> In the browser with JavaScript, so the user sees errors straight away under each field. But the server checks everything again, because browser checks can be skipped.

**How do you protect against XSS?**
> Every text from users is escaped with our FA.esc function before we put it into the page, so HTML or script tags show as plain text. The server also sends a Content Security Policy.

**How does the dark mode work?**
> All colours are CSS variables. The dark theme changes these variables, and the choice is saved in localStorage.

**What did you personally do?** — правду своими словами (какие страницы смотрела, что тестировала, что исправляла).

---

## 🟠 Мирас — Back-end (architecture, owner features)

Где код: `server.js`, `server/routes/*.js` (API), `server/middleware/auth.js` (логин и роли), `server/middleware/security.js` (заголовки, rate limit), `server/utils/` (валидация, пароли).

**Explain the architecture.** (слайд 3)
> Three layers. The browser sends AJAX requests with JSON to our Node.js and Express server. The server checks the user and the input, then talks to MySQL with parameterised SQL and sends JSON back.

**How does login work?**
> When you log in, the server creates a random token and sends it to the browser. The browser keeps it in localStorage and sends it in the Authorization header with every request. In the database we store only the SHA-256 hash of the token, with an expiry date of 7 days.

**How are passwords stored?**
> Never as plain text. We hash them with scrypt from Node's built-in crypto module, with a random salt for every user. When checking a password we use a constant-time comparison.

**How do you make sure a customer can't use admin features?**
> Roles are checked on the server. The admin routes use requireRole('admin') and the owner routes use requireRole('owner'). Even if someone changes the page, the server answers 403 Forbidden.

**What is the difference between 401 and 403?**
> 401 means you are not logged in. 403 means you are logged in, but your role is not allowed to do this.

**How can an owner edit only their own restaurant?**
> Every owner query has `WHERE owner_id = ?` with the logged-in user's id. If it's not your restaurant, the query finds nothing and you get an error. We test this in our automated tests.

**How do you prevent SQL injection?**
> We never put user input directly into SQL. Every query uses question-mark placeholders, and the MySQL driver escapes the values.

**What other security did you add?**
> A rate limiter: after 20 failed login attempts in 15 minutes from one address, the server blocks further tries. Plus security headers like Content-Security-Policy and X-Frame-Options, and a central error handler that never shows internal errors to the user.

**What is a REST API?**
> The server gives URLs for resources, like /api/restaurants, and the HTTP method says what to do: GET reads, POST creates, PUT updates and DELETE deletes.

**What happens when an owner adds a restaurant?**
> It is saved with the status "pending", so it is not public. An admin has to approve it first.

**What did you personally do?** — правду своими словами (что проверял на сервере, что исправлял, деплой, дизайн Dämdi, сборка видео).

---

## 🟣 Ильяс — Database & QA (admin features, database, tests)

Где код: `database/schema.sql` (таблицы), `database/setup.js` (демо-данные), `database/food_advisor_dump.sql` (полный дамп), `tests/api.test.js` (тесты), `server/routes/admin.js`.

**What tables do you have?**
> Ten: users, sessions, cuisines, restaurants, dishes, reviews, review_votes, review_reports, favorites and feedback.

**How are the tables connected?**
> With foreign keys. For example, a dish belongs to a restaurant, and a review belongs to a user and a restaurant. If a restaurant is deleted, its dishes and reviews are deleted too — that's ON DELETE CASCADE.

**What constraints do you use?**
> UNIQUE — one email per user and only one review per user per restaurant. CHECK — the rating must be between 1 and 5 and prices can't be negative. Plus NOT NULL and foreign keys.

**Why do you have indexes?**
> To make search and filters fast. We have indexes on the columns we filter by, like city, cuisine, price and status.

**How is the average rating calculated?**
> We don't store it. We calculate it with SQL — AVG(rating) with GROUP BY — only from visible reviews. So when an admin hides a review, the average updates automatically.

**What can an admin do?**
> Approve or reject new restaurants, edit or remove any restaurant, block or delete users, hide or delete reviews, handle reported reviews, manage cuisines and read site feedback.

**What happens when you block a user?**
> Their status becomes "blocked" and all their sessions are deleted, so they are logged out at once and cannot log in again.

**How did you test the application?**
> We have 42 automated end-to-end tests with Node's built-in test runner. They call the real API and check every functional requirement and the security rules — for example, wrong roles get 403, SQL injection is treated as plain text, and one user can't edit another's review. Run them with `npm test` while the server is running.

**What is the database file you submitted?**
> A full MySQL dump. You can load it with `mysql -u root -p < database/food_advisor_dump.sql`, or the app creates the same database automatically on the first start.

**What did you personally do?** — правду своими словами (что делал в базе, какие тесты запускал, какие баги нашёл).

---

## ✅ Перед защитой

- [ ] Каждый прочитал **свой раздел** и общий, вслух хотя бы раз.
- [ ] Каждый может открыть **свой файл** в VS Code и показать 1–2 вещи.
- [ ] Ноутбук: `npm run db:setup`, `npm start`, проверить вход за все три роли.
- [ ] Интернет есть (фото блюд грузятся из сети), раздача с телефона наготове.
- [ ] Приходят **все четверо** — иначе ABS и 0 лично.
