<!-- Повторный аудит после редакторского прохода 2026-10-09. Предыдущий аудит доредакционной версии заменён; независимое ревью, по которому делались правки, — review-2026-10-09/ch04.md -->

# Повторный аудит главы 4 «Экономика и бизнес-модели AdTech» (после правок 2026-10-09)

Входы: `master-prompt.md` §10 строка «#### 4.» (4.1–4.15), §3 и §7 Stage B (контракт оформления); `plans/ru/04-adtech-economics-business-models.plan.md`; `chapters/ru/04-adtech-economics-business-models.md`; `chapters/en/04-adtech-economics-business-models.md`; `glossary.md`, `glossary.en.md`. Режим: только чтение. Предыдущие аудиты (`audits/ru/*.audit.md`, `review-2026-10-09/ch04.md`) до вынесения вердикта не читались.

---

# РОЛЬ 1 — Coverage & Accuracy Auditor (RU)

# Резюме аудита

Все 15 требований TOC раскрыты по существу и в заявленном ракурсе (contractual basis, billable event, risk allocation; формулы главы 3 не повторяются). Вся арифметика главы пересчитана и сходится: сквозной путь `$100 → $80 → $68`, spread `$20`, SSP retained `$12`, проверка `$20 + $12 + $68 = $100`; markup `25%` / take rate `20%`; все шесть строк блока «Знаменатели»; таблица gross/net (`$100/$80/$20/20%` и `$20/$0/$20/100%`); пять альтернативных контрактов на `$100`; разложение на центы `20/12/68`. Фактических ошибок, искажённых money/data flow и устаревших утверждений не найдено. Блокеров нет.

Вердикт определяется контрактом оформления: найдены нарушения, которые по `agents/auditor.md` и §7 Stage B квалифицируются как IMPORTANT и блокируют PASS — термины глоссария без сноски (`agency`, `reach`, `served`, `rendered`), сноска не при первом упоминании (`advertiser spend`), бытовые английские слова из явного списка в прозе (`entity`/`entities`, `boundary`), дата исследования в прозе («2026 года»). Все исправления точечные — одно-два слова каждое.

# Блокеры

None.

# Важные проблемы

1. **Термины глоссария без сноски.**
   - Строка 49 (таблица моделей, строка CPM): «`served`, `rendered`, `viewable`[^g-viewable-impression]» — `viewable` снабжён сноской, а `served` и `rendered` нет, хотя в `glossary.md` есть `{#g-served-impression}` и `{#g-rendered-impression}`. В главе `g-served-impression` и `g-rendered-impression` не встречаются ни разу.
   - Строка 130 («Fixed fee и SaaS»): «agency retainer за ведение campaigns» — `agency` имеет статью `{#g-agency}`, сноски нет.
   - Строка 256 («Arbitrage»): «могут оплачивать aggregation, reach, service» — `reach` имеет статью `{#g-reach}`, сноски нет.
2. **Сноска не при первом упоминании.** `advertiser spend[^g-media-spend]` поставлена на строке 108, но понятие уже использовано на строке 27 в таблице слоёв («Для кого сумма является spend, cost, payout…»; «`$100` spend advertiser»). На той же строке 27 `media cost` получил сноску `[^g-cost]` при первом упоминании — для `spend` правило не соблюдено. (Аналогичный, но более спорный случай — `payout` на строке 27 против `publisher payout[^g-publisher-payout]` на строке 136; на строке 27 это слово стоит в общем вопросе, поэтому вынесено в необязательные.)
3. **Бытовые английские слова из явного списка §3 в прозе.**
   - `entity`/`entities`: строка 194 «**Reporting entity** — компания, чью финансовую отчётность мы читаем»; строка 222 «которые reporting entity классифицирует»; строка 306 «из-за разных reporting entities и counterparties»; строка 323 «cost of revenue одной reporting entity». Глава сама даёт русский эквивалент («компания, чью финансовую отчётность мы читаем»), поэтому замена на «отчитывающаяся компания» ничего не теряет.
   - `boundary`: строка 71 «billable event лежит внутри их measurement boundary»; строка 304 (таблица ledger, ячейка Publisher) «85% of SSP-boundary proceeds» — здесь ещё и английский предлог `of` внутри русской таблицы. В code blocks (строки 104–105, 287–292) `SSP-boundary` допустим как метка формулы.
