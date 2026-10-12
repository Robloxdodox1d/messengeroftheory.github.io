# 💬 Мессенджер

Простой мессенджер на чистом HTML/CSS/JS + Firebase Realtime Database.
Работает как статический сайт — идеально для GitHub Pages.

## Возможности

- 🔐 Вход по имени (анонимная авторизация Firebase)
- 💬 4 комнаты: `#general`, `#random`, `#tech`, `#music`
- ⚡ Реальное время — сообщения появляются мгновенно
- 👥 Счётчик онлайн-пользователей
- 📱 Адаптивный дизайн (мобильная версия с выезжающим меню)
- 🎨 Автоматические аватары с уникальными цветами
- 📅 Разделители дат (Сегодня / Вчера)

---

## 🚀 Настройка за 5 минут

### 1. Создайте Firebase-проект

1. Перейдите на [console.firebase.google.com](https://console.firebase.google.com/)
2. **Add project** → введите имя → создайте проект
3. Слева выберите **Build → Realtime Database** → **Create Database**
4. Выберите регион → **Start in test mode** (потом заменим правила)

### 2. Включите анонимную авторизацию

1. **Build → Authentication → Get started**
2. Вкладка **Sign-in method** → включите **Anonymous**

### 3. Получите конфиг

1. ⚙️ **Project settings** (шестерёнка) → вкладка **General**
2. Прокрутите до **Your apps** → нажмите `</>` (Web)
3. Зарегистрируйте приложение
4. Скопируйте объект `firebaseConfig`

### 4. Вставьте конфиг в `index.html`

Найдите в `index.html` блок:

\`\`\`js
const firebaseConfig = {
  apiKey: "YOUR_API_KEY",
  // ...
};
\`\`\`

Замените на свой из Firebase.

### 5. Настройте правила безопасности

В Firebase Console → **Realtime Database → Rules** вставьте:

\`\`\`json
{
  "rules": {
    "messages": {
      ".read": "auth != null",
      "$room": {
        ".write": "auth != null"
      }
    },
    "online": {
      ".read": "auth != null",
      "$uid": {
        ".write": "auth != null && auth.uid === $uid"
      }
    }
  }
}
\`\`\`

Нажмите **Publish**.

---

## 🌐 Деплой на GitHub Pages

1. Создайте репозиторий на GitHub
2. Загрузите `index.html` и `README.md` в корень
3. **Settings → Pages**
4. Source: **Deploy from a branch** → Branch: `main` / `root`
5. Через минуту сайт будет доступен по адресу:
   `https://<ваш-username>.github.io/<название-репозитория>/`

---

## 🎨 Кастомизация

### Добавить комнаты

Найдите в `index.html`:

\`\`\`js
const ROOMS = ['general', 'random', 'tech', 'music'];
\`\`\`

Добавьте свои, например: `['general', 'games', 'memes']`

### Изменить цвета

В блоке `:root` поменяйте:

\`\`\`css
--accent: #6366f1;   /* основной цвет (кнопки) */
--bg: #0f0f10;       /* фон */
\`\`\`

---

## ⚠️ Ограничения бесплатного тарифа Firebase

- 10 ГБ трафика в месяц
- 100 одновременных подключений
- 1 ГБ хранилища

Для личного проекта и небольшого сообщества — с запасом.
