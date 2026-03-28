# 🤖 Agentic CMS

**Статический шаблон сайта для малого бизнеса, управляемый ИИ-агентом через естественный язык.**

Вместо традиционной админ-панели контентом управляет ИИ-агент (Gemini CLI), который редактирует Markdown-файлы и коммитит изменения через GitHub — сайт пересобирается автоматически.

## Стек

- **[Astro.js](https://astro.build/)** — статическая генерация (SSG)
- **[Tailwind CSS 4](https://tailwindcss.com/)** — стилизация
- **GitHub Pages** — хостинг + CI/CD
- **Gemini CLI + Agent Skills** — ИИ-администратор (LUI)

## Архитектура контента

Данные хранятся в Markdown/JSON файлах, типизированных через [Astro Content Collections](https://docs.astro.build/en/guides/content-collections/):

| Коллекция | Описание | Формат |
|-----------|----------|--------|
| `pages` | Уникальные страницы (Главная, О нас) | Markdown |
| `nodes` | Типовой контент (позиции меню, занятия) | Markdown |
| `blocks` | Переиспользуемые фрагменты (баннеры, отзывы) | Markdown |
| `taxonomy` | Словари для группировки (категории, уровни) | Markdown |
| `staff` | Профили сотрудников | Markdown |
| `settings` | Глобальные настройки (меню, часы работы) | JSON |

## Быстрый старт

```bash
# Клонировать шаблон
git clone https://github.com/ai-denser-ru/Agentic_CMS.git my-site
cd my-site

# Установить зависимости
npm install

# Запустить dev-сервер
npm run dev

# Собрать для продакшена
npm run build
```

## Структура проекта

```
src/
├── content/           ← Контент (Markdown + JSON)
│   ├── pages/         ← Страницы сайта
│   ├── nodes/         ← Позиции, услуги, новости
│   ├── blocks/        ← Промо-баннеры, врезки
│   ├── taxonomy/      ← Категории, теги, уровни
│   ├── staff/         ← Сотрудники
│   └── settings/      ← Навигация, контакты, часы работы
├── content.config.ts  ← Zod-схемы всех коллекций
├── layouts/           ← HTML-каркасы страниц
├── components/        ← Header, Footer
└── pages/             ← Роутинг (Astro file-based)
```

## Деплой

Деплой на GitHub Pages происходит автоматически при push в `main` через GitHub Actions (`.github/workflows/deploy.yml`).

## Лицензия

MIT
