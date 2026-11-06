<p align="center">
  <img src="./drops-stash.svg" width="76" height="76" alt="Twitch Drops Stash logo">
</p>

<h1 align="center">Twitch Drops Stash</h1>

<p align="center">
  <strong>Windows x64 · 0.2.0 Beta 1 · Pre-release</strong><br>
  <a href="#возможности">Русский</a> · <a href="#english">English</a>
</p>

Приложение для Windows, которое находит кампании Twitch Drops, отслеживает прогресс и автоматически забирает доступные награды. Сейчас доступна публичная бета для тестирования.

**[Скачать Beta 1 для Windows x64](https://github.com/kry3/twitch-drops-stash/releases/download/v0.2.0-beta.1/Twitch-Drops-Stash-0.2.0-beta.1-Windows-x64.zip)** · [Описание релиза и SHA-256](https://github.com/kry3/twitch-drops-stash/releases/tag/v0.2.0-beta.1) · [Сообщить об ошибке](https://github.com/kry3/twitch-drops-stash/issues)

## Возможности

- Автоматический выбор канала и получение наград после подтверждения Twitch.
- Очередь игр, приоритет отслеживаемых каналов и обзор доступных кампаний.
- Инвентарь с прогрессом, просмотр трансляции, работа в трее и автозапуск.
- Русский и английский интерфейс, светлая и тёмная темы.

## Как это работает

После входа приложение загружает доступные кампании, выбирает подходящую трансляцию по очереди игр и отслеживает прогресс по данным Twitch. Если эфир закончится, оно подберёт другой подходящий канал. Когда Twitch подтвердит выполнение условий, приложение заберёт награду.

## Первый запуск

1. Распакуйте ZIP в отдельную папку с правом записи.
2. Запустите **Twitch Drops Stash.exe**. Приложению нужен Microsoft Edge WebView2 Runtime.
3. Войдите в Twitch через браузер. Для кампаний с привязкой свяжите аккаунт Twitch с аккаунтом игры.

## Тестирование и обратная связь

Сборка проверялась на Windows 11 x64. Windows 10 x64 и Windows 11 ARM64 ещё требуют проверки.

При ошибке укажите версию Windows, шаги воспроизведения и результат в [GitHub Issues](https://github.com/kry3/twitch-drops-stash/issues). В ZIP есть инструкция по сохранению диагностического отчёта. Проверьте его содержимое перед публикацией.

---

## English

Twitch Drops Stash is a Windows app for finding Twitch Drops campaigns, tracking progress, and automatically claiming eligible rewards. The public beta includes a game queue, followed-channel priorities, an inventory, a stream viewer, tray controls, and a Russian and English interface.

**[Download Beta 1 for Windows x64](https://github.com/kry3/twitch-drops-stash/releases/download/v0.2.0-beta.1/Twitch-Drops-Stash-0.2.0-beta.1-Windows-x64.zip)** · [Release notes and SHA-256](https://github.com/kry3/twitch-drops-stash/releases/tag/v0.2.0-beta.1) · [Report a bug](https://github.com/kry3/twitch-drops-stash/issues)

Extract the ZIP to a writable folder, run **Twitch Drops Stash.exe**, and sign in to Twitch in your browser. Microsoft Edge WebView2 Runtime is required. Windows 11 x64 has been tested. Windows 10 x64 and Windows 11 ARM64 still need testing.

For bug reports, include your Windows version, the steps to reproduce the issue, and what happened. The ZIP explains how to save a diagnostic report. Review it before sharing.

---

Сборка / Build by **kry3**. Основано на / Based on [TwitchDropsMiner by DevilXD](https://github.com/DevilXD/TwitchDropsMiner). Лицензия / License: [MIT](./LICENSE).