4. **Дата исследования в прозе.** Строка 256: «но его rates нельзя использовать как current benchmark 2026 года». Это маркер актуальности на дату research, который §3 предписывает держать только в разделе источников (там он и так есть, строка 351). Достаточно «как актуальный benchmark» или «на момент написания». (Упоминание «CMA 2020 года» — исторический факт об исследовании, не нарушение.)

# Необязательные улучшения

1. **Заголовки с неустоявшимся английским.** «## Как зарабатывают intermediaries и software providers» — `software providers` не established term (ср. правило `## Contract arithmetic — нет`); «### Fixed fee и SaaS: отдельные money flows» — `money flow` используется в самом master-prompt как рабочий термин курса, поэтому допустимо, но «отдельные денежные потоки» было бы чище.
2. **Плотность code-switching в прозе** сверх явного списка: `scenario` (строка 260 «в одном scenario»), `batch` (252 «предоплаченном batch»), `customer` (8 раз; защитимо как термин ASC 606 «contract with a customer», но на строке 53 «не стать customer» — бытовое употребление), «чьему count доверяет» (71), «decision input» (83), «Публичные filings» (233). Не нарушение контракта по букве, но снижает читаемость.
3. **`payout` на строке 27** упомянут раньше сноски `[^g-publisher-payout]` (строка 136) — см. п. 2 важных проблем; решение за Editor.
4. **«Представление gross или net» на строке 28** — концепт `g-gross-net-revenue` фактически введён здесь, а сноска стоит на строке 108 при словосочетании «gross revenue». Формально словосочетание первое на 108, поэтому не нарушение, но можно перенести сноску на строку 28.
5. **Строка 71** «Publisher и SSP … поэтому продают по CPM» — универсализация; publisher-side продаёт и по CPC (search, контекстные сети). Добавить «обычно».
6. **Строка 201** «получать существенные выгоды» — в ASC 606-10-25-25 control означает «substantially all of the remaining benefits»; «практически все выгоды» точнее.
7. **Повтор примера `$12/$80` vs `$12/$100` и `$20/$80` vs `$20/$100`.** Эти пары выводятся в разделе 3 (строки 104–108, 117–126), полностью повторяются в «Знаменатели» (287–295), в ledger-таблице (303), в «С чем это часто путают» (321) и в «Проверьте себя» (339). Блок «Знаменатели» можно сократить до строк, которых ещё не было (`combined`, `publisher payout share`).
8. **Частичное дублирование** «С чем это часто путают» ↔ «Что важно запомнить»: пункты 3↔2 (проценты без denominator), 5↔5 (gross margin vs take rate), 6↔6 (arbitrage). Суммарно 13 пунктов — в пределах 12–14.
9. **Объём.** Чистая проза до раздела источников (без front matter, таблиц, code blocks, заголовков) — около 2 580 слов, с разделом источников — около 2 820. Превышение ориентира 2 400 примерно на 7 %, не материальное; резерв — п. 7.
10. **Строки 235–236** «Magnite в Form 10-K за 2025 год» / «The Trade Desk в Form 10-K за 2025 год» — это идентификация документа, не дата проверки, поэтому не нарушение; при желании можно оставить год только в источниках 5–6 и писать «в своём последнем Form 10-K».

# Проверка корректности

Пересчёт (выполнен скриптом, все значения совпали с текстом):

