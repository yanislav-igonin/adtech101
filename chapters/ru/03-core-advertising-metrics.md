---
id: ch-03
type: chapter
part: I
chapter: 3
slug: core-advertising-metrics
title: "Основные рекламные метрики"
language: ru
status: reviewed
toc_requirements: ["3.1", "3.2", "3.3", "3.4", "3.5", "3.6", "3.7", "3.8", "3.9", "3.10", "3.11", "3.12", "3.13", "3.14", "3.15", "3.16", "3.17", "3.18", "3.19", "3.20", "3.21", "3.22", "3.23", "3.24", "3.25"]
prerequisites: [ch-01, ch-02]
---

# Основные рекламные метрики

## Суть: метрика — это contract, а не формула

Рекламная метрика — не формула, а contract измерения: договорённость о том, какое событие считается, в какой точке, после каких filters, на каком знаменателе и в чьих деньгах. Арифметика здесь простая — деление и умножение на тысячу, — сложна семантика: impression[^g-impression] и click[^g-click] в разных системах означают разные события, и одно название метрики скрывает разные contracts. Поэтому одна campaign[^g-campaign] порождает три одновременно правдивых отчёта — у advertiser[^g-advertiser], publisher[^g-publisher] и platform — с разными числами. Глава идёт по порядку flow: от возникновения рекламного места до impression, click и outcome, затем цена события, деньги и return, ценность user и monetization, — и собирает всё в одном сквозном примере.

## Почему число без определения ничего не говорит

Рекламная campaign проходит через несколько систем. Publisher наблюдает возникновение рекламного места и доставку рекламы; buying platform — доступные ей запросы и сделки; advertiser — расходы и business outcomes. Каждая система агрегирует собственный участок flow. Поэтому колонка `Impressions: 8,000` сама по себе не сообщает, что именно произошло и почему её число должно или не должно совпадать с соседним отчётом.

**Metric contract**[^g-metric-contract] — полное определение метрики, по которому число можно воспроизвести и интерпретировать:

```text
event definition + measurement point
+ filters и deduplication
+ numerator / denominator
+ dimensions
+ period и event/reporting/attribution window
+ currency
+ perspective и ledger boundary
```

Например, `CTR = 2%`[^g-ctr] ещё не contract. Нужно знать, какие clicks и impressions допустимы, где они зарегистрированы, исключены ли повторы, за какой период и в разрезе какой campaign. Для денежной метрики дополнительно важны валюта, правила currency conversion, refunds и то, чьи это деньги. Далее слово **qualifying** означает событие, прошедшее filters и validation конкретной системы по её contract, а **eligible** — событие, допущенное ею к расчёту (как правило, в знаменатель).

Базовые классы метрик отвечают на разные вопросы:

| Класс | Что измеряет | Пример |
|---|---|---|
| `count` | Сколько qualifying событий или единиц учёта зарегистрировано | 8,000 impressions |
| `rate` | Какая доля одного count приходится на другой | `160 clicks / 8,000 impressions = 2% CTR` |
| `unit/effective metric` | Сколько cost[^g-cost] или revenue[^g-revenue] приходится на единицу результата | `$96 / 160 clicks = $0.60 CPC`[^g-cpc] |
| `return metric` | Как измеренная ценность соотносится с вложением | `$480 / $96 = 5.0x ROAS`[^g-roas] |

Перед сравнением двух колонок задайте семь вопросов:

```text
Кто считает?
Что считается и в какой measurement point?
Где проходит measurement boundary?
Когда событие произошло и в какой period/window попало?
Какие filters и deduplication применены?
Каков denominator?
Какая currency и чьи это деньги?
```

Этот contract важнее названия. Даже арифметически простая формула отвечает на другой вопрос после замены `rendered impression`[^g-rendered-impression] на `served impression`[^g-served-impression], click на install или advertiser spend[^g-media-spend] на publisher revenue[^g-publisher-revenue].

## От opportunity до возможного exposure

На media surface publisher сначала возникает **ad opportunity**[^g-ad-opportunity] — конкретная возможность показать рекламу, например полноэкранный placement[^g-placement] после завершения уровня в игре. **Request** — уже техническое сообщение конкретной системе с просьбой выбрать рекламу, вернуть creative[^g-creative] или принять участие в auction[^g-auction]. Это разные уровни:

