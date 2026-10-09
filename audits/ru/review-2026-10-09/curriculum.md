# Ревью учебного плана AdTech 101 (TOC §10 + планы глав 1–6)

Дата ревью: 2026-10-09. Режим: только чтение. Проверено: `master-prompt.md` (§1–5, §8, §10, §11), `README-adtech.md`, `agents/planner-researcher.md`, шесть `plans/ru/*.plan.md`, заголовки и front matter `chapters/ru/*.md`, якоря `glossary.md`, выводы `audits/ru/*.audit.md` в части дублирования.

Условные обозначения: `N.N` — пункт TOC из `master-prompt.md` §10; `planNN:LINE` — файл `plans/ru/NN-*.plan.md`, строка.

---

## Резюме

1. Макро-последовательность `market → campaign → programmatic → tracking → attribution → MMP → analytics → fraud/privacy → engineering → products/business` для инженера корректна. Forward references в главах 3 и 6 (fill/win rate до auction, third-party audiences до identity/privacy) — контролируемые навигационные упоминания: планы явно ограничивают глубину и отсылают дальше, аудиты это подтверждают. Реальные дефекты порядка в другом: глава 9 (affiliate) требует tracking-механики глав 21–23; главы 12–13 опираются на auction basics главы 18; 7.15 требует first/second price из 18.6–18.8.
2. В TOC есть настоящее дублирование, а не только послойность: `31.1–31.4 ↔ 45.1–45.4` (почти дословно), `2.17 ↔ 16.13`, `8.4–8.8 ↔ 26.5–26.8`, `28.18–28.20 ↔ 54.5–54.6`, `10.4 ↔ 11.8`, `46 ↔ 48` (retries/duplicates/reconciliation), `16.1–16.4 ↔ 2.6–2.9`. Для уже спланированных повторов (CPM/CPC/CPA 3↔4, bid strategy 5.9↔7.13, placement 1/5/6) послойность реализована и зафиксирована в планах.
3. Пропуски относительно §2: walled gardens / SAN как модель покупки и измерения (только 26.14–26.15), search advertising как отдельный рынок (только 8.9), cookie sync / ID matching (нет ни в 19, ни в 24) — без них цели §2.7 и §2.13 выполняются не полностью. Остальные кандидаты — в приложения или как примеры внутри существующих глав.
4. Планы 1–6 между собой согласованы по «уже ожидается / вводится здесь» с четырьмя оговорками: термин `bid`/`auction` используется с главы 3 как известный и не вводится ни одним планом до 7.1/18.1; `ad opportunity`, `impression`, `campaign`, `creative`, `placement` формально «вводятся» дважды (план 1 и планы 3/5) — это уточнение, но помечено как введение; план 3 внутри себя противоречит сам себе про номер главы reconciliation (32 vs 35); ссылки «главы 10 и 14» для yield/mediation/header bidding неверны (это 12–13).
5. Планы единообразны по формату; самый слабый — план 1 (меньше примеров и источников, нет glossary-шага), самый сильный по формату — план 6 (glossary anchors, таблица current/legacy); план 3 самый глубокий, но с наибольшим числом внутренних ошибок.
6. Написанные главы уже 2.9–4.1k слов при 10–25 пунктах, то есть на верхней границе «5–15 минут». Главы 9 (25), 19 (24), 28 (23), 36 (23) при той же плотности выйдут за норму; глава 54 (10 компаний × 10-вопросный framework) рискует стать самой длинной в книге.

---

## A. Логика порядка глав и частей

### A.1. Макро-порядок — корректен

Последовательность частей I–XIII выстроена от «что покупается и кто кому платит» к «как это реализовано» и завершается синтезом. Для software engineer это правильный порядок: сначала domain model (главы 1–4), затем конфигурация со стороны advertiser (5–8), затем supply side (10–14), затем протокол сделки (15–20), затем measurement как обратная связь (21–35), затем «что ломается» (36–43), затем инфраструктура (44–48) и карта рынка (52–55). Главы 30–31 (data model, pipelines) стоят до главы 32 (discrepancies), что верно: читатель сначала видит event model, потом причины расхождений.

### A.2. Forward references в главах 3 и 6 — допустимы и контролируются планами

- **3.23 fill rate, 3.24 win rate до 10/18.** `plan03:33` ограничивает scope словами «их разные stages и product-specific denominators»; `plan03:42` явно откладывает «способы увеличения fill/eCPM» в publisher-главы; раздел 7 плана (`plan03:206–222`) даёт только формулы, denominators и edge cases. Аудит `audits/ru/03:29` подтверждает, что глава осталась в границах. Вердикт: навигационное определение, не дефект. Но в самом TOC это не отражено — пункт `3.23 fill rate` и `10.8 fill rate` сформулированы одинаково, и будущий Planner главы 10 не увидит, что определение уже дано.
- **6.11 third-party audiences, 6.12 retargeting до 24/40.** `plan06:61–66` откладывает cookies/device IDs/identity resolution в главу 24, privacy — в 40, CMP — в 41, мир без third-party identity — в 42, и формулирует правило «match обозначается как необходимая activation boundary без объяснения механизма». Таблица current/legacy (`plan06:85–94`) предотвращает устаревшие утверждения о Chrome/Privacy Sandbox. Вердикт: навигационное упоминание, корректно.
- Общая рекомендация: пометить в TOC пункты-«первые определения» (3.11 eCPM, 3.23 fill rate, 3.24 win rate, 5.9 bid strategy, 6.9 placement) словом «определение» и указать главу углубления, чтобы Planner поздних глав не переопределял термин.

### A.3. Реальные дефекты порядка