- Арифметика договоров (273–279): `10,000 / 1,000 × $10 = $100`; `10,000 / 1,000 × $8 = $80`; spread `$20`; `15% × $80 = $12`; `85% × $80 = $68`; `$20 + $12 + $68 = $100`. ✔
- Знаменатели (287–292): `$20/$80 = 25%`; `$20/$100 = 20%`; `$12/$80 = 15%`; `$12/$100 = 12%`; `$32/$100 = 32%`; `$68/$100 = 68%`. ✔ Центы (282): 20 / 12 / 68. ✔
- Revenue share (104–105): `$12/$80 = 15%`, `$68/$80 = 85%`. ✔ Markup/take rate (117, 123): `25%`, `20%`. ✔
- Таблица gross/net (217–220): principal `$100 − $80 = $20`, `20%`; agent `$20 − $0 = $20`, `100%`. ✔ Совпадение `20%` gross margin и `20%` take rate корректно объяснено как учебное (231).
- Пять контрактов (63–67): `10,000 × $10/1,000`, `200 × $0.50`, `20 × $5`, `25 × $4`, `10 × $10` — все `$100`. ✔
- Ledger-таблица (299–304) согласована с money-label diagram (144–148) и invoice/cash flow (181–187): `$100 / $80 / $68`, receivable/payable направлены верно.

Содержательные утверждения:

- Auction win ≠ billable event; `nurl` vs `burl` (57) — соответствует IAB Programmatic Auction Definitions и OpenRTB 2.x Implementation Guidelines §7.8–7.9; корректно оговорено как programmatic-пример общего правила.
- Pricing basis / optimization target / фактическая метрика (73–83) — корректное разделение, product-specific пример помечен как таковой.
- Markup на cost vs take rate на spend vs gross margin на recognized revenue (112–126) — определения верны и не смешаны.
- Principal/agent через control над specified good/service, индикаторы как evidence, а не балльный тест (196–211) — соответствует ASC 606-10-55-36–40 и IFRS 15 B34–B38. Caveat «mental model, не accounting advice» присутствует (238).
- Gross billings ≠ recognized revenue (194); примеры Magnite (net для platform transactions, gross для части IO-кампаний) и The Trade Desk (gross billings vs net revenue) согласуются с планом и источниками 5–6, помечены как company-specific.
- Arbitrage: price risk vs volume risk при per-impression покупке и prepaid batch (252), basis mismatch как performance risk (254), «не любой fee — arbitrage» (256) — верно.
- Accrued → billed → settled (159–163), receivable/payable как направление обязательства, а не момент cash (155) — верно.
- Ссылка «главы 15–18» для programmatic (18) соответствует TOC (15 Programmatic, 16 DSP/SSP/Exchange, 17 Impression lifecycle, 18 RTB Auction).
- Front matter: `toc_requirements` 4.1–4.15 совпадают с TOC; `id`, `part`, `chapter`, `slug`, `prerequisites [ch-01, ch-02, ch-03]` корректны.

# Проверка границ и плотности

- Границы плана соблюдены: формулы главы 3 не переобъясняются; auction mechanics ограничены одной ссылкой на `nurl`/`burl`; affiliate, yield, SPO, reconciliation pipelines, taxes/FX только названы как исключённые (165, 267); accounting не выходит за decision sketch.
- Повторы внутри главы — см. необязательные п. 7–8. Повторов соседних глав не обнаружено (глава 2 роли, глава 3 формулы — используются как vocabulary).
- Объём — см. необязательные п. 9: ~2 580 слов прозы до источников, превышение ориентира незначительное.
- Диаграммы и таблицы согласованы с прозой (проверено: money-label diagram, event flow, invoice/cash flow, ledger-таблица, таблица gross/net).

# Проверка контракта оформления