- opportunity может не породить request из-за локального правила или фильтра;
- один request может содержать несколько рекламных объектов;
- одна opportunity может вызвать fan-out в несколько downstream `bid request`;
- retries увеличивают request count без новой opportunity;
- batch объединяет несколько opportunities в одном сообщении.

IAB Tech Lab Programmatic Auction Definitions используют `Ad Request` для информации об impression opportunity, выставляемой на auction. На границе протокола OpenRTB 2.6 один `BidRequest` содержит один или несколько объектов `Imp`. Это достаточная причина не считать HTTP requests безусловным proxy user-facing opportunities; конкретная production implementation может отличаться.

```text
publisher surface
  → ad opportunity
  → 0..N request / bid request
  → response / bid / win
  → served response
  → rendered impression
  → measurable → viewable impression
  → click
  → advertiser-defined conversion
  → attributed revenue / customer value
```

Это карта measurement[^g-measurement] points, а не универсальная строго убывающая воронка. Fan-out и retries могут дать requests больше opportunities; video pod — рекламный блок из нескольких video ad units подряд (глава 48) — даёт несколько impressions на одну opportunity; один user может сделать несколько clicks или conversions[^g-conversion]; filters, deduplication и разные windows меняют совокупность событий между отчётами.

**Impression** — зарегистрированное рекламное событие по counting rule конкретной системы. Слово без qualifier не доказывает ни render, ни viewability, ни внимание человека.

| Состояние | Минимальное свидетельство | Чего оно не доказывает |
|---|---|---|
| `served impression` / served response | Server или platform зарегистрировал выдачу ad response, кода или инструкции creative | Что device загрузил и начал отображать creative |
| `rendered impression` | Client/device начал render по применимому правилу | Что достаточная часть creative была на экране достаточно долго |
| `measurable` | Measurement tool смог определить geometry/time условия exposure | Что условия viewability выполнены |
| `viewable impression`[^g-viewable-impression] | Valid rendered served impression выполнил применимые geometry/time criteria | Что человек действительно посмотрел рекламу или обратил внимание |
| `non-viewable` | Measurement состоялся, criteria не выполнены | Что impression был non-measurable |
| `non-measurable` / undetermined | Доступных signals недостаточно для определения viewability | Что impression был видим или невидим |

MRC Desktop Display Impression Measurement Guidelines требуют для квалифицированного client-side count загрузки creative и как минимум начала render. MRC Viewable Ad Impression Guidelines (v2.0) связывают viewable impression с valid rendered served impression. Классический benchmark Viewable Guidelines 2014/2015 — не менее 50% pixels на протяжении одной continuous second для display и двух continuous seconds для video; его же использует Digital Audience-Based Standard 2017. Это не универсальное правило для любого формата и environment: MRC публикует отдельные guidelines для mobile, video, OTT/CTV (streaming и connected TV; глава 49), in-game и AR; детали — глава 37.

### Reach и frequency: от событий к аудитории

**Reach**[^g-reach] — de-duplicated число уникальных единиц аудитории (entity: человек, устройство или домохозяйство), получивших хотя бы одну qualifying exposure за период, либо доля таких единиц в явно заданной совокупности:

```text
reach count = unique entities с ≥ 1 qualifying exposure за period
reach rate  = reached unique entities / declared universe × 100%
```

Единица аудитории обязана быть названа: `person`, `device`, `household`, account или modeled audience. `20,000 device IDs`, `20,000 modeled persons` и `20,000 households` — не взаимозаменяемые counts. Без размера universe — заявленной аудитории, относительно которой считается доля, — нельзя вычислить reach rate, а без identity coverage и правил cross-device deduplication нельзя оценить полноту reach.

**Frequency**[^g-frequency] — среднее число qualifying exposures на одну единицу аудитории, вошедшую в reach, за тот же период:

```text
frequency = qualifying impressions / reached unique entities
```

Учебный пример: 60,000 qualifying viewable impressions за неделю распределены между 20,000 de-duplicated persons выбранной совокупности. Reach count равен 20,000 persons, average frequency — `60,000 / 20,000 = 3`. Это не означает, что каждый человек видел рекламу ровно три раза: frequency является средним.