1. **Глава 9 (Performance и Affiliate Marketing) раньше части V.** Пункты `9.13 tracking link`, `9.14 click ID`, `9.15 subID`, `9.16 S2S postback`, `9.17 smartlink`, `9.18 deep link` — это механика, которую курс обещает «на уровне конкретных HTTP/event flows» (§2.5) только в главах 21–23 (`21.8 S2S tracking`, `21.10 postback`, `22.6 click ID`, `22.10 sub IDs`, `22.4–22.5 redirect`) и `28.14 deep linking`. Если глава 9 объяснит их по-настоящему — она продублирует 21–22; если не объяснит — шесть пунктов станут голословными labels. Это hard forward dependency на шесть пунктов. Варианты: (a) перенести главу 9 в часть XI «Отдельные экосистемы» после tracking (affiliate — такая же отдельная экосистема, как CTV и retail media); (b) оставить место, но переформулировать 9.13–9.18 как «роль в affiliate flow; механика — главы 21–23».
2. **Главы 12–13 (waterfall/mediation/header bidding) раньше главы 18 (RTB auction).** `12.12 переход к parallel auctions`, `13.3 parallel auction`, `13.14 winning bid в ad server`, `13.12 price buckets`, `13.17 yield vs latency` предполагают знание того, что такое auction, bid, clearing price (`18.1`, `18.4`, `18.6–18.8`). Читатель к главе 12 знает auction только из навигационных упоминаний главы 3 (bid rate / win rate). Варианты: вставить в главу 12 абзац-primer «что такое auction и bid для целей этой главы» (с явным deferral в 18) или переставить части III и IV местами частично: 15–18 перед 12–14. Второй вариант ломает логику «сначала publisher side, потом programmatic», поэтому предпочтителен primer.
3. **7.15 max bid vs actual price** требует first-price/second-price (`18.6–18.8`). Рекомендация: ограничить формулировку 7.15 до «actual price ≤ bid; почему — глава 18».
4. **Пайплайны разнесены между частью VII (глава 31) и частью X (главы 44–48).** Это не ошибка порядка сама по себе, но корень самого сильного дублирования в TOC (см. B.1). Нужно одно место для «как устроен pipeline» и одно для «что в нём ломается».
5. **Коллизии терминов, одинаковых по label и разных по смыслу:** `2.5 media buyer` (функция внутри advertiser/agency) vs `9.6 media buyer` (affiliate, покупающий трафик за свой счёт); `22.8 publisher ID` (параметр tracking URL) vs `42.4 publisher IDs` (first-party identity publisher-а). Планы 2 и будущие 9/22/42 должны явно разводить эти смыслы; сейчас в TOC они выглядят как повтор одного понятия.

---

## B. Дублирование внутри TOC

### B.1. Повторы, не названные в задании, но видные из TOC

| Пункты | Вердикт | Комментарий |
|---|---|---|
| `31.1 ingestion, 31.2 streaming, 31.3 queue/broker, 31.4 consumer, 31.8 aggregation, 31.10 realtime reporting` ↔ `45.1 ingestion, 45.2 streams, 45.3 queues, 45.4 consumers, 45.6 aggregation, 45.7 realtime analytics` | **дублирование** | Почти дословный повтор. Усугубляется тем, что аудитория по §1 уже знает queues/Kafka/stream processing, то есть оба списка малоценны сами по себе; ценность — только AdTech-specific delta (объёмы, cardinality, serving vs analytics path, billing-grade). |
| `2.17 совмещение ролей внутри одной компании` ↔ `16.13 совмещение ролей` | **дублирование** | Один и тот же пункт. План 2 раскрывает его полностью (`plan02:142–148`: причины, benefits, risks, упражнение). |
| `8.4 display/banner, 8.5 native, 8.6 video, 8.7 interstitial, 8.8 rewarded video` ↔ `26.5 banner, 26.6 interstitial, 26.7 rewarded, 26.8 native` | **дублирование** | Список форматов повторён в mobile-главе без mobile-specific delta в формулировке. |
| `28.18 AppsFlyer, 28.19 Adjust, 28.20 Singular` ↔ `54.5 AppsFlyer — MMP, 54.6 Adjust — MMP` | **дублирование** | Vendor profiles дважды; в 54 к тому же единый framework из 10 вопросов, который в 28 будет пересказан. |
| `3.16 CAC, 3.21 ARPU и ARPPU, 3.22 LTV` ↔ `33.9 ARPU, 33.10 ARPPU, 33.11 LTV, 33.12 CAC` | **послойно, но не разграничено в TOC** | `plan03:32, 199–204` уже даёт формулы, denominators, cohort/horizon caveats. Глава 33 должна быть про cohort-over-time, payback и качество acquired users, а не переопределять термины. |
| `32.20 reconciliation` ↔ `47.9 reconciliation` ↔ `48.4 reconciliation advertiser/publisher` ↔ `48.9 correction/backfill` ↔ `31.15 backfill, 31.16 reprocessing` | **частично дублирование** | Четыре места для reconciliation плюс backfill дважды. Нужно разграничить: 32 — «почему не сходится», 47 — «realtime counter vs ledger», 48 — «процесс сверки и исправления». 31.15–31.16 и 48.9 — одно и то же. |
| `28.10 conversion values` ↔ `29.8 conversion values` | **дублирование** | Conversion value — концепт SKAdNetwork/AdAttributionKit; место — 29. В 28 достаточно «MMP управляет conversion value mapping — см. 29». |
| `7.8 pacing` ↔ `20.14 pacing` ↔ `47.1 pacing counters`; `7.11 budget allocation` ↔ `20.15 budget allocation` | **послойно** | 7 — что это с точки зрения advertiser; 20 — как DSP это считает; 47 — где хранится state. Разграничение разумное, но в TOC не подписано. |
| `3.11 eCPM` ↔ `10.9 eCPM` ↔ `12.3 historical eCPM` ↔ `20.10 eCPM` | **послойно, с риском** | Три разных смысла: publisher realized revenue (3/10), historical estimate для ranking (12), DSP expected eCPM как bid-нормализация (20). Это полезное различие, если каждая глава назовёт свой смысл; иначе читатель получит три «определения eCPM». |
| `29.1 ATT` ↔ `40.10 ATT`; `29.3 IDFA availability` ↔ `40.11 mobile identifiers` ↔ `24.6 IDFA` | **послойно** | 24 — что за identifier; 29 — последствия для attribution; 40 — как privacy-ограничение. Нормально, если 40 не пересказывает 29. |
| `13.10 bid timeout` ↔ `18.13 timeouts` ↔ `32.5 timeouts` ↔ `46.7 timeout handling` | **послойно** | header bidding / auction / discrepancy / reliability — четыре разных вопроса, но на одном слове. |
| `23.19 late conversions` ↔ `32.15 late events` ↔ `46.6 late events` | **послойно** | Допустимо при разграничении: 23 — attribution window, 32 — почему отчёты меняются задним числом, 46 — event-time vs processing-time в системе. |
| `12.6 mobile mediation, 12.7 mediation platform, 12.8 ad network mediation` ↔ `26.10 mediation` | **дублирование** | Три пункта о mediation в 12, затем ещё один в 26 без delta. |
| `3.5 frequency` ↔ `7.10 frequency cap` ↔ `11.12 frequency capping` ↔ `47.3 frequency caps` ↔ `42.9 frequency/campaign measurement limits` | **послойно** | Метрика / настройка advertiser / правило ad server / realtime state / ограничение без identity — пять ракурсов. Нужна подпись ракурса в TOC. |
| `49.x video` ↔ `8.6 video, 8.12 CTV` ↔ `50.x CTV` | **частично** | 8.12 CTV как формат и целая глава 50 — нормально; но 49 (VAST, quartiles) и 50 (SSAI, pods) частично пересекаются по «video auction flow» (49.8) и «CTV supply chain» (50.8). |