| Пункт контракта | Результат |
|---|---|
| Ровно один H1 | ✔ строка 14 |
| Секции `##`, подсекции `###`; хвост `## С чем это часто путают` → `## Что важно запомнить` → `## Проверьте себя` → `## Источники и дополнительное чтение` | ✔ строки 317, 326, 336, 343; порядок верный |
| Вводная `## Суть` | ✔ строка 16 (с подзаголовком через двоеточие) |
| Заголовки и шапки таблиц по-русски, английский только как термин | ✔ шапки всех 6 таблиц русские; заголовки — замечание по `software providers` (необязательное п. 1) |
| Каждая `[^g-id]` разрешается в `{#g-id}` глоссария | ✔ 56 сносок, 56 уникальных id, все найдены в `glossary.md` |
| Один термин — одна сноска | ✔ дублей нет |
| Каждый термин со статьёй в глоссарии имеет сноску | ✘ `served`, `rendered` (49), `agency` (130), `reach` (256) — важная проблема 1 |
| Сноска при первом упоминании | ✘ `advertiser spend` (27 → 108) — важная проблема 2; `payout` (27 → 136) — спорно |
| Бытовые английские слова из явного списка | ✘ `entity`/`entities` ×4 (194, 222, 306, 323), `boundary` (71, 304) — важная проблема 3 |
| Без дат проверки/research-пометок в прозе | ✘ «current benchmark 2026 года» (256) — важная проблема 4; «Источники проверены 2026-08-28» стоит в разделе источников — ✔ |
| Front matter полный и согласован с TOC | ✔ |
| Проза ≤ ~2 400 слов; Confusions + Remember ≤ 12–14 пунктов | ~2 580 (незначительно выше, необязательное п. 9); 6 + 7 = 13 ✔ |

# Coverage Table

| Requirement | Status | Evidence / Explanation |
|---|---|---|
| 4.1 CPM | ✅ COVERED | Раздел «CPM, CPC и outcome pricing»: строка CPM в таблице моделей (49) — billable event «тысяча qualifying impressions», риск payee/advertiser, обязательность named basis `served/rendered/viewable` и владельца count; альтернативный контракт `10,000 × $10 CPM` (63); «В CPM buyer уже должен `$100`, даже если подписок нет» (69); отделение от bid/target/observed (18, 83). Формула главы 3 не повторяется. |
| 4.2 CPC | ✅ COVERED | Строка CPC (50): qualifying click как trigger, impression-to-click risk у payee, post-click risk у advertiser, click point/deduplication/invalid-click filters как billing contract; `200 × $0.50` (64); пример CPC billing при `target CPA` (75–83). |
| 4.3 CPA/CPI/CPL | ✅ COVERED | Строки CPA/CPI/CPL (51–53) с отдельными action/install/lead, validator/attribution owner и остаточным quality/LTV risk advertiser; вывод «сдвиг риска, а не исчезновение» (55); три альтернативных контракта (65–67); объяснение выбора модели через measurement boundary и postback (71). |
| 4.4 revenue share | ✅ COVERED | Таблица моделей (91); подраздел «Revenue share: процент без базы не определён» (97–108): определение proceeds и revenue share, обязательные параметры договора, worked split `$12/$80 = 15%`, `$68/$80 = 85%`, запрет переноса 15% на `$100` (12%). |
| 4.5 fixed fee и SaaS pricing | ✅ COVERED | Таблица (92–93); подраздел «Fixed fee и SaaS: отдельные money flows» (128–138): типовые случаи fixed fee, мотив предсказуемости и снятия конфликта incentives, распределение риска; `$2,000/month` как fixed или usage tier, явное отделение от `$100 media flow` и условие объединения в одном договоре. |
| 4.6 markup | ✅ COVERED | Таблица (94); подраздел «Markup, spread и take rate» (110–126): spread как абсолютная разница, `markup = $20/$80 = 25%` с denominator на acquisition cost, отличие от gross margin. |
| 4.7 take rate | ✅ COVERED | Таблица (95); `take rate = $20/$100 = 20%` (120–126); требование participant boundary/numerator/denominator/included fees; «Знаменатели» (287–292) с тремя take-подобными ставками; таблица ledger (303). |
| 4.8 advertiser spend | ✅ COVERED | Раздел «Одна сделка, разные ledgers» (145, 151): spend как начисленная сумма за выбранный состав media/service, вариативность состава в dashboard; ledger-таблица (301) с «чего запись не доказывает» (invoice date, cash date, business return). |
| 4.9 media cost | ✅ COVERED | Строка 152: entity-specific cost — `$100` для advertiser, `$80` downstream для network, «без владельца media cost не определён»; diagram (144–148); ledger-таблица (301–302). |
| 4.10 publisher payout | ✅ COVERED | Строка 153: payout после share/fees/adjustments, payable для SSP / receivable для publisher, признание revenue по policy publisher; statement/invoice-вариант (184); ledger-таблица (304); accrued/billed/settled (159–163). |
| 4.11 gross/net revenue | ✅ COVERED | Раздел «Gross/net revenue и gross margin» (192–238): reporting entity, recognized revenue, gross billings; principal/agent через control над specified good/service, decision sketch (203–209), индикаторы как evidence (211); парная таблица `$100 gross` / `$20 net` (217–220); Magnite/TTD как contract-specific примеры; явное отрицание «до/после расходов» (196, 322). |
| 4.12 gross margin | ✅ COVERED | Формулы `gross profit = recognized revenue − CoR`, `gross margin = … / recognized revenue` (224–227); определение CoR (222); механика `20%` vs `100%` и caveat о прочих CoR и OpEx (229); отличие от take rate (231, 323). |
| 4.13 arbitrage | ✅ COVERED | Раздел «Arbitrage: spread в обмен на принятый риск» (240–256): определение, простой buy/sell вариант `$80/$100`, различие price risk vs volume risk (per-impression vs prepaid batch), basis mismatch CPM→CPC/CPA с зависимостью от CTR/CVR и возможным loss, отличие от прозрачной fee и проблема opacity (с CMA как иллюстрацией механизма). |
| 4.14 заработок посредников на одном долларе | ✅ COVERED | «Арифметика договоров» (273–282): `$20` network + `$12` SSP = `$32` на `$100`, разложение на центы, «не benchmark и не accounting profit»; «Знаменатели» (287–295) с `combined intermediary share = 32%`; ledger-таблица «Экономический остаток» (299–304). |
| 4.15 путь $100 от advertiser до publisher | ✅ COVERED | Раздел «Путь учебных `$100`» (258–315): явные допущения (262–269), арифметика с проверкой суммы (273–279), раздельные event/data flow (169–177) и invoice/cash flow (181–190), ledger-таблица четырёх участников, оговорка о неуниверсальности цепочки (260, 282), чеклист (310–315). |

