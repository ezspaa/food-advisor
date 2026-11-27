# 🎤 Dämdi — живая защита CW1.2

**Среда, 2 декабря · 9:00–13:00 · Room 121 · CE-202**
~**6 минут** + Q&A. Выступают и отвечают **все четверо**. Кто не пришёл, получает «absent» за CW1.2. Если кто-то не может прийти, он должен заранее подать **mitigating circumstances**.

Структура, как просил учитель: **1) intro → 2) architecture → 3) live demo всех функций (бо́льшая часть времени) → 4) code structure → 5) contribution table**, потом Q&A про **структуру и детали кода**.

Текст для речи на **английском** (жирным), пояснения на русском.

---

## ⏱ План (5:50)

| Время | Кто | Часть | Что на экране |
|---|---|---|---|
| 0:00–0:25 | Мадина | 1. Intro | Слайды 1–2 |
| 0:25–1:00 | Мирас | 2. Architecture | Слайд 3 (слайд 4 пролистать) |
| 1:00–2:30 | Замира | 3. Demo: guest + customer (FR1–FR7) | Сайт |
| 2:30–3:45 | Мирас | 3. Demo: owner (FR8–FR10) | Сайт |
| 3:45–4:50 | Ильяс | 3. Demo: admin (FR11–FR13) | Сайт |
| 4:50–5:40 | Мадина | 4. Code structure + 5. Team | Слайды 5–6 |
| 5:40–5:50 | Мадина | Конец → Q&A | Слайд 7 |

**Демо занимает 3:50 из 5:50**, как и требует учитель («most of your time»).

---

## 🔧 Подготовка

### Накануне: репетиция всем вместе с секундомером
- Пройти весь сценарий **2 раза подряд**. Если выходит дольше 6:00, сокращать текст, а не говорить быстрее.
- Каждый **сам кликает в своей части**: так видно, что он знает приложение.

### Утром 2 декабря, на ноутбуке Мираса
```bash
git pull
```
```bash
npm run db:setup
```
```bash
npm start
```
- `db:setup` обязательно: сбрасывает данные, чтобы спам-отзыв и спамер были на месте, а прошлые тестовые отзывы исчезли.
- **Chrome, окно 1:** слайды Dämdi в режиме **Present**. **Окно 2:** сайт `http://localhost:3000`, **без входа** в аккаунт. Переключаться между окнами: **Cmd+`** (клавиша слева от 1).
- Масштаб сайта **Cmd+0**, потом **Cmd+=** один раз, чтобы с задних рядов было видно.
- **VS Code открыт** с проектом: на Q&A будут вопросы по коду.
- **Интернет** нужен: фото блюд и слайды грузятся из сети. Держи раздачу с телефона наготове. Слайды заранее **скачай в PDF** (Share → Export) на случай, если сеть пропадёт.
- Зарядка и переходник **USB-C → HDMI**.
- Уведомления выключить (режим «Не беспокоить»).

---

## 1. Мадина: Intro (0:00–0:25), слайды 1–2

**Слайд 1:**
> **Good morning! We are Group 4 from CE-202. Our Food Advisor web application is called Dämdi — it means "tasty" in Kazakh. I'm Madina, and this is Zamira, Ilyas and Miras.**

(Когда называешь имена, показывай рукой на каждого.)

**Слайд 2** (→):
> **Dämdi helps people decide where to eat in Aktobe, Almaty and Astana. It has three roles: customers find and review restaurants, owners manage their own restaurants and menus, and admins keep the content trustworthy. Miras will explain how it works.**

---

## 2. Мирас: Architecture (0:25–1:00), слайд 3

Веди рукой или мышкой по схеме: **Client → Server → Data**.
> **Dämdi has three layers. The browser uses HTML, CSS and jQuery, and talks to our server only with AJAX and JSON.
> The server is Node.js with Express. It has a REST API, checks the login token and the user's role on every request, and validates all input.
> The data is in MySQL — ten tables with foreign keys. All SQL uses placeholders, so SQL injection is not possible.
> We used only the course technologies.** *(здесь листаешь слайд 4 и сразу дальше)*
> **Now Zamira will show the site live.**

**Переключиться на окно с сайтом: Cmd+`**