### B.2. Повторы из задания — проверка по планам

| TOC-пункт | Главы | Вердикт | Как разграничить |
|---|---|---|---|
| `placement` | 1 (термин), 5.5, 6.9, 8.3, 10.4, 11.8 | **послойно для 1/5/6; дублирование для 10.4 ↔ 11.8** | `plan01:65` вводит минимально; `plan05:25` — как поле конфигурации («где показывать»), с явным deferral формата в 8; `plan06:33` — как targeting axis «где допускается показ»; `glossary.md:80` фиксирует overload publisher-side / buy-side. 8.3 — формат/ad unit compatibility. Но 10.4 и 11.8 оба publisher-side (`placement` vs `placement/ad unit`); один из них убрать или переформулировать 11.8 как «маппинг placement → ad unit в ad server». |
| `CPM/CPC/CPA` | 3.10–3.15, 4.1–4.3 | **послойно, реализовано** | `plan04:21`: «Формулы из главы 3 не переобъясняются; здесь важны trigger, payer/payee, validation, риск». `plan04:34` в OUT OF SCOPE прямо запрещает повтор. Аудит `audits/ru/04:36` подтверждает. Хорошо бы отразить в TOC: «4.1 CPM как contractual basis и risk allocation». |
| `bid strategy` | 5.9, 7.13 | **послойно, реализовано** | `plan05:40`: «только как выбранная политика… Алгоритмы, auction mechanics и pacing — глава 7»; `glossary.md:518` отделяет strategy / target / actual bid / billable price. Глава 7 должна раскрыть семейство стратегий и их математику, не переопределяя термин. |
| `кто кому платит` / money flow | 1.6, 2.16, 4.8–4.15, 16.11 | **послойно для 1/2/4; 16.11 — риск** | `plan01:24`: «только направление денег»; `plan02:26`: «только направление и тип оплаты»; `plan04` — ledgers, gross/net, `$100`. 16.11 money flow после всего этого должен быть только про auction-specific money path (clearing price → fees → publisher), иначе это четвёртый пересказ. |
| `fill rate`, `eCPM` | 3.11, 3.23, 10.8, 10.9 | **послойно, но TOC не подписан** | `plan03:42` явно откладывает стратегию fill/eCPM в 10 и «14» (ошибочно — см. D). Глава 10 должна строить yield из уже определённых метрик. Рекомендация: 10.8 → «fill rate как управляемый показатель», 10.9 → «eCPM как инструмент сравнения demand». |
| `frequency cap` | 7.10, 11.12, 47.3 | **послойно** | 7 — настройка advertiser; 11 — правило delivery в ad server; 47 — счётчик и его consistency. См. B.1. |
| `DSP/SSP/exchange/ad network` | 2.6–2.9, 16.1–16.4, 16.13–16.15 | **частично дублирование** | `plan02:30` обещает «рабочие distinctions» и откладывает глубокие сравнения в 16. Но `16.1 DSP; 16.2 SSP; 16.3 exchange; 16.4 ad network` как голые labels провоцируют повторное определение; `16.13 совмещение ролей` = `2.17`. Содержательно новыми в 16 являются 16.5–16.12 (что продаёт SSP, что покупает DSP, функция exchange, aggregation, money/data flow) и 16.14–16.15 (глубокие сравнения). Рекомендация: убрать 16.1–16.4 и 16.13, оставить 16.5–16.12, 16.14–16.15. |
| `viewability` | 3.3, 17.14, 37.2–37.3 | **послойно** | `plan03:27, 48` даёт лестницу served/rendered/measurable/viewable и датированные MRC thresholds, откладывая OMID/attention в 37. 17.14 — место в flow одного impression; 37 — методология и vendors. Разграничено корректно, в TOC не подписано. |
| `retries/duplicates/idempotency` | 23.17–23.18, 32.6–32.8, 46.1–46.3, 48.2–48.3 | **46 ↔ 48 дублирование; остальное послойно** | 23 — dedup conversions на уровне tracking contract; 32 — как это создаёт discrepancy. 46.1–46.3 и 48.2–48.3 оба про «retries → duplicates → что делать», разница только в слове idempotency. Рекомендация: 46 = runtime/serving reliability (retries, idempotency, ordering, partial failure), 48 = offline data correctness (schemas, contracts, lineage, anomalies, reconciliation). Убрать 48.2–48.3 либо переформулировать как «обнаружение missing/duplicate в данных». |
| `ingestion/streams/queues` | 31.1–31.4, 45.1–45.4 | **дублирование** | См. B.1. Варианты: (a) 31 — logical pipeline для reporting (что считаем, где агрегируем, retention/backfill), 45 — architecture и failure modes; тогда из 45 убрать 45.1–45.4, 45.6, оставить 45.5 batching, 45.8 serving vs analytics paths, 45.9 backpressure, 45.10 typical architecture; (b) слить 45 в 31 и оставить в части X только 44, 46–48. |
| `MMP vs product analytics` | 28.21, 33.17 | **послойно** | 28 — с позиции MMP (что он не делает); 33 — с позиции analytics (чем advertising analytics отличается от product analytics). Допустимо; `plan02:111, 165` уже ввёл misconception, так что к 28 это будет третье упоминание — в 28 достаточно одной таблицы. |
| `identity providers` | 2.15, 24.x, 42.5 | **послойно** | `plan02:82` — роль; 24 — механика matching; 42.5 — как альтернатива third-party cookies. 42.6–42.7 (deterministic/probabilistic identity) повторяют 24.14–24.15 — там нужно явно «те же методы в условиях без третьесторонних ID», иначе дублирование. |

