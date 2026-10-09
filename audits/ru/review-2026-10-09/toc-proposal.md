# Предложение по реструктуризации TOC — 2026-10-09

Основание: решение владельца курса «полная реструктуризация сейчас, до главы 7» и findings `curriculum.md` (разделы A–F). **Статус: вариант A утверждён и применён 2026-10-09** — `master-prompt.md` §10–11, ссылки в планах 1–4, README-adtech.md и README.md обновлены.

Цель: устранить дублирование, закрыть три пропуска (walled gardens, search auction, cookie sync), убрать forward dependency главы 9 — и при этом сдвинуть как можно меньше номеров, потому что в шести главах, шести планах и шести переводах уже стоят ссылки «глава N».

---

## 1. Два варианта размещения новой главы про walled gardens

Новая глава нужна в любом случае: главы 5–6 де-факто учат на Google Ads и Meta, не объясняя, что это закрытые платформы с собственным auction, собственным измерением и без SSP/OpenRTB. Вопрос — куда её ставить.

### Вариант A (рекомендую): на место главы 9 в части II, affiliate — в часть XI

Логика: часть II называется «Campaigns и Performance Marketing» и описывает кампанию глазами advertiser. После campaign (5), targeting (6), bidding (7) и creative (8) естественный вопрос — «а где всё это покупается и чем self-serve платформа отличается от open programmatic, о котором будет часть IV». Affiliate marketing — такая же отдельная экосистема, как CTV и retail media, и зависит от механики tracking (21–23), поэтому его место — часть XI, после части V.

**Что сдвигается:** только главы 45–55 (см. §3). Главы 1–44 сохраняют номера. В написанных главах 1–6 и их EN-переводах **ни одна ссылка не меняется** (они ссылаются на 2, 3, 4, 6, 7, 8, 11, 24, 27–29, 32, 37, 40). В планах меняются три ссылки.

### Вариант B: новая глава в части IV после главы 15, affiliate остаётся главой 9

Логика ревьюера плана: walled gardens — альтернатива open programmatic, поэтому место рядом с 15. Но тогда 9.13–9.18 (tracking link, click ID, S2S postback, deep link) остаются до части V, и сдвигаются все главы 16–55: меняются ссылки на 24, 27–29, 32, 37, 40 в главах 2, 3 и 6 (RU и EN) и десятки ссылок в планах.

**Стоимость B примерно в 10 раз выше A при том же содержательном результате.** Единственное преимущество B — тематическая близость к 15, которую в A закрывает прямая ссылка из 15.1–15.4 на главу 9.

---

## 2. Новый TOC (вариант A) — изменения по частям

Жирным — новое или перемещённое. «→» — что делать с пунктом. Пункты, которые не упомянуты, не меняются.

### Часть I. Фундамент (1–4) — без изменений

Подписать ракурс у послойных пунктов, чтобы будущие Planner-ы видели, что определение уже дано:
- 3.11 `eCPM — определение; publisher-side realized revenue per mille`
- 3.23 `fill rate — определение и denominators`, 3.24 `win rate — определение`
- 4.1–4.3 `CPM/CPC/CPA как contractual basis и risk allocation (формулы — глава 3)`

### Часть II. Campaigns и Performance Marketing (5–9)

- 5.5 `placement — поле конфигурации campaign (publisher-side смысл — глава 1, targeting axis — 6.9, формат — 8.3)`
- 5.9 `bid strategy — как выбранная policy (математика — глава 7)`
- 6.9 `placement — как targeting axis`
- 7.15 `max bid vs actual price → «actual price ≤ bid; почему — глава 18»`
- 8.3 `placement — compatibility с форматом и ad unit`
- **9. Walled gardens, self-serve platforms и search (новая)**
  9.1 self-serve platform vs open programmatic; 9.2 walled garden; 9.3 closed auction без SSP/exchange/OpenRTB; 9.4 search advertising как рынок; 9.5 keyword auction концептуально (relevance/quality и ad rank без формул); 9.6 social feed auction; 9.7 first-party data platform как основа targeting; 9.8 self-reporting и conversion claims; 9.9 SAN vs non-SAN; 9.10 Apple Search Ads как пример; 9.11 API-based integrations (MMP, conversions API) концептуально; 9.12 где walled gardens стоят в value chain; 9.13 почему главы 5–8 учили на Google/Meta и что из этого переносимо; 9.14 trade-offs для advertiser: reach и данные против прозрачности и контроля.

