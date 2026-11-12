# Частые вопросы · FAQ

Twitch Drops Stash — сборка **kry3**. Основа — [DevilXD/TwitchDropsMiner](https://github.com/DevilXD/TwitchDropsMiner),
MIT. Здесь ответы на то, что спрашивают чаще всего. Если ответа нет — «О приложении →
Сообщить об ошибке» в приложении.

## Это вирус? Windows пишет «Неизвестный издатель»

Нет. Подписи издателя у сборки пока нет: сертификат стоит денег, и его нет. Windows
показывает синее окно всем неподписанным программам одинаково.

- Нажмите **«Подробнее»**, затем **«Выполнить всё равно»**.
- Сверьте сумму файла с суммой в заметках к выпуску:
  `Get-FileHash "Twitch Drops Stash.exe" -Algorithm SHA256`.
- Приложение показывает SHA-256 своего файла при первом запуске, а кнопка «Снять метку
  “скачано из интернета”» убирает предупреждение до следующего скачивания архива.

Откуда взять сумму для сверки: заметки к выпуску на странице загрузок, раздел с архивом.

## Сколько это ест трафика

Видео и звук не скачиваются вообще: приложение только сообщает Twitch «я смотрю». Работы —
порядка мегабайта в час: плейлист канала, короткие запросы «я смотрю» и опрос инвентаря.
Приложение считает потраченное само и не оценивает на глаз: знакомство при первом запуске
показывает цифру за текущую сессию («За 2.0 ч приложение получило от Twitch 2.0 МБ»).

Отдельно стоит обновление: оно скачивается целиком, 22 МБ (23 188 792 байта), и на время
загрузки занимает канал. Это единственный момент, когда приложение действительно забирает
скорость.

## Почему не растут баллы канала

Потому что Twitch начисляет баллы за просмотр только настоящему плееру. Приложение
отправляет событие «просмотрел минуту», Twitch его принимает (ответ 204) и баллы не
начисляет — это проверено измерением: 373 принятых минуты подряд, баланс не изменился.
Бонусы (кнопка «Забрать» в чате) забирать можно, но это экспериментальная часть.

## Шкала стоит, награда не идёт

С 0.7.0 Beta 10 в строке состояния видно, когда Twitch последний раз отвечал: «проверено
только что», «проверено 4 мин назад». Если 15 минут нет ни ответов, ни прогресса —
появляется плашка «Похоже, Twitch не отвечает» с кнопкой «Переподключиться». Если десять
минут не прибавляется зачтённая минута, приложение само пересобирает связь один раз и
говорит об этом, если перезапуск не помог.

Что проверить самому: сеть и VPN, часы Windows (рассинхрон ломает запросы Twitch), не
смотрите ли вы тот же канал в браузере — Twitch считает одну минуту на аккаунт, а не две.

## Приложение не запускается или окно пустое

- Нужен **Microsoft Edge WebView2 Runtime** (в Windows 11 он уже есть, в Windows 10 —
  чаще всего есть). Без него интерфейс не отрисуется.
- Приложение не любит папки только для чтения: распакуйте архив в «Документы» или в
  отдельную папку, куда можно писать.
- Антивирус может заблокировать первый запуск неподписанного EXE: разрешите файл в
  исключениях.
- При старте приложение проверяет сеть, Twitch, часы и запись в папку: если что-то не так,
  появится строка с причиной и кнопкой действия.

## Нужен ли браузер и где хранится вход

Браузер нужен только для входа: приложение открывает страницу Twitch в вашем обычном
браузере (Chrome, Edge, Vivaldi или Brave), вы входите там, а приложение получает только
токен. Пароль оно не видит. Токен хранится в `cookies.jar` рядом с EXE — не открытым
текстом, а зашифрованным средствами Windows для вашей учётной записи (DPAPI): скопировать
файл на другую машину или прочитать его блокнотом и получить вход нельзя. «Выйти из
аккаунта» удаляет сессию, «Аккаунты» позволяют держать несколько входов.

## Twitch пишет «Ваш браузер не поддерживается»

Это ответ Twitch на старую сборку браузера, а не на приложение: такой браузер не может
войти, и токен в приложение не придёт. Начиная с 1.0.1 приложение открывает браузеры от
самого нового к старому и само переходит к следующему, если Twitch отказал. Если отказ
остался — «Настройки» → «Браузер для входа»: выберите Edge (он обновляется вместе с
Windows) или обновите другой браузер, затем нажмите «Войти в Twitch» ещё раз.

## Что в журнале и уходит ли он куда-нибудь

Журнал (`diagnostics\events.jsonl` рядом с EXE) пишется по умолчанию, чтобы у ошибки было
описание. В нём: версия, система, события сбора, имена отслеживаемых каналов, id аккаунта.
Токена входа в нём нет. Сам по себе он никуда не отправляется: уходит только то, что вы
отправите кнопкой «Сообщить об ошибке». Отключить журнал можно файлом `diagnostics.disabled`
рядом с EXE.

## Куда уходит отчёт об ошибке и идея

Два пути. **Telegram** — личное сообщение автору: кроме него никто не видит, аккаунт GitHub
не нужен. **GitHub** — публичное обращение: видно всем и остаётся в истории.

По умолчанию предлагается Telegram, и это работает в любой сборке: в неё вложен ключ только
на отправку. Прочитать этим ключом нельзя ничего — ни чужие отчёты, ни служебные данные: он
умеет единственное — дописать сообщение в чат автора. Поэтому его наличие в файлах сборки
ничего не раскрывает. Если сервер отчётов не отвечает, выбор сам переходит на GitHub, а не
остаётся «выбранным, но мёртвым».

Отправка из одной сети ограничена (несколько отчётов за четверть часа) — это защита от
чужого потока сообщений в чат автора. При отказе приложение скажет, сколько ждать, и
предложит GitHub.

В любом случае уходит версия и технические данные сборки, а описание вы пишете сами и видите
перед отправкой.

## Как обновиться и как откатиться

«О приложении» → «Проверить обновления» → «Скачать обновление» (сумма сверяется с
опубликованной) → «Установить и перезапустить». Прежний EXE сохраняется как
`Twitch Drops Stash.exe.bak-update`; если новая сборка не подтвердила работу интерфейса,
помощник вернёт прежний. Итог установки — `updates\result.json` и `updates\updater.log`.

Откат вручную: полностью выйдите из приложения и верните прежний EXE из
`.bak-update` на его место. Сессия, настройки и собранные часы сохранятся.

## Обновление скачивается медленно

Архив обновления — 22 МБ (23 188 792 байта) одним файлом: патча нет, сборка перекрывается
целиком. Лежит он на GitHub, и скорость здесь зависит только от маршрута до GitHub, а не от
приложения: приложение читает файл блоками без паузы и ничего не ограничивает. Замер с
одного российского канала: 130–295 КБ/с, то есть от полутора до трёх минут; на плохом
маршруте те же 22 МБ идут десять и больше минут.

С 1.0.2 под полосой прогресса видно скорость и остаток («13 МБ из 22 МБ · 60% ·
295 КБ/с · ~2 мин»), а в журнал пишется строка `update_download` — сколько байт пришло,
за сколько секунд и с какой средней скоростью. Если загрузка оборвалась, в журнале
останутся `status: error` и то, сколько успело прийти, а раз в 10 секунд — замер скорости:
по присланному журналу видно, ровный канал или рваный, и где именно он просел. Размер
обновления показан до нажатия («Доступна версия 1.0.2 · 22 МБ»), чтобы не начинать его вслепую.

Если связь оборвалась на середине, с 1.0.2 скачивание не начинается заново: приложение
просит у сервера остаток и дописывает файл, а контрольная сумма в конце проверяется
по-прежнему. Обрыв на 4,4 МБ стоит докачать 18 МБ, а не все 22.

После 100% есть короткая пауза: приложение закрывается, помощник заменяет EXE и ждёт
подтверждения запуска (до 45 секунд). Полоса в этот момент уже не двигается, это нормально.
Если новая сборка не запустилась, помощник вернёт прежнюю.

## Это не нарушает правила Twitch

Честный ответ: автоматизация просмотра — серая зона. Twitch требует, чтобы Drops
засчитывались за реальный просмотр, и оставляет за собой право ограничить аккаунт за
накрутку. Приложение не скачивает видео, не выдаёт себя за плеер и не накручивает часы
сверх кампаний, но решение использовать его — ваше, и риск на вас. Мы не обещаем, что
Twitch не изменит правила или не заблокирует аккаунт.

## Чем это отличается от TwitchDropsMiner

Это форк: код сбора — от [DevilXD/TwitchDropsMiner](https://github.com/DevilXD/TwitchDropsMiner)
(MIT), интерфейс, вход через браузер, обновления, несколько аккаунтов, сторож сбора и
отчёты — наши. Авторство основы и лицензия сохранены в `LICENSE`.

---

# FAQ (English)

Twitch Drops Stash is built by **kry3**, based on
[DevilXD/TwitchDropsMiner](https://github.com/DevilXD/TwitchDropsMiner) (MIT).

**Is it a virus? Windows says "Unknown publisher".** No. The build has no publisher
signature: a certificate costs money and is not there yet. Press **More info** →
**Run anyway**, then compare the file sum with the release notes:
`Get-FileHash "Twitch Drops Stash.exe" -Algorithm SHA256`. The app shows its own SHA-256 on
first start, and the "Remove the downloaded mark" button stops the warning until the archive
is downloaded again.

**How much traffic does it use?** No video or sound is downloaded: the app only tells Twitch
"I am watching". A few megabytes a day. The app measures it: the first-run introduction shows
the figure for the current session.

**Why do channel points not grow?** Twitch credits watch points only to a real player. The app
sends the "watched a minute" event, Twitch accepts it (204) and credits nothing — measured:
373 accepted minutes, no change in the balance. Claiming bonuses stays experimental.

**The bar is stuck.** Since 0.7.0 Beta 10 the status line says when Twitch last answered, and
after 15 minutes of silence a note with Reconnect appears. After ten minutes without a
credited minute the app rebuilds the connection itself once, and says so if that did not
help.

**It does not start or the window is blank.** You need Microsoft Edge WebView2 Runtime;
extract to a writable folder; allow the unsigned EXE in your antivirus. At start the app
checks the network, Twitch, the clock and folder access, and names the cause with an action.

**Twitch says "Your browser is not supported".** That is Twitch's answer to an old browser
build, not to the app: such a browser cannot sign in and no token comes back. Since 1.0.1 the
app opens browsers newest first and moves to the next one when Twitch refuses. If the refusal
stays: Settings → Sign-in browser — pick Edge (it updates with Windows) or update the other
browser, then select Sign in to Twitch again.

**Where is the sign-in kept?** Only a token, in `cookies.jar` next to the EXE — not as plain
text: Windows encrypts it for your user account (DPAPI), so copying the file to another
machine or reading it in Notepad does not give anyone your sign-in. The password is never
seen by the app: you sign in on the Twitch site in your browser.

**What is in the journal?** `diagnostics\events.jsonl`: version, system, collection events,
followed channel names, account id. No sign-in token. It never leaves the machine by itself:
only what you send with the "Report a problem" button. `diagnostics.disabled` turns it off.

**Where does a report or an idea go?** Two ways. **Telegram** is a private message to the
author: nobody else sees it, and no GitHub account is needed. **GitHub** is a public issue:
everyone sees it and it stays in the history.

Telegram is offered first and it works in every build: the app carries a key that may only
send. That key cannot read anything — not other people's reports, not the service data — it
can only append a message to the author's chat, so having it in the shipped files reveals
nothing. If the report server does not answer, the choice moves to GitHub by itself instead
of staying "selected but dead".

Sending from one network is limited (a few reports per quarter of an hour) so that a foreign
flood cannot fill the author's chat; a refusal names the wait and offers GitHub.

Either way it carries the version and the technical data of the build, and the description is
yours — it stays visible before sending.

**How do I update or roll back?** About → Check for updates → Download → Install and restart.
The previous EXE is kept as `Twitch Drops Stash.exe.bak-update` and restored if the new build
does not confirm its interface. To roll back by hand, exit completely and put the old EXE back.

**Does it break Twitch's rules?** An honest answer: automating viewing is a grey area. Twitch
requires real viewing for Drops and may restrict accounts for artificial watch time. The app
does not download video, does not pretend to be a player, and does not farm hours beyond the
campaigns, but the decision and the risk are yours.