---

## C. Пропуски в TOC

Оценка относительно целей §2 (особенно §2.7 OpenRTB без магии, §2.11 data infrastructure, §2.13 «за 10 минут понять любую компанию»).

### C.1. В основной курс (IMPORTANT)

1. **Walled gardens / Self-Attributing Networks как отдельная модель покупки и измерения.** В TOC есть только `26.14 SAN; 26.15 non-SAN` в контексте mobile. Между тем Meta/Google/TikTok/Apple Search Ads — это (а) другой способ покупки (нет OpenRTB, нет SSP, closed auction), (б) другой способ измерения (platform self-reporting, claim conversions — связано с `25.17 why platforms claim the same conversion`), (в) главная интеграция MMP (`28.8 network integrations`). Планы 5–6 уже используют Google Ads и Meta как основные примеры (`plan05:63–74`, `plan06:75–83`), то есть курс де-факто учит на walled gardens, но нигде не объясняет, чем они структурно отличаются от open programmatic. Без этого §2.13 не выполняется: читатель не сможет поместить Meta Ads или Google Ads в value chain. Рекомендация: отдельный раздел в главе 15 («programmatic open web vs closed platforms») или новая глава в части IV/VI; 26.14–26.15 ссылаются на неё.
2. **Search advertising / keyword auction как рынок.** Только `8.9 search` (формат) и `6.8 keyword` (targeting). Поисковая реклама — крупнейший сегмент по spend, с собственной моделью auction (quality score, ad rank), без publisher-side в классическом смысле. Достаточно одного раздела внутри новой главы о walled gardens (п. 1) или в 15, с явным «это не RTB и не programmatic в смысле части IV».
3. **Cookie sync / user ID matching между SSP и DSP (buyeruid, match tables).** Отсутствует и в 19 (OpenRTB `user` object — 19.11), и в 24 (identity). Без этого «OpenRTB flow без магии» (§2.7) невозможен: читатель не поймёт, откуда DSP знает пользователя в bid request и почему retargeting работает в open web. Рекомендация: добавить `24.x cookie sync / ID matching между платформами` и упомянуть в 19.11.

### C.2. Как подразделы существующих глав (NICE-TO-HAVE)

- **Server-side conversion tracking / Conversions API (CAPI-like) и дедупликация pixel ↔ server** — встраивается в главу 23 (`23.9 browser pixel`, `23.12 S2S`, `23.17 deduplication`); добавить формулировку «browser + server dual tracking и event dedup».
- **UTM / web analytics vs ad tracking** — как пример в `22.12 dynamic parameters` и как distinction в `33.17 product vs advertising analytics`.
- **GA4 / first-party analytics tools** — как пример в 33; план 3 уже цитирует GA4 определения ARPU/LTV (`plan03:69–70`), то есть инструмент фактически присутствует.
- **GPC (Global Privacy Control), Do Not Track как legacy** — в 41 (`41.3 consent signal`, `41.8 GPP`); DNT упомянуть как deprecated.
- **Apple Search Ads attribution (AdServices)** — в 27/29 рядом с `27.10 referrer` и `29.5 SKAdNetwork`; это третий canonical mobile attribution source и важный пример SAN.
- **Creative approval/policy** — `8.15 approval` есть; достаточно.
- **Deals/PMP** — глава 14 покрывает.

### C.3. В приложения или Advanced track

- **DOOH, audio, in-game** — исключение из основного курса оправдано; одна строка в приложении D или в главе 52.6 как «другие vertical ecosystems». Отсутствие не мешает целям §2.
- **Privacy Sandbox internals, Protected Audience** — план 6 уже фиксирует retirement (`plan06:94`), Advanced.
- **Ads data hub / clean room internals, PET** — Advanced (как и заявлено в README).

---

## D. Согласованность планов между собой

### D.1. Цепочка «вводится здесь → уже ожидается»

| Переход | Результат |
|---|---|
| План 1 → план 2 | Согласованы. План 2 (`plan02:55–61`) ожидает ровно то, что план 1 ввёл (`plan01:58–75`). Одна неточность: `plan02:58` «если `creative` используется в главе, дать короткое явное определение» — но `plan01:68` уже ввёл creative; планировщик 2 не был уверен в состоянии course state. |
| План 2 → план 3 | Согласованы. `plan03:80–83` ожидает роли из 2 и «attribution на уровне идеи» — `plan02:76, 164` ввёл attribution provider и caveat «attribution ≠ causality». |
| План 3 → план 4 | Согласованы по метрикам (`plan04:70`). Оговорка: `plan04:69` ожидает «billable на уровне разных event points» из главы 3, но план 3 использует billable только в research/edge cases (`plan03:55, 220, 238`), не в «Вводится здесь». Нестрого, но план 4 сам вводит `billable event` (`plan04:76`), так что пробела для читателя нет. |
| План 4 → план 5 | Согласованы по pricing basis / billable event / optimization target (`plan05:84`). Но `plan05:84` включает в «уже ожидается» слово **`bid`** — см. D.2. |
| План 5 → план 6 | Согласованы полностью, с glossary anchors (`plan06:102–109`); все 25 якорей, на которые ссылается план 6 как на существующие, присутствуют в `glossary.md`; все 9 новых якорей (`plan06:115–123`) добавлены Author-ом. |