# Вердикт

`REVISION REQUIRED` — блокеров и содержательных ошибок нет, все 15 требований покрыты, арифметика верна; вердикт определяют только нарушения контракта оформления (важные проблемы 1–4), каждое исправляется заменой одного-двух слов или добавлением сноски.

---

# РОЛЬ 2 — Translation Auditor (RU → EN)

Источник: `chapters/ru/04-adtech-economics-business-models.md`. Перевод: `chapters/en/04-adtech-economics-business-models.md`.

## Структурный паритет (подсчитано скриптом)

| Параметр | RU | EN |
|---|---|---|
| Заголовки (количество и уровни, порядок) | 23 | 23, уровни идентичны |
| Строки таблиц | 39 | 39 |
| Code blocks (количество, язык `text`) | 14 | 14 |
| Абзацы вне таблиц/кода/заголовков | 51 | 51 |
| Маркированные / нумерованные пункты | 24 / 24 | 24 / 24 |
| Сноски `[^g-…]` | 56, 56 уникальных | 56, тот же набор, тот же порядок |
| Ссылки (URL) | 14 | 14, байт в байт |
| Числовые значения (`$`, `%`, объёмы) | 275 | 275, идентичны (расхождения только в прилегающей пунктуации) |
| Front matter | — | отличается ровно в `title` и `language: en` |
| Кириллица в EN | — | не найдена |
| Якоря EN-сносок в `glossary.en.md` | — | все 56 найдены |

Служебные секции EN: `## The Core Idea: …`, `## Common Confusions`, `## What to Remember`, `## Check Yourself`, `## Sources and Further Reading` — соответствуют контракту.