MRC Digital Audience-Based Standard 2017 года использует qualifying viewable impressions для своей measurement basis. Product dashboards могут считать reach по другому impression basis, по devices или с modeling. Поэтому `reach` и `frequency` сравнимы только при одинаковых единице аудитории, exposure rule, совокупности, de-dup scope и period.

## От exposure к реакции и outcome

**Click** — qualifying user-initiated interaction с рекламой. Даже у одного действия есть несколько measurement points:

```text
user initiates click
  → click tracker / redirect      # measured click
  → destination receives request # received click
  → landing page resolves/loads   # resolved click
```

User может закрыть экран, сеть может оборваться, redirect может не завершиться, а разные системы могут применить разные filters. Поэтому initiated, measured, received и resolved clicks не обязаны совпадать. IAB/MRC Click Measurement Guidelines v1.0 (2009) по-прежнему перечислены MRC как measurement baseline, но их browser/HTTP wording является legacy и не описывает исчерпывающе современные app- и platform-взаимодействия; redirect выше — типичный, не единственный flow.

**CTR (Click-Through Rate)** показывает долю выбранных impressions, после которых зарегистрированы выбранные clicks:

```text
CTR = qualifying clicks / counted impressions × 100%
```

Если advertiser report считает 160 clicks и 8,000 impressions по одному contract, `CTR = 2%`. Замена served impressions на rendered, всех clicks на filtered clicks или совокупности уровня campaign на совокупность уровня creative изменит число. Высокий CTR сам по себе не означает качественный traffic, conversions или causal lift.

**Conversion** — valuable action или outcome, который advertiser определил как значимый и который система засчитала по measurement и attribution[^g-attribution] rules. Для subscription app это может быть install, trial, первая оплаченная подписка или renewal. Эти actions нельзя складывать без явного counting rule: один click способен привести к install, trial и subscription, то есть к нескольким conversions.

Наблюдаемый purchase означает, что событие зарегистрировано. **Attributed conversion** означает, что выбранное attribution rule назначило рекламному touchpoint credit за этот outcome. Counts зависят от conversion definition, attribution/lookback window (срока после touchpoint, в течение которого outcome ещё может получить credit; глава 25), filters, late-arriving events и режима подсчёта. Ни observed, ни attributed conversion сами по себе не доказывают, что реклама вызвала outcome: attribution распределяет credit, а causality требует доказательства incrementality — экспериментальной оценки прироста, который дала реклама (глава 34).

**CVR (Conversion Rate)**[^g-cvr] имеет смысл только с названным предшествующим событием (precursor):

```text
CVR = qualifying conversions / declared eligible precursor events × 100%
```

| Полное имя | Числитель | Знаменатель | Какой переход измеряет |
|---|---|---|---|
| click-to-install CVR | attributed installs | eligible clicks | Click → install |
| install-to-trial CVR | qualifying trials | attributed installs | Install → trial |
| click-to-subscription CVR | attributed subscriptions | eligible clicks | Click → subscription |

Голое `CVR` скрывает разные funnels. Даже значение выше 100% не всегда является ошибкой: например, Google Ads считает conversions на trackable ad interactions, а режим `Every` (засчитывать каждую conversion после interaction, а не одну) вместе с несколькими conversion actions может дать больше одной conversion на interaction. Знаменатель и counting rule — часть названия метрики.

## Нормализованная цена события: CPM, eCPM и cost-per-X

Абсолютные расходы не позволяют сравнить активность разного масштаба. Unit metrics делят признанный cost или revenue на явно определённое событие. В post-fact отчёте это фактические средние; те же названия могут обозначать pricing model, bid[^g-bid] или optimization target[^g-optimization-target], что не гарантирует совпадения с фактическим средним.