### D.2. Термины, которые все считают введёнными, но никто не вводит

- **`bid` и `auction`.** Используются как известные с главы 3 (`plan03:16` «response / bid / win», `plan03:113` bid rate/win rate), главы 4 (`plan04:50, 76` «auction win сам по себе не обязан быть billable event»), главы 5 (`plan05:84` «bid … — глава 4», хотя план 4 не вводит bid; `plan05:100` bid strategy определяется через «auction bids»), главы 6 (`plan06:58`). Формальное введение — только `7.1 bid` и `18.1 auction basics`. В glossary нет `g-bid` и `g-auction`. Для инженера слова интуитивны, поэтому это не блокер, но это тот самый случай «каждый план считает введённым, ни один не вводит». Рекомендация: добавить в glossary `g-bid`, `g-auction` с минимальным определением и сноску при первом использовании в главе 3 (или одну строку в `plan03` «Вводится здесь»).
- **Зеркальный случай — термины, попавшие в glossary без плана.** `glossary.md` содержит `g-rtb`, `g-programmatic` (первое использование — глава 1) и `g-pacing` (глава 5), но ни один план не перечисляет их в «Вводится здесь»: `plan01:27` лишь разрешает RTB «как один пример», `plan05:164` лишь откладывает pacing в главу 7. Это статьи, добавленные Author-ом вне планового набора терминов. Не ошибка по существу (определения корректны и осторожны), но Stage A п. 10 (сверка с glossary) выполняется только с главы 6; для глав 1–5 планы и glossary расходятся.
- **Invoice, accounts receivable/payable, accrual, ledger** — `plan04:71` относит их к «общим engineering/accounting-adjacent concepts». По §1 бизнес-понятия объясняются с нуля; для software engineer AR/AP и accrual не являются «известными». Рекомендация: минимальная сноска или одна строка в главе 4 (аудит главы 4 не отметил, но это нарушение §1 на уровне плана).

### D.3. Термины, вводимые дважды

Формально помечены как «Вводится здесь» в двух планах:

- `ad opportunity`: `plan01:66` и `plan03:90`;
- `impression`: `plan01:67` и `plan03:92`;
- `campaign`: `plan01:69` и `plan05:91`;
- `creative`: `plan01:68` и `plan05:94`;
- `placement`: `plan01:65` и `plan05:95`;
- `revenue/spend/cost`: `plan01:74` (media spend, fee, publisher revenue) и `plan03:107`, затем `plan04:86–88` (advertiser spend, media cost, publisher payout).

Во всех случаях это осознанное уточнение (план 1 оговаривает «точные границы отложены», план 5 — «ранее встречавшиеся слова без формальной configuration semantics»), и glossary содержит по одной статье на термин. Проблема только в маркировке: формат Planner Brief имеет две категории («уже ожидается» / «вводится здесь»), а нужна третья — **«уточняется здесь»** (термин известен, глава добавляет слой). Рекомендация: добавить её в `agents/planner-researcher.md` Required Output Format и в §7 Stage A master-prompt.

### D.4. Ссылки «отложено в главу N» — сверка с TOC

| Ссылка в плане | Что говорит TOC | Вердикт |
|---|---|---|
| `plan01:26` «fill и yield — главы 10 и 14» | fill — 10.8, 12.5; yield — 10.10, 12.9; глава 14 — способы продажи inventory | Частично неверно: должно быть «10 и 12». |
| `plan02:28` «yield, fill, direct/indirect monetization и способы продажи — главы 10 и 14» | yield management — 12.9 | Неполно: пропущена 12. |
| `plan03:42` «yield strategy, mediation, header bidding и способы увеличения fill/eCPM — главы 10 и 14» | mediation — 12, header bidding — 13 | **Неверно**: должно быть «10, 12–14». |
| `plan03:47` «discrepancy taxonomy и reconciliation — глава 32» | 32.20 reconciliation | Верно. |
| `plan03:73` «До chapter 35 достаточно научить задавать семь вопросов» и `plan03:240` «detailed reconciliation — глава 35» | глава 35 — Experimentation; reconciliation — 32 | **Неверно и противоречит `plan03:47` внутри того же плана.** В текст главы ошибка не попала: `chapters/ru/03-core-advertising-metrics.md:283` говорит «Детальная reconciliation относится к главе 32». Дефект только в плане. |
| `plan03:46` «analytics stack, cohort modeling, retention/churn, predictive LTV — главы 30–34» | 33 | Верно (диапазон). |
| `plan01:27`, `plan03:44` «главы 15–20» programmatic/RTB/OpenRTB/DSP | 15–20 | Верно. |
| `plan01:28`, `plan03:45` «главы 21–29» tracking/identity/attribution/MMP/privacy | 21–29 | Верно. |
| `plan01:30` «главы 36–43» fraud/transparency/privacy/consent | 36–43 | Верно. |
| `plan01:38` sellers.json/schain — глава 38 | 38.8, 38.11 | Верно. |
| `plan02:29` ad-serving internals — 11; `plan02:30` «15–20, особенно 16»; `plan02:31` «21–25»; `plan02:32` «27–29, особенно 28»; `plan02:33` «36–37, особенно 37»; `plan02:34` «40–42»; `plan02:35` «52–54» | — | Все верно. |
| `plan04:35–45` 5, 9, 10, 14, 16, 18–20, 31, 32, 48, 38–39 | — | Все верно. |
| `plan05` 6, 7, 8 | — | Верно. |
| `plan06` 7, 8, 20, 24, 40, 41, 42, 43, 40–42 | — | Верно. |

Итого три ошибочные ссылки, все в планах 1–3 и все вокруг части III (главы 10–14): планировщики не различали 10 (monetization), 12 (mediation/yield), 13 (header bidding), 14 (sales methods).

