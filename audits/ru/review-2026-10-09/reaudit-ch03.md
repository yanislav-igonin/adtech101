# Повторный аудит главы 3 «Основные рекламные метрики» — 2026-10-09

Режим: только чтение; файлы главы, плана и глоссария не изменялись. Две роли подряд: Coverage & Accuracy Auditor (RU) и Translation Auditor (RU ↔ EN).

Входы: `master-prompt.md` §10 (строка «#### 3.», 3.1–3.25, с пометками «(определение)» для 3.3, 3.5, 3.11, 3.22, 3.23, 3.24), §7 Stage B «Контракт оформления главы», §3; `plans/ru/03-core-advertising-metrics.plan.md`; `chapters/ru/03-core-advertising-metrics.md`; `chapters/en/03-core-advertising-metrics.md`; `glossary.md`, `glossary.en.md`.

Раскрытие: до вынесения вердикта я не читал `audits/ru/*.audit.md` и `review-2026-10-09/ch03.md`; однако первые 60 строк `review-2026-10-09/00-summary.md` были выведены в терминал при разведке (случайно, вместе с `git log`). Каждый finding ниже независимо проверен grep-ом или пересчётом, а не взят из summary. §7 отчёта `ch03.md` прочитан только после вердикта — см. раздел «Статус IMPORTANT из ревью 2026-10-09».

---

# Роль 1 — Coverage & Accuracy Auditor (RU)

# Резюме аудита

Все 25 требований TOC раскрыты на нужной глубине, фактических ошибок не найдено, центральные flow (opportunity → request → served → rendered → viewable → click → conversion → value; spend → platform → publisher revenue) и все distinctions из §8 master-prompt (CPM vs eCPM, served/rendered/viewable, attribution vs incrementality, spend vs revenue) изложены корректно. Арифметика сквозного примера пересчитана полностью, включая добавленные 80 installs, CPI и две новые CVR, — сходится и внутренне непротиворечива (50% × 30% = 15%). Структура главы соответствует контракту оформления: один H1, `## Суть`, четыре хвостовые секции уровня `##` в нужном порядке, русские заголовки и шапки таблиц, 49 глоссарных сносок — все разрешаются в `glossary.md`, ни одна не дублируется, все стоят при первом упоминании в прозе. Research-даты из учебного текста убраны.

Вердикт `REVISION REQUIRED` вынесен только по контракту оформления (по промпту роли любое нарушение контракта — IMPORTANT и блокирует PASS): отсутствует сноска `[^g-agency]` при трижды употреблённом термине `agency`, и в прозе остались бытовые латинские слова из явного списка §3 (`entity`, `boundary`), плюс `systems`, `activity`. Объём правок — около десяти мест, перевод затрагивает только позиции якорей и несколько слов.

# Блокеры

None.

# Важные проблемы

1. **Термин `agency` без глоссарной сноски.** `glossary.md` содержит статью `Agency {#g-agency}`; в главе слово употреблено три раза — стр. 173 (таблица, «media, agency, sales и onboarding costs»), стр. 179, стр. 208 — и ни разу не снабжено `[^g-agency]`. Контракт: «каждый термин, имеющий статью в glossary.md, получает сноску при первом упоминании». Исправление: `agency[^g-agency]` на стр. 173.
2. **Бытовая латиница из запретного списка §3 в прозе.** Контракт прямо называет `entity` и `boundary` словами, которые пишутся по-русски:
   - `entity`/`entities`: стр. 112 («на reached unique entity»), стр. 304 («определения unique entity»). Стр. 103 («уникальных единиц учёта (unique entities)») — вводящая глосса с русским эквивалентом, допустима; стр. 106–107, 115 — code blocks, не проза.
   - `boundary`/`boundaries` в бытовом значении: стр. 282 («из-за boundary, routing, batching, fan-out и filters»), стр. 309 («разные boundaries и ledgers»). Употребления `ledger boundary` (стр. 175, 183, 271) и `measurement boundary` — установленные термины (есть `{#g-ledger-boundary}`), не нарушение.
   - Прочие бытовые слова той же природы: `systems` (стр. 133 «разные systems могут применить разные filters»), `activity` (стр. 163 «сравнить activity разного размера»), `ledgers` (стр. 309).
   Исправление: «единица учёта», «границ», «системы», «активность/объём», «реестры».

# Необязательные улучшения

1. Стр. 86: «video pod … даёт несколько impressions на одну opportunity» — на уровне протокола каждый слот pod обычно является отдельным `Imp`/impression opportunity (и сама глава на стр. 236 говорит, что GAM выводит opportunities для pods из durations). Уточнить: «один рекламный блок (ad break) на media surface → несколько impressions», чтобы не создать впечатление, что opportunity и slot — синонимы.
2. Стр. 234/238: сноска `[^g-billable-event]` стоит на «billable impression» (стр. 238), тогда как «billing event» впервые встречается в таблице на стр. 234. Формально термин глоссария — `Billable event`; можно перенести сноску на стр. 234.
3. Стр. 175: «CPM-инвентарём» — русская форма термина `Advertising inventory {#g-inventory}`; по букве правила сноска `[^g-inventory]` нужна, но слово употреблено один раз в русском склонении. На усмотрение редактора.
4. Стр. 217/220: «payer»/«payers» в смысле «платящий пользователь» — в глоссарии есть `Payee / payer {#g-payee-payer}` с другим (расчётным) значением из главы 4. Сноска здесь была бы ошибочной; чтобы избежать коллизии при сборке, можно писать «paying user».
5. Стр. 155–157 и далее: `eligible` (clicks, requests, bid requests) используется как квалификатор без определения, тогда как `qualifying` определено на стр. 36. Одна фраза «eligible — допущенные к расчёту по правилу системы» или унификация с `qualifying`.
6. Стр. 238: «В legacy Google Ad Manager reporting встречалась формула …» — vendor-пример без даты, что §3 допускает; но это единственный остаток «истории инструмента» в прозе. Можно перенести в примечание к источнику 7.
7. «С чем это часто путают» (6) и «Что важно запомнить» (7) — суммарно 13 пунктов, в норме (≤ 14); пункты 4 обеих секций (CPM/eCPM) частично дублируют друг друга.
8. Чистая проза — 2 544 слова (без front matter, заголовков, таблиц, code blocks и списка источников; со списком источников — 2 654). Ориентир 2 400 превышен на 6–10 %, не «материально»; при желании сжать — кандидаты стр. 99 (перечисление семейств MRC guidelines) и стр. 236.
9. 3.22: TOC помечает «cohort-анализ — глава 33»; в секции LTV forward reference на главу 33 нет (есть только на главы 4, 25, 32, 34, 37, 48, 49). Одной ссылки достаточно.

# Проверка корректности

Проверено по тексту главы, плану и известным первоисточникам; ошибок не найдено.

| Утверждение | Строка | Статус |
|---|---|---|
| Один `BidRequest` OpenRTB 2.6 содержит один или несколько `Imp` | 71 | Верно |
| MRC Desktop Display: client-side count требует загрузки creative и начала render | 99 | Верно |
| MRC Viewable v2.0: viewable impression ← valid rendered served impression | 99 | Верно |
| Порог 50 % pixels / 1 s display, 2 s video; тот же в Digital Audience-Based Standard 2017; не универсален по форматам | 99 | Верно (с корректным caveat) |
| Reach = de-duplicated unique entities с ≥ 1 qualifying exposure; frequency = impressions / reached entities | 103–115 | Верно |
| Click Measurement Guidelines v1.0 (2009): initiated / measured / received / resolved; browser-centric wording legacy | 133 | Верно |
| Google Ads: CVR на trackable ad interactions; режим `Every` может дать > 100 % | 159 | Верно |
| CPM — buyer cost per mille, eCPM — seller realized revenue per mille; eCPM бывает и на buy side как нормализованный cost | 167–175 | Верно |
| CAC ≠ platform CPA (customer event, cost scope, allocation) | 179 | Верно |
| ROAS = attributed value / ad spend; ROI = net profit / total cost; высокий ROAS совместим с отрицательным ROI | 195–208 | Верно |
| GA4 Data API: ARPU — total revenue (purchase + subscription + ad) на active user; ARPPU — purchase revenue на paying user | 222 | Верно |
| Observed vs predicted LTV; revenue vs contribution LTV; identity/sampling caveat | 224 | Верно |
| GAM sell-through: `Total impressions / Total ad requests`; video pods — через durations | 236 | Верно |
| OpenRTB различает win notice и billing notice; win ≠ billable impression | 238 | Верно |
| Fill rate и win rate — не дополнения до 100 %, разные стадии и владельцы | 228–234 | Верно |
| Advertiser 8 000 = platform 8 000 billable impressions объяснено допущением «DSP только этого advertiser», с оговоркой «в реальности не гарантировано» | 275 | Верно, допущение явное |

Пересчёт арифметики (все числа учебные, валюта USD, период неделя):

| Метрика | Формула в главе | Пересчёт | Статус |
|---|---|---|---|
| CTR | 160 / 8 000 × 100 % | 2,0 % | ✓ |
| CPM | $96 / 8 000 × 1 000 | $12,00 | ✓ |
| CPC | $96 / 160 | $0,60 | ✓ |
| CPI | $96 / 80 | $1,20 | ✓ |
| CVR click → install | 80 / 160 | 50 % | ✓ |
| CVR install → subscription | 24 / 80 | 30 % | ✓ |
| CVR click → subscription | 24 / 160 | 15 % | ✓; цепочка 50 % × 30 % = 15 % согласована |
| CPA (subscription) | $96 / 24 | $4,00 | ✓ |
| ROAS | $480 / $96 | 5,0x = 500 % | ✓ |
| ROI | ($480 − $600) / $600 | −$120 / $600 = −20 % | ✓ |
| Fill rate (publisher) | 80 000 / 100 000 | 80 % | ✓ |
| eCPM (publisher) | $800 / 80 000 × 1 000 | $10,00 | ✓ |
| Bid rate (platform) | 45 000 / 60 000 | 75 % | ✓ |
| Win rate (platform) | 9 000 / 45 000 | 20 % | ✓ |
| Frequency | 60 000 / 20 000 | 3,0 | ✓ |
| ARPU | $1 000 / 1 000 | $1,00 | ✓ |
| ARPPU | $1 000 / 100 | $10,00 | ✓ |
| Таблица классов (стр. 43–45) | 160/8 000; $96/160; $480/$96 | 2 %; $0,60; 5,0x | ✓, совпадает с walkthrough |

Кросс-отчётная согласованность: 8 000 billable impressions ≤ 9 000 wins ≤ 45 000 bids ≤ 60 000 bid requests; 8 000 impressions advertiser ≤ 80 000 impressions publisher; 60 000 platform requests ≠ 100 000 publisher requests — различие объяснено (boundary, routing, batching, fan-out, filters); $12 CPM buyer vs $10 eCPM seller — объяснено двумя причинами (удержания посредников и разный состав impressions) с отсылкой к главе 4. Неявное следствие $480 / 24 = $20 attributed value на подписку — правдоподобно.

# Проверка границ и плотности

- Границы плана соблюдены: роли из главы 2 используются только как measurement perspectives; take rate, gross/net, settlement названы и отданы главе 4 (стр. 193, 271); attribution/lookback window — глава 25; incrementality — глава 34; reconciliation — глава 32; viewability methodology — глава 37; video pod — глава 48; OTT/CTV — глава 49. Экскурсов в auction mechanics, OpenRTB payloads, cohort modeling нет.
- Повторов главы 2 нет; минимальный контекст по ролям оставлен.
- Плотность: 2 544 слова чистой прозы (метод: убраны front matter, заголовки, таблицы, code blocks, список источников; глоссарные маркеры не считались). Превышение ориентира 2 400 — 6 %, не материальное.
- «С чем это часто путают» 6 пунктов + «Что важно запомнить» 7 = 13 (≤ 14); дублирование частичное (см. Необязательные 7).
- Один сквозной пример (subscription app в mobile game) используется во всех секциях; побочных примеров два (reach/frequency, cohort ARPU/ARPPU), оба из плана.

# Проверка контракта оформления

| Пункт контракта | Результат |
|---|---|
| Ровно один H1 | ✓ (стр. 14) |
| Вводная секция `## Суть` | ✓ (стр. 16, подзаголовок через двоеточие допустим) |
| Хвост: `## С чем это часто путают`, `## Что важно запомнить`, `## Проверьте себя`, `## Источники и дополнительное чтение` — уровень и порядок | ✓ (стр. 292, 301, 311, 318) |
| Заголовки секций по-русски, английский только как термин | ✓ (18 заголовков; `Advertiser: outcome и эффективность acquisition` и т. п. — термины) |
| Шапки таблиц по-русски | ✓ (7 таблиц; `contract` в шапках стр. 214/230 — глоссарный термин) |
| Каждая `[^g-id]` разрешается в `{#g-id}` глоссария | ✓ 49/49 |
| Один термин — одна сноска | ✓ (все 49 по одному разу) |
| Сноска при первом упоминании | ✓ для 49 терминов. Автоматические срабатывания «позже первого упоминания» проверены вручную и оказались ложными: стр. 27/31/33/51/52/76–83/106–107 — code blocks; `bid request` (стр. 67) ≠ `bid`; `currency conversion` (стр. 36) ≠ `conversion`; заголовки `###`/`##` (стр. 101, 161, 210, 226) сносок не несут |
| Термины с статьёй в глоссарии имеют сноску | ✗ `agency` ×3 без `[^g-agency]` (IMPORTANT 1). `Programmatic Auction Definitions` (стр. 71) — имя документа; `destination`/`landing page` — только в code block; `payer` — другое понятие (см. Необязательные 4) |
| Бытовая латиница в прозе | ✗ `entity` ×2, `boundary`/`boundaries` ×2, `systems`, `activity`, `ledgers` (IMPORTANT 2). `population`, `owner`, `stage`, `semantics`, `conclusion`, `presentation` — отсутствуют |
| Research-даты и пометки в прозе | ✓ отсутствуют («на дату», «проверено» — только в источниках 6–8). Годы изданий стандартов (2009, 2014/2015, 2017) на стр. 99, 120, 133 — версии документов, не даты проверки |
| YAML front matter | ✓ `id: ch-03`, `chapter: 3`, `toc_requirements` 3.1–3.25 совпадают с TOC, `prerequisites: [ch-01, ch-02]`, `language: ru` |

# Coverage Table

| Requirement | Status | Evidence / Explanation |
|---|---|---|
| 3.1 request и opportunity | ✅ COVERED | Стр. 63–71: определения обоих уровней, пять случаев расхождения (нет request, несколько объектов, fan-out, retries, batch), ссылка на IAB `Ad Request` и `Imp` в OpenRTB 2.6; стр. 73–86 карта measurement points с оговоркой о немонотонности |
| 3.2 impression | ✅ COVERED | Стр. 88: impression как зарегистрированное событие по counting rule системы; «без qualifier не доказывает render, viewability, внимание» |
| 3.3 served/rendered/viewable impression (определение) | ✅ COVERED | Таблица стр. 90–97 (served, rendered, measurable, viewable, non-viewable, non-measurable: свидетельство и чего не доказывает); стр. 99 MRC-критерии с caveat по форматам; методология отдана главе 37 |
| 3.4 reach | ✅ COVERED | Стр. 103–110: count и rate, обязательная единица учёта, universe, identity coverage, пример `20,000 device IDs / persons / households` |
| 3.5 frequency (определение) | ✅ COVERED | Стр. 112–120: формула, пример 60 000 / 20 000 = 3, «среднее, не каждый ровно три раза», условия сравнимости |
| 3.6 click | ✅ COVERED | Стр. 124–133: user-initiated interaction, measurement points measured/received/resolved, причины расхождения, статус Click Guidelines 2009 |
| 3.7 CTR | ✅ COVERED | Стр. 135–141: формула, расчёт 2 %, влияние смены basis, «высокий CTR ≠ качество/conversions/lift» |
| 3.8 conversion | ✅ COVERED | Стр. 143–145: advertiser-defined outcome, несколько conversions с одного click, observed vs attributed, attribution ≠ causality с отсылками к главам 25 и 34 |
| 3.9 CVR | ✅ COVERED | Стр. 147–159: формула с named precursor, таблица трёх переходов, edge case > 100 % (Google Ads `Every`); в walkthrough три CVR с пометками |
| 3.10 CPM | ✅ COVERED | Стр. 167, 175: формула, buyer perspective, pricing basis / rate / bid / observed average; walkthrough $12 |
| 3.11 eCPM (определение; publisher-side realized revenue per mille) | ✅ COVERED | Стр. 168, 175: recognized revenue / impressions × 1 000, seller perspective, сравнение demand с разными pricing, buy-side употребление; walkthrough $10 |
| 3.12 CPC | ✅ COVERED | Стр. 169, 177: формула, bid/target ≠ average; walkthrough $0,60 |
| 3.13 CPA | ✅ COVERED | Стр. 170, 177, 179: формула, action ≠ customer, контраст с CAC; walkthrough $4 |
| 3.14 CPI | ✅ COVERED | Стр. 171, 177: формула, зависимость install count от measurement/attribution; walkthrough `$96 / 80 = $1.20` и CVR click → install 50 % — ранее отсутствовавший шаг install добавлен |
| 3.15 CPL | ✅ COVERED | Стр. 172, 177: формула, lead definition/quality, «lead ещё не customer». Кратко, но для требования-определения достаточно |
| 3.16 CAC | ✅ COVERED | Стр. 173, 179: формула, состав числителя, условия, при которых platform CPA нельзя переименовать в CAC |
| 3.17 revenue | ✅ COVERED | Стр. 183–193: диаграмма смены label по ledger boundary, revenue как признанная участником сумма, состояния estimated/invoiced/settled/recognized |
| 3.18 spend и cost | ✅ COVERED | Стр. 193: spend — расход buyer на media, cost — затраты анализируемого участника (media / downstream / бизнес); gross/net и take rate отданы главе 4 |
| 3.19 ROAS | ✅ COVERED | Стр. 195–201, 208: формула, запись `5.0x`/`500%`, attribution-dependence, walkthrough |
| 3.20 ROI | ✅ COVERED | Стр. 201–208: формула, пример ROAS 5,0x при ROI −20 %, причина расхождения |
| 3.21 ARPU и ARPPU | ✅ COVERED | Стр. 214–222: таблица формул и contract, пример $1 / $10, GA4 как product-specific contract |
| 3.22 LTV (определение) | ✅ COVERED | Стр. 218, 224: observed vs predicted, revenue vs contribution, cohort/horizon/identity/model; cohort-анализ не раскрывается (отдан главе 33, явной ссылки нет — Необязательные 9) |
| 3.23 fill rate (определение и denominators) | ✅ COVERED | Стр. 232, 236: формула, отсутствие единого denominator (responses / impressions / requests / opportunities / ad units), GAM sell-through, video pods, match/response/delivery rate |
| 3.24 win rate (определение) | ✅ COVERED | Стр. 233–238: win rate и bid rate, win notice ≠ billing/delivery, OpenRTB win vs billing notice, датированный пример GAM |
| 3.25 почему одна campaign выглядит по-разному | ✅ COVERED | Стр. 240–290: три согласованных отчёта с расчётами, таблица перспектив, data flow ≠ money flow, семь вопросов, reconciliation → глава 32 |

# Вердикт

`REVISION REQUIRED` — исключительно из-за двух нарушений контракта оформления (сноска `[^g-agency]`; бытовая латиница `entity`, `boundary`, `systems`, `activity`, `ledgers`). Coverage, корректность, арифметика и структура — без замечаний.

## Статус IMPORTANT из ревью 2026-10-09 (`ch03.md` §7, прочитан после вердикта)

| № | Рекомендация | Статус |
|---|---|---|
| 1 | Добавить install в walkthrough (CPI, CVR click → install, install → subscription) | Исправлено: 80 installs, `$1.20 CPI`, 50 % / 30 % / 15 % |
| 2 | Убрать research-даты из prose (стр. 67, 95, 218, 232, 234) | Исправлено: в прозе дат проверки нет; перечень MRC guidelines сжат; история GAM Reports сведена к одной фразе «в legacy … встречалась формула» |
| 3 | Сноски глоссария к первому упоминанию, добавить отсутствующие, убрать `[^g-conversion]` с currency conversion | Исправлено в основном: все 49 сносок при первом упоминании, `[^g-conversion]` перенесена. Остаток: `agency` без сноски (IMPORTANT 1 выше) |
| 4 | Fill rate numerator: неувязка «counted impressions» vs «response может не стать impression» | Исправлено: таблица — `filled responses / eligible ad requests` с пояснением; в walkthrough числитель явно подписан как counted impressions по contract ad server |
| 5 | Добавить `## Суть` | Исправлено (стр. 16) |

Из NICE-TO-HAVE также закрыты: 6 (`qualifying` определено, стр. 36), 7 (объяснение совпадения 8 000, стр. 275), 8 (отсылка $12/$10 → глава 4, стр. 271), 9 (buy-side eCPM, стр. 175), 10 (происхождение порогов, стр. 99), 12 (`population` → «совокупность», шапка «Числитель | Знаменатель»; `entity`/`universe` остались — см. IMPORTANT 2), 13 (13 пунктов вместо 20), 14 (video pod, lookback window, incrementality расшифрованы), 15 («масштаб условный», стр. 242).

---

# Роль 2 — Translation Auditor (RU ↔ EN)

Сравнение `chapters/en/03-core-advertising-metrics.md` с `chapters/ru/03-core-advertising-metrics.md`.

**Полнота и структурный паритет.** Заголовков 18/18 (уровни и порядок совпадают построчно: H1 стр. 14; `##`/`###` на стр. 16, 20, 61, 101, 122, 161, 181, 210, 226, 240, 244, 262, 273, 292, 301, 311, 318). Строк таблиц 43/43, code fences 28/28 (все `text`), маркированных пунктов 11/11, нумерованных 19/19, ссылок 15/15, непустых строк 234/234. Служебные секции EN названы `## The Core Idea`, `## Common Confusions`, `## What to Remember`, `## Check Yourself`, `## Sources and Further Reading` — по контракту.

**Якоря.** Мультимножество `[^g-…]` идентично: 49 идентификаторов, каждый ровно один раз в обоих файлах; `diff` пуст; переименований и добавлений нет.

**Front matter.** Отличается ровно в `title` («Основные рекламные метрики» → «Core Advertising Metrics») и `language: ru → en`; `id`, `chapter`, `slug`, `toc_requirements`, `prerequisites`, `status` совпадают.

**Русский в EN.** Кириллицы в теле нет (grep по диапазону U+0400–U+04FF — 0 совпадений).

**Точность.** Все числа, формулы, комментарии в code blocks (`# click → install`, `# числитель — counted impressions …` → `# numerator — counted impressions …`), URL и даты в источниках («24 июня 2026 года» → «June 24, 2026»; «проверено 27 августа 2026 года» → «checked August 27, 2026») перенесены без изменений. Различия current/legacy (Click Guidelines 2009, legacy GAM reporting), universal/product-specific (GA4, GAM) и статус caveat сохранены. Добавлений и сокращений не обнаружено.

## Findings

```text
[MINOR] стр. 193 — RU «**Revenue** — выручка, признанная выбранным участником…» → EN «**Revenue** is the proceeds recognized by the chosen participant…». Слово `proceeds` — отдельный глоссарный термин `{#g-proceeds}`, в EN главе 4 используемый в ином значении (сумма до распределения). glossary.en.md определяет Revenue как «the amount recognized…». Рекомендуется «the amount (revenue) recognized by the chosen participant».
[MINOR] стр. 118, 208, 220 vs 242, 275 — RU «учебный» (5 употреблений) передано двумя словами: `textbook` (118 «A textbook example», 208 «textbook walkthrough», 220 «A textbook subscription cohort») и `instructional` (242 «instructional», 275 «instructional example»). Унифицировать (например, `illustrative` или `textbook`).
[MINOR] стр. 135 — RU «долю выбранных impressions, после которых зарегистрированы выбранные clicks» → EN «the share of the counted impressions after which the counted clicks were registered». «Выбранных» (selected/chosen) передано как `counted`; смысл сохранён, но утрачен оттенок «выбранная по contract совокупность». Вариант: «the share of the selected impressions … the selected clicks».
```

## Вердикт

`PASS` — FAIL findings отсутствуют; три MINOR не блокируют.

---

# Сводка

- Роль 1: `REVISION REQUIRED` (контракт оформления): IMPORTANT 1 — `agency` ×3 без `[^g-agency]`; IMPORTANT 2 — бытовая латиница `entity` (112, 304), `boundary`/`boundaries` (282, 309), `systems` (133), `activity` (163), `ledgers` (309). Блокеров нет; 25/25 требований COVERED; арифметика walkthrough (включая 80 installs, CPI $1.20, CVR 50 % / 30 % / 15 %) сходится.
- Роль 2: `PASS`; MINOR — `proceeds` вместо revenue (193); `textbook`/`instructional` для «учебный»; `counted` вместо «выбранных» (135).
- Чистая проза RU: 2 544 слова (без front matter, заголовков, таблиц, code blocks и списка источников; со списком источников — 2 654).
