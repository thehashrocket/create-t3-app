---
title: Перші кроки
description: Початок роботи з вашим новим T3 App
layout: ../../../layouts/docs.astro
lang: uk
---

Ви щойно створили новий додаток T3 і готові до роботи. Ось мінімум для запуску вашої програми.

## База даних

### MySQL, PostgreSQL

Якщо ви обираєте MySQL або PostgreSQL як свою базу даних, ваше T3 додаток буде починатись з `start-database.sh` bash-скриптом, який може створити контейнер Docker з базою даних для локальної розробки. Якщо у вас вже є база даних, ви можете видалити цей файл і вказати свої облікові дані для бази даних в `.env`. На macOS ви також можете використовувати [DBngin](https://dbngin.com/), якщо ви не хочете використовувати Docker.

### Prisma

Якщо ваш додаток включає Prisma, переконайтеся, що ви запустили `npx prisma db push` з кореневої директорії вашої програми. Ця команда синхронізує схему Prisma з вашою базою даних і генерує типи TypeScript для Prisma Client на основі вашої схеми. Зверніть увагу, що вам потрібно [перезапустити сервер TypeScript](https://tinytip.co/tips/vscode-restart-ts/) після цього, щоб він міг виявити згенеровані типи.

### Drizzle

Якщо ваш додаток включає в себе Drizzle, перевірте `.env` файл для інструкцій щодо побудови вашої змінної середовища `DATABASE_URL`. Як тільки ваш файл середовища готовий, запустіть `pnpm db:push` (або еквівалент для інших менеджерів пакетів), щоб відправити вашу схему.

## Аутентифікація

Якщо ваш додаток включає NextAuth.js, ми починаємо з `DiscordProvider`. Це один з найпростіших провайдерів, пропонований NextAuth.js, однак він все ще вимагає певного початкового налаштування з вашого боку.

Звичайно, якщо ви віддаєте перевагу використанню іншого провайдера автентифікації, ви також можете використати один із [багатьох провайдерів](https://next-auth.js.org/providers/), які пропонує NextAuth.js.

1. Вам потрібен обліковий запис Discord, тому зареєструйтеся, якщо ще не зареєструвалися.
2. Перейдіть на https://discord.com/developers/applications і натисніть "New Application" у правому верхньому куті. Дайте вашому додатку ім'я та погодьтеся з Умовами використання.
3. Коли ви створите додаток, перейдіть до "Settings → OAuth2 → General".
4. Скопіюйте "Client ID" і додайте його у ваш `.env` як `DISCORD_CLIENT_ID`.
5. Натисніть "Reset Secret", скопіюйте новий secret і додайте його у ваш `.env` як `DISCORD_CLIENT_SECRET`.
6. Натисніть "Add Redirect" і введіть `http://localhost:3000/api/auth/callback/discord`.
   - Для деплойменту в продакшені дотримуйтесь попередніх кроків для створення іншого додатка Discord, але цього разу замініть `http://localhost:3000` на URL, на який ви деплоїте.
7. Збережіть зміни.
8. Встановіть `NEXTAUTH_SECRET` у `.env`. У розробці будь-який рядок працюватиме, для продакшена див. примітка в `.env` про генерацію безпечного secret.

Тепер у вас має бути можливість увійти в систему.

## Сетап едітора

Наступні розширення рекомендуються для оптимального досвіду розробки. Нижче наведені посилання на підтримку плагінів для редактора.

- [Prisma Extension](https://www.prisma.io/docs/guides/development-environment/editor-setup)
- [Tailwind CSS IntelliSense Extension](https://tailwindcss.com/docs/editor-setup)
- [Prettier Extension](https://prettier.io/docs/en/editors.html)

## Наступні кроки

- Якщо ваш додаток включає tRPC, ознайомтеся з `src/pages/index.tsx` і `src/server/trpc/router/post.ts`, щоб дізнатися, як працюють запити tRPC.
- Подивіться на документацію `create-t3-app`, а також на документацію пакетів, які включає ваш додаток.
- Приєднуйтесь до нашого [Discord](https://t3.gg/discord) і поставте зірку на [GitHub](https://github.com/t3-oss/create-t3-app)! :)