## Смысловая сверка

Проверены все абзацы, таблицы, code blocks и источники. Числа, примеры, ссылки на главы («chapters 15–18»), caveats (учебные числа, «не benchmark», «не accounting advice», «не universal contract»), различение current/historical (CMA 2020, 10-K за 2025) и роли секций сохранены. Терминологическая консистентность: «фактическая метрика/среднее» → `realized metric/average` (73, 75, 80, 83, 311, 319, 338), «представление» → `presentation`, «вывод» → `conclusion`, «граница» → `boundary`, «посредник» → `intermediary` — единообразно. Подписи внутри code blocks («фактические метрики:», «Проверка:») переведены (`realized metrics:`, `Check:`), что соответствует практике перевода русского текста в коде.

## Findings

```text
[MINOR] строка 114 («**Markup** измеряет надбавку к base cost») — EN: "**Markup** measures the markup over the base cost" — тавтология; смысл не искажён, естественнее "measures the uplift (premium) over the base cost".
[MINOR] строка 242 («продаёт дороже») — EN: "sells it dearer" — архаичный оборот; смысл сохранён, естественнее "sells it for more".
```

FAIL-находок нет: пропусков, добавлений, смены чисел/примеров, нарушений front matter, остаточного русского и переименованных якорей не обнаружено.

## Вердикт перевода

`PASS` (2 MINOR, не блокируют).

---

# Приложение. Сверка с §7 предыдущего обзора (`review-2026-10-09/ch04.md`), прочитано после вынесения вердикта

| IMPORTANT из §7 | Состояние |
|---|---|
| 1. Языковой контракт: английские подзаголовки, шапки таблиц, не-терминологическая лексика | **Исправлено в основном**: все `###` и шапки таблиц русские, `Check:`/`Assumptions:` переведены, `remainder`/`evidence`/`score`/`owner`/`named` ушли. **Остаток**: `entity`/`entities` ×4 (194, 222, 306, 323), `boundary` (71, 304) — совпадает с важной проблемой 3 настоящего аудита. |
| 2. 4.5 fixed fee: добавить абзац | **Исправлено** — абзац на строке 130 (retainer, setup/managed-service fee, minimum commitment, flat sponsorship; мотив; риск сторон); sidecar разделён на fixed `$2,000/month` и usage tier (132). |
| 3. Сократить повторы (Confusions/Remember, дублирующая таблица терминов) | **Исправлено** — 6 + 7 пунктов; таблица терминов свёрнута в одно предложение (306). Остаточный повтор `$12/$80` и `$20/$80` в блоке «Знаменатели» — необязательное п. 7. |
| 4. Misleading-места: markup «растёт от», совпадение `20%/20%`, `$0` в net row, batch vs per-impression, направление statement/invoice | **Исправлено** — 114 («измеряет надбавку»), 231 (оговорка о совпадении), 220 + 229 (`$0` объяснён), 252 (per-impression без volume risk vs prepaid batch), 184 (statement SSP → publisher или invoice publisher → SSP по договору). |
| 5. Глоссарий | Вне рамок главы; в `glossary.md` присутствуют `{#g-publisher-payout}`, `{#g-payee-payer}`, `{#g-settlement}` (accrued/billed/settled); отдельной статьи `billable amount` нет — глава определяет его inline (33), сноска не требуется. |

Nice-to-have 6–10 из §7 реализованы (money-label diagram 144–148; причина выбора модели через observability 71; причина net presentation Magnite 235; пояснение «managed network» 31; сноски `inventory`/`ad-opportunity`/`campaign`/`supply`; `g-win-rate` удалён; «фактическая метрика» унифицирована).

# Приложение. Число слов чистой прозы RU

Подсчёт без front matter, таблиц и code blocks; сноски `[^g-…]` исключены из токенов:

- проза до раздела «Источники и дополнительное чтение», без заголовков — **2 582 слова**;
- то же с разделом источников — 2 823;
- с заголовками и источниками — 2 946.
