# Twitch Drops Stash 1.0.0

Короткое имя сборки — **1.0**; номер версии в приложении — `1.0.0`.

## Русский

Первая стабильная сборка. Это код release candidate (0.7.0 Beta 13) с номером 1.0 и двумя
правками по делу: канал отчёта по умолчанию и живая ссылка на частые вопросы. Новых экранов
и новых обещаний не появилось.

Twitch Drops Stash собирает награды Twitch Drops, не скачивая видео и звук: приложение
сообщает Twitch, что вы смотрите канал, само переключается, когда эфир кончается, и забирает
награду, когда Twitch подтвердит условия. Вход — на сайте Twitch в вашем браузере, пароль
приложение не видит.

### Что важно знать при первом запуске

- **Знакомство из трёх шагов.** Что приложение делает и чего не делает, вход, выбор «что
  собирать». Кнопка «Пропустить» есть на каждом шаге, настройки по умолчанию рабочие.
- **Предупреждение Windows.** Подписи издателя нет, поэтому Windows скажет «Неизвестный
  издатель». Нажмите «Подробнее» → «Выполнить всё равно»; в знакомстве показана сумма
  SHA-256 запущенного файла, и её можно сверить с суммой в заметках к выпуску. Кнопка «Снять
  метку “скачано из интернета”» убирает предупреждение до следующего скачивания архива.
- **Самопроверка окружения.** При запуске проверяются сеть, доступность Twitch, часы, запись
  в папку и предупреждение Windows. Пока всё в порядке — ничего не показывается; если что-то
  не так, появляется строка с причиной и одним действием.
- **Трафик измеряется.** Знакомство показывает, сколько байт приложение получило от Twitch за
  сессию: за сутки это единицы мегабайт, а не гигабайты.

### Что изменилось за время беты

- **Сторож сбора и восстановление после сна.** Десять минут без зачтённой минуты при живом
  канале — один автоматический перезапуск связи и запись в журнал; если не помогло, приложение
  говорит об этом и предлагает «Переподключиться». Пауза в работе больше 15 секунд (сон,
  гибернация, заморозка) — пересборка связи.
- **Ошибки человеческим языком.** Ни одного имени класса исключения на экране; у ошибки есть
  действие и кнопка «Сообщить об ошибке», которая подставляет описание и прикладывает журнал.
- **Журнал у всех.** Локальный журнал (`diagnostics\events.jsonl`) пишется по умолчанию: без
  него отчёт нечего прикладывать. Он остаётся на компьютере и уходит только по нажатию кнопки.
- **Вёрстка при изменении размера окна.** Единственная открытая P1 с 9 ноября закрыта замером:
  28 сочетаний «страница × ширина» (1510, 1320, 1100, 960) и два языка с двумя темами чистые.
- **«Проверено N минут назад» и плашка застоя.** Видно, когда Twitch последний раз отвечал, и
  когда сбор стоит.
- **Пауза с длительностью, уведомление о награде, экспорт наград в CSV, несколько аккаунтов,
  обновления с проверкой суммы и откатом.**
- **Баллы канала честно помечены.** Начисление баллов за просмотр не работает и не может
  работать без настоящего плеера — это измерено: 373 принятых минуты подряд, баланс не
  изменился. Забор бонусов остаётся экспериментальным.
- **Отчёт и идея — сначала в Telegram, и в любой сборке.** Оба окна предлагают личное
  сообщение автору, а не публичное обращение: аккаунт GitHub для этого не нужен. Раньше
  Telegram работал только на машине автора — ключ лежал в файле рядом с EXE, и у всех
  остальных канал просто не предлагался. Теперь в сборку вложен ключ только на отправку:
  прочитать им нельзя ничего, дописать сообщение в чат автора — можно. GitHub остаётся
  вторым вариантом и страховкой, когда сервер отчётов молчит.
- **«Частые вопросы» ведут на FAQ.** Раньше кнопка упиралась в пустую страницу: файла не было
  в репозитории. Теперь FAQ есть и в приложении, и в архиве, и на странице загрузок.

### Правки после проверки 11 ноября

Проверка перед выпуском нашла семь мест, где приложение вело себя хуже, чем говорит. Всё
исправлено и перепроверено на этой же сборке:

- **Если программа не может запуститься, она объясняет почему.** Раньше окно просто не
  появлялось: ошибка до старта интерфейса уходила в никуда. Теперь — сообщение с причиной и
  строкой в `startup-error.log` рядом с EXE; второй запуск так же говорит, что приложение уже
  работает, вместо тихого выхода.
- **Канал Telegram не объявлен недоступным до ответа сервера.** В первые секунды окно отчёта
  честно пишет «Проверяем канал Telegram…» вместо переключения выбора на GitHub.
- **Заметки к обновлению показываются оформленными:** заголовки, списки и ссылки собираются из
  разметки выпуска, а сам текст остаётся текстом — ничего из сети не становится разметкой окна.
- **Журнал сторожа пишет настоящую длительность молчания** (раньше всегда было `0`).
- **Ответ на некорректный запрос — по-русски**, а не текстом разборщика JSON.
- **FAQ уточняет, как хранится вход:** токен в `cookies.jar` зашифрован средствами Windows для
  текущей учётной записи, поэтому скопировать файл на другую машину и войти нельзя.

### Что не проверено

- **Windows 10 x64 и Windows 11 ARM64.** Проверена только Windows 11 x64.
- **Долгий прогон.** 72 часа без вмешательства на живой машине эта сборка ещё не отработала;
  сторож и восстановление проверены тестами и короткими прогонами.