---

## 3a. Замира: guest и customer (1:00–2:30), FR1–FR7

Начинаешь на главной, **без входа**.

| Клик | Говоришь |
|---|---|
| Главная | **This is the home page.** |
| В поиске набрать `plov`, появятся подсказки | **The search shows live suggestions for restaurants, cuisines and dishes.** *(FR2)* |
| **Restaurants** → фильтр по городу **Aktobe**, кухне, рейтингу **4.0+**, галочка **Open now** | **On the Explore page I can filter by city, cuisine, rating and price, or show only places open now.** *(FR2)* |
| Открыть ресторан → меню → клик по блюду (окно с калориями) | **This is a restaurant page with its menu. Every dish has nutrition facts and allergens.** *(FR3)* |
| **Sign up** → имя `Zamira Demo`, email `zamira@demo.kz`, пароль `Password123` два раза, галочка «I agree» → **Create account** | **Now I register a new customer account.** *(FR1)* |
| Открыть любой ресторан → **Write a review** → 5 звёзд, заголовок `Great plov`, текст `Very tasty plov and fast service.` → опубликовать | **I write a review…** *(FR4)* |
| У своего отзыва **Edit** → поменять на 4 звезды → сохранить | **…and I can edit or delete my own review. The average rating updates straight away.** *(FR5)* |
| Сердечко ❤ на ресторане | **I save the restaurant to my favourites.** *(FR7)* |
| **Profile** → изменить город → **Save**. Показать **Favourites** и **Browsing history** | **In my profile I can update my details, and see my favourites, recently viewed restaurants and recent searches — the history is kept in localStorage.** *(FR6, FR7)* |
| Меню справа вверху → **Log out** | **And I log out. Miras will show the owner side.** *(FR1)* |

💡 Новый аккаунт хорош тем, что у него ещё нет отзывов, поэтому **отзыв можно оставить в любом ресторане**.

---

## 3b. Мирас: owner (2:30–3:45), FR8–FR10

**Log in** → демо-кнопка **Owner**.

| Клик | Говоришь |
|---|---|
| **Dashboard** | **This is the owner dashboard: average rating, reviews per month and the rating breakdown — calculated in SQL with AVG, COUNT and GROUP BY.** *(FR10)* |
| **+ Add restaurant** → название `Dämdi Demo Café`, кухня **Kazakh**, описание `A cosy café for the live demo of Dämdi.`, город `Aktobe`, адрес `Abai Avenue 1`, цена **₸₸** → **Save** | **I add a new restaurant. It starts as pending — not public until an admin approves it.** *(FR8)* |
| У **Dastarkhan House** нажать **Edit** → поменять время закрытия → **Save** | **I can edit my own restaurant, and delete it with this button.** *(FR8, на Delete только показываешь, не нажимаешь)* |
| **Menu** → **Add dish**: `Demo Baursak`, **Starters**, цена `800` → **Save** | **I add a dish to the menu…** *(FR9)* |
| У этого блюда выключить переключатель **Available** (блюдо закончилось), потом **Delete** | **…mark it as sold out, and delete it.** *(FR9)* |
| **Reviews** → **Reply** на любой отзыв → `Thank you for visiting!` → **Save** | **I can reply to guest reviews, and the reply is shown publicly.** *(FR10)* |
| **Log out** | **An owner can only change their own restaurants — the server checks owner_id on every request. Ilyas will show the admin panel.** |

📋 Тексты для формы ресторана скопируй заранее в Заметки, чтобы вставлять через **Cmd+V**, а не печатать.

---

## 3c. Ильяс: admin (3:45–4:50), FR11–FR13

**Log in** → демо-кнопка **Admin**.

| Клик | Говоришь |
|---|---|
| **Overview** | **This is the admin panel with the main statistics.** |
| **Restaurants** → фильтр **Pending** → у `Dämdi Demo Café` нажать **Approve** | **Miras's new restaurant is waiting here. I approve it, and now it is public.** *(FR12)* |
| **Reports** → отзыв от *Best Deals KZ* → **Hide review** | **Users reported this review as spam. I hide it, and the restaurant's rating is recalculated.** *(FR13)* |
| **Users** → найти *Best Deals KZ* → **Block** | **Then I block the spammer. A blocked user is logged out at once and can't log in.** *(FR11)* |
| **Restaurants** → у `Dämdi Demo Café` нажать **Edit** (показать), потом корзину → подтвердить | **Admins can edit or remove any restaurant.** *(FR12)* |
| **Log out** | **Back to Madina.** |