### Часть III. Publisher Side (10–14) — номера без изменений

- 10.4 `placement — publisher-side slot`; 10.8 `fill rate — как управляемый показатель yield`; 10.9 `eCPM — как инструмент сравнения demand`
- 11.8 `placement/ad unit → «маппинг placement → ad unit в ad server»`
- 12: добавить **12.0 primer «auction, bid, clearing price — минимум для этой главы; подробно — глава 18»** (как 12.1, остальные сдвигаются внутри главы)
- 12.3 `historical eCPM — как estimate для ranking`

### Часть IV. Programmatic и RTB (15–20) — номера без изменений

- 15.4 `programmatic ≠ RTB`, добавить **15.11 open programmatic vs closed platforms — связь с главой 9**
- 16: **убрать 16.1–16.4** (голые labels, определены в 2.6–2.9) и **16.13** (= 2.17); перенумеровать оставшиеся 16.5–16.15 → 16.1–16.10; 16.11 money flow → `только auction-specific path: clearing price → fees → publisher`
- 19.11 `user → включая buyeruid и связь с cookie sync (механика — глава 24)`
- 20.10 `eCPM — expected eCPM как bid normalization (не publisher eCPM главы 3/10)`

### Часть V. Tracking, Identity и Attribution (21–25) — номера без изменений

- 22.8 `publisher ID — как параметр tracking URL (не first-party identity publisher-а, см. 42.4)`
- 23: добавить **23.21 browser + server dual tracking (CAPI-like) и dedup pixel ↔ server**
- 24: добавить **24.20 cookie sync / ID matching между SSP и DSP (match tables, buyeruid)**
- 25.17 `why platforms claim the same conversion → ссылка на 9.8`

### Часть VI. Mobile Measurement и MMP (26–29) — номера без изменений

- 26.5–26.8 → **один пункт `26.5 mobile-specific отличия форматов (SDK rendering, rewarded economics); сами форматы — глава 8`**; перенумеровать 26.9–26.16 → 26.6–26.13
- 26.10 mediation → `роль в mobile stack; механика — глава 12`
- 26.14–26.15 SAN/non-SAN → `ссылка на главу 9; здесь — последствия для mobile measurement`
- 27: добавить `27.15 Apple Search Ads attribution (AdServices) как третий canonical source`
- 28: **убрать 28.10** (conversion values — только в 29.8) и **28.18–28.20** (vendors — только в 53); 28.21–28.22 → одна сравнительная таблица; перенумеровать

### Часть VII. Analytics и Measurement (30–35) — номера без изменений

- **31. Reporting, Aggregation, Pipelines и Event-driven Architecture** (поглощает старую 45): 31.1–31.17 как были + `31.18 serving vs analytics paths; 31.19 backpressure; 31.20 batching; 31.21 typical AdTech architecture`
- 33.9–33.12 `ARPU/ARPPU/LTV/CAC — cohort-over-time, payback, качество acquired users; определения — глава 3`
- 33.17 → добавить пример GA4 / web analytics vs ad tracking (UTM)

### Часть VIII. Quality, Fraud и Supply Chain (36–39) — без изменений

- 36.4–36.19 → план фиксирует формат: одна таблица-таксономия `тип → место в funnel → сигнал → кто теряет деньги`

### Часть IX. Privacy, Consent и Addressability (40–43) — без изменений

- 41.3 consent signal → добавить `GPC; DNT как legacy`
- 42.4 `publisher IDs — first-party identity publisher-а (не параметр tracking URL, см. 22.8)`
- 42.6–42.7 → `те же deterministic/probabilistic методы главы 24 в условиях без третьесторонних ID`

### Часть X. Engineering AdTech — **было 44–48, стало 44–47**

- 44. Почему AdTech-инфраструктура особенная — без изменений
- ~~45. Event-driven архитектура~~ → **слита в 31**
- **45. Reliability** (бывшая 46) — без изменений содержания
- **46. Counters, Budgets и Realtime State** (бывшая 47); 47.9 reconciliation → `realtime counter vs ledger`
- **47. Data Quality и Reconciliation** (бывшая 48); **убрать 48.2–48.3** (= 46.1–46.3), 48.4 → `процесс сверки advertiser/publisher`, 48.9 → `correction/backfill (единственное место для backfill; из 31.15–31.16 убрать backfill, оставить reprocessing)`