- **Чужие установки.** Отзывов от людей, которые поставили сборку сами, пока нет.

### Подпись

Подписи издателя нет: сертификат стоит денег, и его нет в бюджете. Раздел про SmartScreen
объясняет предупреждение и даёт проверить файл, но не отменяет окно Windows.

### Если вы были на канале «Стабильный»

До 1.0 стабильных сборок не было, поэтому канал «Стабильный» отдавал беты. Теперь на нём
появилась 1.0 — это и есть обновление, переключать канал не нужно. Пометка «Стабильной
сборки ещё нет» пропадёт сама.

## English

Short name: **1.0**; the version number in the app is `1.0.0`.

The first stable build. It is the release-candidate code (0.7.0 Beta 13) with the number 1.0
and two honest fixes: the default report channel and a working link to the questions page. No
new screens and no new promises.

Twitch Drops Stash collects Twitch Drops rewards without downloading video or sound: the app
tells Twitch you are watching a channel, switches by itself when the stream ends, and claims
the reward once Twitch confirms the conditions. You sign in on the Twitch site in your
browser; the app never sees your password.

### What matters on the first start

- **A three-step introduction.** What the app does and does not do, signing in, and choosing
  what to collect. Every step can be skipped and the defaults work.
- **The Windows warning.** There is no publisher signature, so Windows says "Unknown
  publisher". Press More info → Run anyway; the introduction shows the SHA-256 of the running
  file, which you can compare with the release notes. The "Remove the downloaded mark" button
  stops the warning until the archive is downloaded again.
- **An environment check.** Network, Twitch availability, the clock, folder access and the
  Windows warning are checked at start. While everything is fine, nothing is shown; if not, a
  line with the cause and one action appears.
- **Traffic is measured.** The introduction shows how many bytes the app received from Twitch
  in the session: a few megabytes a day, not gigabytes.

### What changed during the beta

- **Watchdog and recovery after sleep.** Ten minutes without a credited minute while a channel
  is live: one automatic rebuild of the connection and a journal row; if that did not help, the
  app says so and offers Reconnect. A loop pause longer than 15 seconds (sleep, hibernation,
  freeze) rebuilds the connection.
- **Errors in human language.** No exception class names on screen; every error has an action
  and a "Report a problem" button that fills the description and attaches the journal.
- **A journal for everyone.** The local journal (`diagnostics\events.jsonl`) is written by
  default: without it a report has nothing to attach. It stays on the machine and leaves only
  when the button is pressed.
- **Layout at window sizes.** The only open P1 since 9 November is closed by measurement: 28
  page × width combinations (1510, 1320, 1100, 960) are clean in two languages and two themes.
- **"Checked N minutes ago" and the stall note.** You can see when Twitch last answered and
  when collection is stuck.
- **Pause with a duration, reward notification, reward history as CSV, several accounts,
  updates with checksum verification and rollback.**
- **Channel points are labelled honestly.** Earning points from watching does not work and
  cannot work without a real player — measured: 373 accepted minutes, no change in the balance.
  Claiming bonuses stays experimental.
- **Reports and ideas go to Telegram first — in every build.** Both dialogs offer a private
  message to the author instead of a public issue: no GitHub account is needed. Telegram used
  to work only on the author's machine, because the key lived in a file next to the EXE; now
  the build carries a send-only key that cannot read anything and can only append a message
  to the author's chat. GitHub stays the second option and the fallback while the report
  server is silent.
- **"Frequently asked questions" leads to the FAQ.** The button used to open an empty page:
  the file was not in the repository. The FAQ now exists in the app, in the archive, and on
  the download page.

### Fixes after the 11 November check

The pre-release check found seven places where the behaviour was worse than the claims. All
are fixed and re-checked on this build:

- **If the app cannot start, it says why.** It used to show nothing at all: an error before the
  interface existed disappeared. Now a message names the cause and the same line lands in
  `startup-error.log` next to the EXE; a second launch says the app is already running instead
  of exiting silently.
- **The Telegram channel is not declared unavailable before the server answers.** For the first
  seconds the report dialog says "Checking the Telegram channel…" instead of moving the choice
  to GitHub.
- **Update notes are shown formatted:** headings, lists and links are built from the release
  markup while the text stays text — nothing from the network becomes window markup.
- **The watchdog journal records the real silence** (it was always `0`).
- **A malformed request is answered in Russian**, not with the JSON parser's English text.
- **The FAQ explains how the sign-in is stored:** the token in `cookies.jar` is encrypted by
  Windows for the current account, so copying the file elsewhere does not sign anyone in.

### Not verified

- **Windows 10 x64 and Windows 11 ARM64.** Only Windows 11 x64 has been tested.
- **A long run.** 72 hours unattended on a live machine have not happened for this build yet;
  the watchdog and the recovery are covered by tests and short runs.
- **Other people's installs.** There are no reports from people who installed the build
  themselves.

### Signature

There is no publisher signature: a certificate costs money and is not in the budget. The
SmartScreen section explains the warning and lets you verify the file; it does not remove the
Windows window.

### If you were on the Stable channel

Before 1.0 there were no stable builds, so the Stable channel served betas. It now has 1.0 —
that is the update, no channel switch needed. The "no stable build yet" note disappears by
itself.

Сумму SHA-256 этого архива печатает публикация и ставит последней строкой ниже — из тех
байт, которые получил GitHub, а не из черновика: пересборка меняет сумму, и вписанное руками
число обещало бы проверку другого файла.

The SHA-256 of this archive is printed by the publication and appended below from the bytes
GitHub received — not typed in here: a rebuild changes the sum, and a hand-written number
would invite people to verify the wrong file.