---

## 4–5. Мадина: code structure + team (4:50–5:40), слайды 5–6

**Cmd+`** → окно со слайдами → **слайд 5**:
> **Our code is organised by responsibility. server.js starts Express. The routes folder has the REST API, one file per area. The middleware checks login and roles. The database folder has the schema, sample data and a MySQL dump. The public folder has the pages, CSS and jQuery scripts. And we have 42 automated tests.**

**Слайд 6** (→):
> **This is our contribution table.** *(называешь каждого коротко, показывая строку)* **I was the reporter — documentation, slides and video. Zamira led the front end, Miras the back end, and Ilyas the database and testing.**

**Слайд 7** (→):
> **Thank you! We're happy to answer your questions.**

---

## ❓ Q&A: «In the Q&A, you will be asked about the structure and details of your code»

Учитель будет спрашивать **по коду**. Каждый должен уметь **открыть VS Code и показать 2–3 места из своей части**. Ответы на типовые вопросы есть в [`qa-cheatsheet.md`](qa-cheatsheet.md), а ниже то, что **показать в коде**.

### Мадина: общая структура
| Покажи | Где | Скажи |
|---|---|---|
| Дерево папок | левая панель VS Code | **Routes, middleware, utils, database, public, tests — each folder has one job.** |
| Как подключаются маршруты | `server.js`, строки 23–31 | **Each area of the API is a separate router file, mounted under /api.** |
| Таблица требований | `README.md`, раздел 4 | **This table maps every functional requirement to its page, API and SQL.** |

### Замира: front-end
| Покажи | Где | Скажи |
|---|---|---|
| Все AJAX-запросы | `public/js/core.js`, строка 50 (`FA.api`) | **Every request goes through this function: it adds the token and sends JSON.** |
| Web Storage | `public/js/core.js`, строка 17 (`makeStore`), 33 | **A small wrapper around localStorage and sessionStorage.** |
| Защита от XSS | `public/js/core.js`, строка 83 (`FA.esc`) | **We escape all user text before putting it into the page.** |
| Фильтры в адресе | `public/js/explore.js`, строки 18–27 | **The filters are saved in the URL, so results can be shared.** |
| Синхронизация избранного | `public/js/core.js`, строка 544 | **Guest favourites are sent to the server after login.** |

### Мирас: back-end
| Покажи | Где | Скажи |
|---|---|---|
| Проверка роли | `server/middleware/auth.js` (`requireRole`) | **If the role is wrong, the server returns 403.** |
| Логин | `server/routes/auth.js`, строка 53 | **We check the password and create a random token; only its hash is stored.** |
| Хеш пароля | `server/utils/password.js` | **scrypt with a random salt, compared in constant time.** |
| Свой ресторан | `server/routes/owner.js`, строка 17 (`owner_id = ?`) | **Every owner query checks owner_id, so you can't edit someone else's restaurant.** |
| Валидация | `server/utils/validate.js`, строка 93 | **The same rules run on the client and on the server.** |

### Ильяс: база и тесты
| Покажи | Где | Скажи |
|---|---|---|
| Таблица отзывов | `database/schema.sql`, строка 135 | **CHECK rating 1–5, UNIQUE one review per user per restaurant, foreign keys with CASCADE.** |
| Блокировка | `server/routes/admin.js`, строка 90 | **When we block a user, we delete their sessions, so they are logged out.** |
| Одобрение ресторана | `server/routes/admin.js`, строка 142 | **The admin changes the status from pending to approved.** |
| Тесты | `tests/api.test.js` + запуск `npm test` | **42 tests grouped by functional requirement — all pass.** |

### Если не знаешь ответ
> **"That part was done by Miras — Miras, can you explain?"**
Это нормально. Плохо — выдумывать.

**Вопрос про свой вклад** («What did you do?») задают **каждому**. Отвечать **правду**, своими словами и с примером.