### D.5. Структурная несогласованность написанных глав (замечено по заголовкам)

- `chapters/ru/05-campaign-structure.md:395` и `chapters/ru/06-targeting-audiences.md:328` — `# Sources and Further Reading` (H1, английский), тогда как главы 1–4 имеют `## Источники и дополнительное чтение`. README-adtech.md прямо требует `##`, чтобы раздел не стал отдельной EPUB-главой; master-prompt §3 требует русский язык материалов.
- В главе 5 разделы «С чем это часто путают», «Что важно запомнить», «Проверьте себя» — `###` (`05:360, 375, 388`), в остальных главах — `##`. В главе 6 «С чем это путают» (без «часто»). Мелочи, но они ломают структурный паритет, который Stage T (translation auditor) проверяет байт в байт.

---

## E. Качество самих планов

| Критерий | План 1 | План 2 | План 3 | План 4 | План 5 | План 6 |
|---|---|---|---|---|---|---|
| Строк | 162 | 207 | 315 | 290 | 262 | 316 |
| Формат (10 обязательных секций) | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| Coverage Matrix: по одной строке на пункт, конкретный treatment | ✓ 10/10 | ✓ 17/17 | ✓ 25/25 | ✓ 15/15 | ✓ 14/14 | ✓ 17/17 |
| Research findings с датой и источниками | 10 пунктов, 6 источников | 11, 8 | 21, 14 | 13, 9 | 13, 10 | 16, 13 |
| Current vs legacy различение | в одном пункте | есть | датированные MRC/Google примечания | датированные 10-K | есть | **отдельная таблица** (`plan06:85–94`) |
| Misconceptions | 7 | 15 | 17 | 16 | 15 | 18 |
| Конкретные примеры | 2 | 3 | 3 (с согласованными числами) | 3 (единый `$100`) | 3 | 3 |
| Subscription app как сквозной пример | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| Glossary-шаг (Stage A, п. 10) | нет | нет | нет | нет | нет | **да** (`plan06:102–125`, anchors) |
| Внутренние ошибки ссылок | 1 (гл. 14) | 0–1 (гл. 12 пропущена) | 2 (гл. 14; 35↔32) | 0 | 0 | 0 |
| Язык | русский | русский | «chapter 4/35» в русском тексте (`plan03:73, 240`) | русский | «chapter 6/7/8» (`plan05:157`) | «chapter 7/8» (`plan06:58`) |

**Самый слабый — план 1**, по трём причинам: только 2 примера при норме 1–3 (формально в норме, но меньше остальных); меньше всего misconceptions и источников; нет glossary-шага (его нет и в 2–5, но план 1 задаёт первые 18 терминов, и именно ему он был нужнее всего). Это пропорционально простоте главы, поэтому не критично.

**Самый глубокий — план 3**, но с наибольшим числом внутренних дефектов: ошибка 32↔35 в двух местах, неверная ссылка на главу 14 для mediation/header bidding, повторное «введение» opportunity/impression. Исследовательская часть при этом лучшая в наборе (датированные MRC guidelines, OpenRTB nurl/burl, Google deprecated Reports).

**Эталон формата — план 6**: таблица current/legacy, glossary anchors со стабильными ID и явным разделением «статьи для glossary» / «определить inline» (`plan06:125`), три типа настройки control/signal/exclusion как сквозная модель.

Планы 5–6 заметно опираются на Google/Meta документацию как основные источники (10 из 10 и 9 из 13) — это оправдано темой, но подтверждает находку C.1: курс учит campaign structure и targeting на walled gardens, не объяснив, что это walled gardens.

Общее замечание ко всем планам: ни один не использует master-prompt §4 (четыре view: product/business/data/engineering) как явный checklist; это не обязательно (§4 говорит «не создавай четыре секции механически»), но engineering view в планах 1–2 и 5 присутствует слабо.

---

## F. Размер и нагрузка

### F.1. Факты по написанным главам

| Глава | Пунктов TOC | Слов (ru) | Слов на пункт |
|---|---|---|---|
| 1 | 10 | 2 894 | 289 |
| 2 | 17 | 3 466 | 204 |
| 3 | 25 | 3 767 | 151 |
| 4 | 15 | 4 078 | 272 |
| 5 | 14 | 3 830 | 274 |
| 6 | 17 | 3 493 | 205 |

При скорости чтения технического русского текста с таблицами и формулами ~150–200 слов/мин это 15–25 минут на главу, то есть уже на верхней границе или выше нормы §3 «5–15 минут». Глава 3 с 25 пунктами удержалась в объёме только за счёт 151 слова на пункт — минимальной плотности в наборе, что подтверждает аудит (`audits/ru/03:31` «плотность оправдана»).

### F.2. Главы под риском перегрузки

- **Глава 9 (25 пунктов).** Помимо объёма — forward dependency (A.3.1). Если убрать/сократить 9.13–9.18 до ссылок на 21–23 и перенести главу в часть XI, остаётся 19 пунктов про экономику affiliate — нормальная глава.
- **Глава 19 OpenRTB (24 пункта).** 19.3–19.14 (объекты request) и 19.15–19.21 (response) — reference-материал; 19.22–19.24 (JSON request/response, request-to-impression flow) — walkthrough, частично совпадающий с главой 17 (один impression от начала до конца). Варианты: (a) разделить на «19a. Bid request» и «19b. Bid response, notifications, macros»; (b) перенести 19.24 в 17.18 и оставить 19 как annotated reference с JSON. Приложение D («Основные стандарты») может взять часть reference-нагрузки.
- **Глава 28 MMP (23 пункта).** 28.18–28.20 (три vendor) перенести в 54; 28.10 conversion values — в 29; 28.21–28.22 (MMP vs product analytics / vs network reporting) — одна таблица. Остаётся ~18 пунктов.
- **Глава 36 Ad Fraud (23 пункта).** 36.4–36.19 — таксономия из 16 типов; естественно оформляется одной таблицей «тип → где в funnel → сигнал → кто теряет деньги», а не 16 разделами. Объём управляем, если план это зафиксирует.
- **Глава 3 (25)** — уже написана и прошла аудит; не трогать.