### Часть XI. Отдельные экосистемы — **было 49–51, стало 48–51**

- **48. Video Advertising** (бывшая 49)
- **49. CTV** (бывшая 50); 50.8 CTV supply chain → `ссылается на 48.8, не повторяет VAST`
- **50. Retail / Commerce Media** (бывшая 51)
- **51. Performance и Affiliate Marketing** (бывшая 9): 9.13–9.18 переформулировать как `роль tracking link / click ID / subID / S2S postback / smartlink / deep link в affiliate flow (механика — главы 21–23, 28)`; 9.6 `media buyer — affiliate, покупающий трафик за свой счёт (не 2.5)`

### Часть XII. Карта рынка — **было 52–53, стало 52**

- **52. Категории AdTech-компаний и метод анализа продукта** (слияние 52+53): 52.1–52.6 категории + 52.7–52.20 framework (бывшие 53.1–53.14). Framework должен собрать role card главы 2 и vendor-economics checklist главы 4, не создавая третий.

### Часть XIII. Финальный разбор — **было 54–55, стало 53–54**

- **53. Десять компаний** (бывшая 54): формат — reference-карточки по одному шаблону (иначе самая длинная глава книги)
- **54. Финальный end-to-end case study** (бывшая 55)

**Итого: 54 главы** (было 55: −45, −53, −9 на старом месте, +9 новая, +51 affiliate).

---

## 3. Таблица перенумерации

| Было | Стало | Примечание |
|---|---|---|
| 1–8 | 1–8 | — |
| 9 Affiliate | **51** | перенос в часть XI |
| — | **9 Walled gardens** | новая |
| 10–44 | 10–44 | — |
| 45 Event-driven | **→ 31** | слияние |
| 46 | 45 | |
| 47 | 46 | |
| 48 | 47 | |
| 49 | 48 | |
| 50 | 49 | |
| 51 | 50 | |
| 52 + 53 | **52** | слияние |
| 54 | 53 | |
| 55 | 54 | |

---

## 4. Что придётся править в уже написанном (вариант A)

Проверено grep-ом по `chapters/ru`, `chapters/en`, `plans/ru`, `glossary*.md`, `agents/`, `README*`.

**Главы 1–6 (RU и EN):** ничего. Все 14 ссылок указывают на главы ≤ 44.

**Планы (три ссылки на сдвинутые номера + четыре исправления ошибок, найденных ревью):**
- `plans/ru/04-…plan.md`: «глава 9» (traffic arbitrage) → «глава 51»; «глава 48» (data quality) → «глава 47»
- `plans/ru/02-…plan.md`: «главы 52–54» → «главы 52–53»
- `plans/ru/01-…plan.md:26`: «главы 10 и 14» → «главы 10 и 12» (ошибка, не перенумерация)
- `plans/ru/02-…plan.md:28`: «главы 10 и 14» → «главы 10, 12 и 14»
- `plans/ru/03-…plan.md:42`: «главы 10 и 14» → «главы 10, 12–14»
- `plans/ru/03-…plan.md:73, 240`: «глава 35» / «chapter 35» → «глава 32»

**`master-prompt.md` §10:** переписать TOC по §2 выше; §2 цели курса — без изменений; §11 приложения — добавить в D строку «DOOH, audio, in-game — вне основного курса».

**`README-adtech.md`:** central sequence `market → campaign → programmatic → …` дополнить: `market → campaign → platforms (walled gardens) → publisher side → programmatic → tracking → …`.

**`agents/planner-researcher.md`, master-prompt §7 Stage A п. 6:** добавить третью категорию терминов «Уточняется здесь» и обязательный glossary-шаг (сейчас выполнен только планом 6).

**Сайт и сборка:** `part` в front matter глав 1–6 не меняется; порядок глав на сайте — по полю `chapter`, поэтому новая глава 9 и перенесённая 51 встанут на место автоматически.

---

## 5. Порядок выполнения

1. Утвердить вариант A или B.
2. Переписать §10 `master-prompt.md` (одним коммитом, с этим документом как обоснованием).
3. Исправить семь ссылок в планах 1–4.
4. Обновить `README-adtech.md` и `agents/planner-researcher.md`.
5. Только после этого запускать `Глава 7`.