| Метрика | Фактическая формула | Перспектива и знаменатель | Главная неоднозначность |
|---|---|---|---|
| **CPM (Cost per Mille)**[^g-cpm] | `advertiser cost or spend / counted impressions × 1,000` | Buyer; тысяча выбранных impressions | Может означать pricing basis[^g-pricing-basis], rate, bid либо observed average CPM |
| **eCPM (effective CPM)**[^g-ecpm] | `recognized revenue / counted impressions × 1,000` | Обычно publisher/seller; тысяча выбранных impressions | Revenue и impression scope зависят от seller contract |
| **CPC (Cost per Click)** | `cost / qualifying clicks` | Buyer; clicks по disclosed rule | Bid/target CPC не равен фактическому average CPC |
| **CPA (Cost per Action)**[^g-cpa] | `cost / qualifying actions` | Buyer; advertiser-defined action | Action может быть trial, order, lead или subscription, не обязательно новый customer |
| **CPI (Cost per Install)**[^g-cpi] | `cost / qualifying installs` | Mobile acquisition; attributed installs | Install count зависит от measurement и attribution rules |
| **CPL (Cost per Lead)**[^g-cpl] | `cost / qualifying leads` | Lead generation; business-defined lead | Lead definition и quality различаются; lead ещё не customer |
| **CAC (Customer Acquisition Cost)**[^g-cac] | `allocated acquisition costs / new customers` | Бизнес advertiser; новые customers | В числитель могут входить media, agency[^g-agency], sales и onboarding costs |

`Mille` означает тысячу. Observed CPM отвечает: «сколько buyer потратил на тысячу counted impressions?» eCPM отвечает: «сколько признанного revenue seller получил на тысячу counted impressions?» Формулы симметричны, но числители принадлежат разным ledger boundaries[^g-ledger-boundary]. Publisher может использовать eCPM, чтобы сравнивать demand[^g-demand], оплачиваемый по CPM, CPC или CPA, на общей basis фактического revenue. На buy side eCPM тоже встречается — как нормализованный cost: DSP[^g-dsp], платящий по CPC или CPA, приводит расход к цене за тысячу impressions, чтобы сравнить его с CPM-инвентарём. Поэтому CPM и eCPM не являются автоматически двумя названиями одного числа.

CPC, CPA, CPI и CPL образуют один шаблон `recognized cost / qualifying events`, но событие определяет бизнес-смысл. Низкий CPL бесполезен, если lead не проходит qualification; низкий CPI не говорит, что install оформит подписку; CPA нельзя читать без имени action.

CAC шире platform CPA. Если platform report показывает `$4 CPA` за subscription, он использует platform cost и attributed subscription action. Бизнес может считать новым customer только первую подтверждённую оплату и включать в acquisition costs media, agency, sales и onboarding. Пока customer event, period, cost allocation и refunds не согласованы, platform CPA нельзя переименовать в CAC.

## Чьи деньги и какой return

Одна сумма меняет название в зависимости от участника и ledger boundary:

```text
advertiser: spend / media cost
        → selling или buying platform:
          revenue на одной boundary,
          downstream media/traffic cost на другой boundary
        → publisher: recognized publisher revenue
```

**Revenue** — выручка, признанная выбранным участником по его правилам. **Spend** — расход buyer на media в выбранном scope. **Cost** — затраты того участника, чью экономику анализируют; для advertiser это может быть media cost, для platform — downstream cost, для бизнеса — более широкий набор расходов. Estimated dashboard value, invoiced amount, settled amount и recognized revenue могут относиться к разным состояниям. Для сравнения нужно согласовать period, timezone, currency conversion, taxes/refunds и participant. Gross/net accounting[^g-gross-net-revenue], take rate[^g-take-rate] и settlement[^g-settlement] подробно разбираются в главе 4.

**ROAS (Return on Ad Spend)** измеряет media efficiency:

```text
ROAS = attributed conversion value or revenue / ad spend
```

Результат можно записать как `5.0x` или `500%`. Он зависит от attribution rules и выбранного value field. **ROI (Return on Investment)**[^g-roi] оценивает прибыльность более широкого investment scope:

```text
ROI = net profit / total relevant investment cost
    = (return − total relevant cost) / total relevant cost
```

В учебном walkthrough advertiser получает `$480` attributed conversion value при `$96` ad spend: ROAS равен `5.0x`. Если трактовать `$480` как attributed revenue, а полный согласованный cost с media, delivery продукта, agency и operations равен `$600`, net profit составляет `−$120`, а ROI — `−20%`. Высокий ROAS совместим с отрицательным ROI, потому что denominators и cost scopes различаются. И ROAS, и attributed revenue остаются attribution-dependent: без causal design они не доказывают incremental return.