### F.3. Части XI–XIII

- **Часть XI (49–51, по 8 пунктов).** Короткие reference-главы по 3–7 минут — соответствует §3 «маленькая reference-тема». Не лишние: CTV и retail media входят в §2.13 и 52.6. Риск — пересечение 49 ↔ 50 (video auction flow / CTV supply chain) и 8.12 CTV как формат; достаточно, чтобы 50 ссылалась на 49, а не повторяла VAST.
- **Часть XII (52–53).** 52 (6 пунктов) и 53 (14 пунктов) можно слить в одну главу «Карта рынка и метод анализа продукта»: 52 — это категоризация, 53 — framework, и оба служат одной цели §2.13. Глава 2 (`plan02:147`) уже ввёл diagnostic «problem/customer/payer/data/money», а глава 4 — operational checklist vendor economics (`plan04:231`); 53 должен собрать их, не создавая третий framework.
- **Часть XIII (54–55).** 54: десять компаний × framework из 10 вопросов (`master-prompt.md:532`) = 100 ответов плюс 54.11–54.12. Это самая длинная глава книги при любой плотности. Варианты: разбить на 54a (buy side + measurement: TTD, AppLovin, AppsFlyer, Adjust, DoubleVerify) и 54b (sell side + data + commerce: GAM, Magnite, Criteo, LiveRamp, Amazon Ads), либо оформить как reference-карточки по одному шаблону. 55 — capstone, обязательно сохранить; его 20 пунктов — чеклист перерисовки цепочки, а не 20 разделов.
- **Часть X (44–48).** 44 (8 пунктов, все — мотивация «почему особенная») — кандидат на вступление к части, а не главу. 46 и 48 — кандидаты на слияние или жёсткое разграничение (B.2). После устранения дублирования с 31 часть X становится 3–4 главами: 45 (architecture), 46 (runtime reliability), 47 (realtime state), 48 (data correctness).

---

## Приоритизированные рекомендации

### IMPORTANT

1. **TOC: устранить дублирование 31.1–31.4/31.8/31.10 ↔ 45.1–45.4/45.6/45.7.** Разграничить 31 как logical reporting pipeline и 45 как architecture/failure modes, либо слить.
2. **TOC: решить forward dependency главы 9.** Перенести главу 9 в часть XI или переформулировать 9.13–9.18 как «роль в affiliate flow, механика — главы 21–23».
3. **TOC: добавить walled gardens / SAN / search как модель покупки и измерения** (новая глава в части IV или раздел в 15); 26.14–26.15 и 25.17 ссылаются на неё. Без этого §2.13 не выполняется для Meta/Google/TikTok/Apple Search Ads.
4. **TOC: добавить cookie sync / ID matching между SSP и DSP** в 24 (и упоминание в 19.11). Иначе §2.7 «OpenRTB без магии» не достигается.
5. **TOC: убрать прямые повторы:** 16.13 (= 2.17), 16.1–16.4 (голые labels, определённые в 2.6–2.9), 10.4 или 11.8, 26.5–26.8 (= 8.4–8.8; оставить «mobile-specific отличия форматов»), 26.10 (mediation = 12.6–12.8), 28.10 (= 29.8), 28.18–28.20 (= 54.5–54.6), 48.2–48.3 (= 46.1–46.2).
6. **Планы 1–3: исправить ссылки на часть III.** `plan01:26` → «10 и 12»; `plan02:28` → добавить 12; `plan03:42` → «10, 12–14»; `plan03:73, 240` → «глава 32» (текст главы 3 уже ссылается на 32 корректно — расхождение только между планом и главой).
7. **Glossary/план 3: ввести `bid` и `auction`** (минимальные статьи `g-bid`, `g-auction`) при первом существенном использовании в главе 3; снять их из «уже ожидается» в `plan05:84`.
8. **Главы 5–6: привести `# Sources and Further Reading` к `## Источники и дополнительное чтение`** и уровни заголовков заключительных разделов к `##` (нарушение README и §3; ломает EPUB и паритет перевода).

### NICE-TO-HAVE

9. **Planner-формат: добавить категорию «Уточняется здесь»** в `agents/planner-researcher.md` и master-prompt §7 Stage A п. 6, чтобы послойные термины (opportunity, impression, placement, campaign, creative, eCPM, pacing, frequency) не маркировались как «вводится» повторно.
10. **TOC: подписать ракурс у послойных пунктов** (`3.23 fill rate — определение и denominator`, `10.8 fill rate — как управляемый показатель`, `20.10 eCPM — expected eCPM как bid normalization`, `47.3 frequency caps — realtime state`), чтобы будущие Planner-ы видели, что уже дано.
11. **TOC: развести коллизии labels** `2.5/9.6 media buyer` и `22.8/42.4 publisher ID` формулировкой.
12. **TOC: primer по auction в главе 12** (один абзац с deferral в 18) и ограничение 7.15 до «actual price ≤ bid».
13. **Главы 19, 28, 36, 54: заранее зафиксировать стратегию объёма** (split 19 или перенос 19.24 в 17; таблица-таксономия в 36; карточки или split в 54).
14. **Части X и XII: слить 52+53; сделать 44 вступлением к части X; слить или жёстко разграничить 46/48.**
15. **Включить как подпункты:** CAPI-like server-side conversions и pixel↔server dedup в 23; UTM в 22.12; GA4 как пример в 33.17; GPC в 41, DNT как legacy; Apple Search Ads attribution в 27/29.
16. **План 4: снять AR/AP/accrual из «уже ожидается»** или дать сноску — нарушение §1 для бизнес-терминов.
17. **Приложение D:** принять reference-нагрузку OpenRTB-объектов из 19 и одной строкой упомянуть DOOH/audio как вне scope.

---

## Таблица «TOC-пункт → главы → вердикт → как разграничить»