## Ценность user во времени: ARPU, ARPPU и LTV

Acquisition metric говорит, сколько стоило получить событие или customer; product-value metric — сколько выбранная совокупность users принесла или, согласно модели, принесёт.

| Метрика | Рабочая формула | Обязательный contract |
|---|---|---|
| **ARPU (Average Revenue per User)**[^g-arpu] | `selected revenue / all eligible users` | User definition, revenue categories, period, cohort/совокупность |
| **ARPPU (Average Revenue per Paying User)**[^g-arppu] | `selected purchase revenue / paying users` | Payer event, purchase revenue, refunds, period |
| **LTV (Lifetime Value)**[^g-ltv] | `cumulative observed or predicted value / cohort members` | Cohort, horizon, identity, observed/predicted status, revenue/contribution basis |

Учебный subscription cohort: за месяц 1,000 active users создают `$1,000` выбранного recognized revenue, из них 100 users платят; для простоты весь revenue в примере является purchase revenue. Тогда `ARPU = $1,000 / 1,000 = $1`, а `ARPPU = $1,000 / 100 = $10`. ARPU включает non-paying users выбранной совокупности; ARPPU делит только на payers. Эти числа ничего не говорят о lifetime без cohort и горизонта (cohort-анализ — глава 33).

Google Analytics Data API, например, определяет ARPU как total revenue на active user с purchase, subscription и ad revenue, а ARPPU — purchase revenue на paying active user. Это product-specific contract, не универсальный словарь: другая компания может иначе определять active user, payer, revenue, taxes и refunds.

**Observed LTV** суммирует фактически зарегистрированную value cohort к заданному горизонту, например `30-day revenue LTV`. **Predicted LTV** оценивает будущую value по модели и assumptions, например `12-month predicted contribution LTV`. Revenue LTV не вычитает расходы; contribution/profit LTV использует оговорённую маржинальную basis. GA4 User Lifetime объединяет lifetime interactions и поддерживает observed и predictive metrics, но identity method и sampling влияют на результат. Поэтому «LTV пользователя» без cohort, горизонта, identity rule, value basis и model status — не определённое число.

## Где теряется monetization: fill rate и win rate

Fill и win описывают разные стадии flow и принадлежат разным владельцам. Они не являются дополнениями друг друга до 100%.

| Метрика | Один распространённый contract | Стадия и владелец | Почему число меняется дальше |
|---|---|---|---|
| **Fill rate**[^g-fill-rate] | `filled responses / eligible ad requests` | Publisher/ad server[^g-ad-server]: request → fill | Filled response может не отрисоваться и не стать counted impression, поэтому fill на response basis выше доли доставленных показов |
| **Bid rate** | `submitted bids / eligible bid requests` | Buyer: request → bid/no-bid | Buyer фильтрует opportunities и отвечает не на все requests |
| **Win rate**[^g-win-rate] | `winning bids / submitted eligible bids` | Buyer/deal: bid → auction win | Win notice ещё не является delivery или billing event |

У fill rate нет одного безопасного vendor-neutral denominator. Product может делить filled responses, counted impressions или другой fill event на requests, opportunities или ad units — и это разные метрики. Google Ad Manager sell-through documentation использует `Total impressions / Total ad requests`; для optimized video pods часть requests/unfilled units выводится из durations и configured ad opportunity duration. Это точное product definition, но не правило для любого ad server. `Match rate`, `response rate`, `delivery rate` и `fill rate` могут именовать соседние transitions, а не aliases.

Win rate также требует раскрытия совокупности. Auction может получить bid, выбрать его победителем, отправить win notice, но не доставить creative или не создать billable impression[^g-billable-event]. OpenRTB различает win notice и billing notice; billing policy может зависеть от delivery, viewability или других правил. В legacy Google Ad Manager reporting встречалась формула `Deals win rate = winning bids / bids`; это датированный пример denominator, а не универсальная taxonomy.

## Одна campaign, три правдивых отчёта

Соберём метрики на одном согласованном сценарии. Все числа ниже **учебные**, их масштаб условный и подобран для простой арифметики. Subscription app рекламируется внутри mobile game; period, например, одна неделя, валюта — USD. Каждый расчёт использует собственный явно названный contract, а не предполагает общий global event store.

### Advertiser: outcome и эффективность acquisition

Advertiser report содержит только его срез: 8,000 counted impressions, 160 qualifying clicks, 80 attributed installs, 24 attributed subscriptions, `$96` spend и `$480` attributed conversion value.

```text
CTR  = 160 / 8,000 × 100%        = 2%
CPM  = $96 / 8,000 × 1,000       = $12
CPC  = $96 / 160                 = $0.60
CPI  = $96 / 80                  = $1.20
CVR  = 80 / 160 × 100%           = 50%   # click → install
CVR  = 24 / 80 × 100%            = 30%   # install → subscription
CVR  = 24 / 160 × 100%           = 15%   # click → subscription
CPA  = $96 / 24                  = $4    # action = attributed subscription
ROAS = $480 / $96                = 5.0x
```

Здесь `$12 CPM`, `$1.20 CPI` и `$4 CPA` — post-fact averages, а не заявление о billing model или bid. Три CVR описывают три разных перехода одной воронки и без пометки несравнимы. `$480` — attributed value, не доказанная causal value.

### Publisher: delivery и monetization

Publisher за тот же period агрегирует всех buyers, а не только этого advertiser: 100,000 eligible ad requests, 80,000 counted impressions и `$800` recognized publisher revenue.

```text
fill rate = 80,000 / 100,000 × 100% = 80%   # числитель — counted impressions по contract этого ad server
eCPM      = $800 / 80,000 × 1,000   = $10
```

Итоги publisher закономерно больше среза advertiser. Его `$800 revenue` не является `$96 spend` advertiser: это другая совокупность impressions и другая ledger boundary. Разница между `$12 CPM` buyer и `$10 eCPM` seller складывается из удержаний посредников на пути денег и из разного состава impressions; удержания посредников — тема главы 4.

### Platform: auction и граница delivery

Рассматриваемая platform — в учебном примере DSP, через который покупает только этот advertiser, — видит 60,000 eligible bid requests, отправляет 45,000 bids, получает 9,000 wins; 8,000 событий становятся counted/billable impressions по выбранному contract. Поэтому её 8,000 billable impressions совпадают с 8,000 counted impressions advertiser; в реальности и это совпадение не гарантировано.

```text
bid rate = 45,000 / 60,000 × 100% = 75%
win rate = 9,000 / 45,000 × 100%  = 20%
```

Разница между 9,000 wins и 8,000 counted/billable impressions не обязана быть ошибкой: win и billing/delivery — разные event points. При этом 60,000 platform requests не обязаны равняться 100,000 publisher requests из-за границ измерения, routing, batching, fan-out и filters.

| Перспектива | Наблюдаемый срез | Главные решения | Денежный смысл |
|---|---|---|---|
| Advertiser | Купленные impressions, clicks, attributed outcomes | Эффективность acquisition и value | Spend/cost и attributed value |
| Publisher | Все eligible requests и demand sources | Delivery и monetization | Recognized publisher revenue |
| Platform | Traversed requests, bids, wins и её billing events | Auction participation и граница delivery | Собственные revenue, spend или downstream cost в конкретном реестре |

Data flow и money flow здесь расходятся. Impression/click/conversion events могут поступать asynchronously в разные reports; invoice и settlement не обязаны следовать тому же network path. Арифметическая согласованность внутри каждого metric contract не доказывает равенство raw events между системами. Для первичной диагностики снова нужны семь вопросов из первой секции. Детальная reconciliation относится к главе 32.

## С чем это часто путают

- **Opportunity, ad request и bid request — не один event.** Opportunity возникает на media surface; requests являются system-bound messages с batching, fan-out, retries и filtering.
- **Impression не означает человеческий просмотр.** Served, rendered, measurable и viewable дают разные уровни доказательства; viewable означает standardized opportunity to see, не attention.
- **Non-viewable не равно non-measurable.** В первом случае measurement завершился и criteria не выполнены; во втором status определить не удалось.
- **CPM не равен eCPM, CPA не равен CAC.** Первая пара различается ledger perspective; вторая — action/customer definition и cost scope.
- **ROAS не равен ROI.** ROAS нормализует attributed value на ad spend; ROI использует net profit и полный выбранный investment cost.
- **Fill rate и win rate не являются одной auction metric с двух сторон.** Fill относится к publisher delivery, win — к переходу bid → win по раскрытому auction contract.