| TOC-пункт | Главы, где повторяется | Вердикт | Как разграничить |
|---|---|---|---|
| ingestion / streams / queues / consumers / aggregation / realtime | 31.1–31.4, 31.8, 31.10 / 45.1–45.4, 45.6, 45.7 | дублирование | 31 — logical reporting pipeline (что считаем, rollups, retention, backfill); 45 — architecture, serving vs analytics path, backpressure. Убрать generic queue/consumer из одной из глав. |
| совмещение ролей | 2.17 / 16.13 | дублирование | Оставить в 2; в 16 — только auction-specific следствия (SSP с exchange-функцией, DSP с own supply). |
| DSP / SSP / exchange / ad network | 2.6–2.9 / 16.1–16.4 / 16.14–16.15 | частично дублирование | 2 — роль, customer, payer, data in/out; 16 — что именно продаётся/покупается, aggregation, money/data flow, глубокие сравнения. Убрать 16.1–16.4 как labels. |
| banner / native / video / interstitial / rewarded | 8.4–8.8 / 26.5–26.8 | дублирование | 8 — формат, assets, measurement; 26 — только mobile-specific delta (SDK rendering, rewarded economics). |
| mediation | 12.6–12.8 / 26.10 | дублирование | Оставить в 12; 26.10 — ссылка плюс роль в mobile stack. |
| AppsFlyer / Adjust / Singular | 28.18–28.20 / 54.5–54.6 | дублирование | Vendor profiles только в 54; 28 — функции MMP без vendor. |
| conversion values | 28.10 / 29.8 | дублирование | Только в 29 (SKAN/AAK); 28 — «MMP конфигурирует mapping, см. 29». |
| retries / duplicates / idempotency | 23.17–23.18 / 32.6–32.8 / 46.1–46.3 / 48.2–48.3 | 46↔48 дублирование; остальное послойно | 23 — dedup rule в tracking contract; 32 — как создаёт discrepancy; 46 — runtime (idempotency, ordering, partial failure); 48 — offline обнаружение и исправление. Убрать 48.2–48.3. |
| reconciliation / backfill | 31.15–31.16 / 32.20 / 47.9 / 48.4, 48.9 | частично дублирование | 32 — почему не сходится; 47 — realtime counter vs ledger; 48 — процесс сверки advertiser/publisher и correction. Backfill — одно место (48.9 или 31.15). |
| placement | 1 (термин), 5.5, 6.9, 8.3, 10.4, 11.8 | послойно (1/5/6/8); 10.4↔11.8 дублирование | 5 — поле конфигурации; 6 — targeting axis; 8 — compatibility с форматом; 10 — publisher-side slot; 11.8 → «маппинг placement → ad unit в ad server» или убрать. |
| CPM / CPC / CPA / CPI / CPL | 3.10–3.15 / 4.1–4.3 | послойно, реализовано | 3 — формула и denominator; 4 — contractual basis и risk allocation. Подписать в TOC. |
| bid strategy | 5.9 / 7.13 | послойно, реализовано | 5 — поле и policy boundary; 7 — семейство стратегий и математика. |
| money flow / кто кому платит | 1.6 / 2.16 / 4.8–4.15 / 16.11 | послойно; 16.11 риск | 1 — направление; 2 — contractual path и service fees; 4 — ledgers, gross/net, `$100`; 16 — только clearing price → fees → publisher в auction. |
| fill rate / eCPM | 3.11, 3.23 / 10.8, 10.9 / 12.3 / 20.10 | послойно | 3 — определение; 10 — как управляемый показатель yield; 12 — historical eCPM для ranking; 20 — expected eCPM как bid normalization. Подписать смысл в каждой главе. |
| frequency / frequency cap | 3.5 / 7.10 / 11.12 / 47.3 / 42.9 | послойно | метрика / настройка advertiser / правило ad server / realtime state / ограничение без identity. |
| pacing / budget allocation | 7.8, 7.11 / 20.14, 20.15 / 47.1 | послойно | 7 — с позиции advertiser; 20 — алгоритм DSP; 47 — state и race conditions. |
| viewability | 3.3 / 17.14 / 37.2–37.3 | послойно, реализовано | 3 — лестница served/rendered/viewable и датированные thresholds; 17 — место в flow; 37 — методология, OMID, vendors. |
| CAC / ARPU / ARPPU / LTV | 3.16, 3.21–3.22 / 33.9–33.12 | послойно | 3 — формулы и caveats (уже дано); 33 — cohorts over time, payback, campaign profitability; не переопределять. |
| MMP vs product analytics | 2 (misconception) / 28.21 / 33.17 | послойно | 28 — что MMP не делает; 33 — чем advertising analytics отличается; в 28 одна таблица. |
| identity providers / deterministic / probabilistic | 2.15 / 24.14–24.18 / 42.5–42.7 | послойно; 42.6–42.7 риск | 2 — роль; 24 — механика; 42 — те же методы без третьесторонних ID (явно ссылаться на 24). |
| ATT / IDFA | 24.6 / 29.1–29.3 / 40.10–40.11 | послойно | 24 — identifier; 29 — последствия для attribution; 40 — privacy-ограничение. |
| timeouts | 13.10 / 18.13 / 32.5 / 46.7 | послойно | header bidding / auction / discrepancy / reliability — подписать ракурс. |
| late events / late conversions | 23.19 / 32.15 / 46.6 | послойно | attribution window / отчёт меняется задним числом / event-time vs processing-time. |
| media buyer | 2.5 / 9.6 | коллизия labels | 2 — функция внутри advertiser/agency; 9 — affiliate, покупающий трафик за свой счёт. Развести формулировкой. |
| publisher ID | 22.8 / 42.4 | коллизия labels | 22 — параметр tracking URL; 42 — first-party identity publisher-а. |
| video / CTV | 8.6, 8.12 / 49 / 50 | частично | 8 — формат; 49 — VAST/tracking; 50 — SSAI/pods/household identity; 50.8 ссылается на 49.8, не повторяет. |