## Что важно запомнить

1. Метрика — contract измерения, а не только название и формула.
2. Reach требует определения единицы аудитории и universe; frequency — общего impression basis, reached совокупности и period.
3. CTR и особенно CVR сравнимы только при названных числителях, знаменателях и filters; CVR называется как конкретный переход.
4. CPM/CPC/CPA/CPI/CPL могут быть ценой по договору, bid/target или фактическими averages; eCPM обычно нормализует seller revenue.
5. Conversion, ROAS и attributed revenue зависят от attribution rules; attribution не равна causality.
6. ARPU, ARPPU и LTV требуют user, revenue, cohort, period/horizon и model definitions.
7. Advertiser, publisher и platform могут иметь одновременно правильные, но разные отчёты об одной campaign: они видят разные границы и реестры, и одна сумма (spend, cost, revenue) меняет название при переходе границы.

## Проверьте себя

1. Одна opportunity породила три downstream bid requests. Какой count описывает media event, а какой — protocol messages?
2. Почему `CVR = 15%` нельзя сравнить с другим `CVR = 12%`, пока не раскрыты denominators и conversion rules?
3. Как campaign с `5.0x ROAS` может иметь отрицательный ROI?
4. Какие metric contracts позволяют одновременно получить advertiser CPM `$12`, publisher eCPM `$10` и platform win rate `20%` без противоречия?

## Источники и дополнительное чтение

1. [MRC — Standards & Guidelines](https://www.mediaratingcouncil.org/standards-and-guidelines)
2. [MRC/IAB — Desktop Display Impression Measurement Guidelines v1.1](https://www.mediaratingcouncil.org/sites/default/files/Standards/Desktop-Display-Impression-Measurement-Guidelines-US%20%28MMTF%20Final%20v1.1%29.pdf) и [MRC — Viewable Ad Impression Measurement Guidelines v2.0](https://mediaratingcouncil.org/sites/default/files/Standards/081815%20Viewable%20Ad%20Impression%20Guideline_v2.0_Final.pdf)
3. [MRC/IAB — Digital Audience-Based Measurement Standards, Final 1.0](https://www.mediaratingcouncil.org/sites/default/files/Standards/MRC%20Digital%20Audience-Based%20Measurement%20Standards%20Final%201.0.pdf)
4. [IAB/MRC — Click Measurement Guidelines v1.0](https://www.mediaratingcouncil.org/sites/default/files/Standards/click-measurement-guidelines2009-2.pdf)
5. [MRC — Outcomes and Data Quality Standards](https://www.mediaratingcouncil.org/sites/default/files/Standards/MRC%20Outcomes%20and%20Data%20Quality%20Standards%20%28Final%29.pdf)
6. [IAB Tech Lab — Programmatic Auction Definitions](https://github.com/InteractiveAdvertisingBureau/programmatic-auction-definitions/blob/main/auction%20definitions.md) (финальная версия от 24 июня 2026 года) и [OpenRTB 2.x](https://iabtechlab.com/standards/openrtb/)
7. [Google Ad Manager — Sell-through](https://support.google.com/admanager/answer/7304688?hl=en) и [Report metrics](https://support.google.com/admanager/table/7568664?hl=en) (проверено 27 августа 2026 года; Reports tool с тех пор заменён Interactive reports)
8. [Google Ads — CTR](https://support.google.com/google-ads/answer/2615875?hl=en), [Conversion rate](https://support.google.com/google-ads/answer/2684489?hl=en), [ROI](https://support.google.com/google-ads/answer/1722066?hl=en), [Google Analytics Data API schema](https://developers.google.com/analytics/devguides/reporting/data/v1/api-schema) и [GA4 User lifetime](https://support.google.com/analytics/answer/9947257?hl=en) (проверено 27 августа 2026 года)