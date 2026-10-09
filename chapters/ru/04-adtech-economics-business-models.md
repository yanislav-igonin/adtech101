---
id: ch-04
type: chapter
part: I
chapter: 4
slug: adtech-economics-business-models
title: "Экономика и бизнес-модели AdTech"
language: ru
status: reviewed
toc_requirements: ["4.1", "4.2", "4.3", "4.4", "4.5", "4.6", "4.7", "4.8", "4.9", "4.10", "4.11", "4.12", "4.13", "4.14", "4.15"]
prerequisites: [ch-01, ch-02, ch-03]
---

# Экономика и бизнес-модели AdTech

## Суть: цена следует договору, а не метке в dashboard

`CPM`[^g-cpm], `CPC`[^g-cpc] или `CPA`[^g-cpa] в интерфейсе ещё не объясняет, за что платят. Одна и та же метка может быть договорной ценой, `bid`[^g-bid], optimization target[^g-optimization-target] или фактическим средним после событий. Денежное обязательство создаёт договорная **pricing basis**[^g-pricing-basis] вместе с определением **billable event**[^g-billable-event] — qualifying-события, после которого можно начислить сумму. Даже auction win[^g-auction] сам по себе не обязан быть billable (в programmatic-покупке[^g-programmatic], главы 15–18).

Чтобы прочитать экономику сделки, разложите её на шесть независимых слоёв:

| Слой | Главный вопрос | Пример |
|---|---|---|
| Contractual pricing | За какую basis договорились платить? | `$10 CPM` за тысячу qualifying impressions[^g-impression] |
| Billing | Какое событие создаёт charge и какую сумму? | Render или иной billing signal по contract policy |
| Optimization | Какой outcome меняет будущие решения системы? | `target CPA` по подписке |
| Participant ledger[^g-ledger-boundary] | Для кого сумма является spend[^g-media-spend], cost, payout или retained amount[^g-retained-amount]? | `$100` spend advertiser[^g-advertiser]; `$80` media cost[^g-cost] посредника[^g-intermediary] |
| Представление в отчётности | Что конкретная компания признаёт revenue[^g-revenue] и cost? | Представление gross или net |
| Settlement[^g-settlement] | Когда начисление стало invoice, а обязательство — cash? | Month-end invoice, оплаченный позже |

Числа `$100` и `$80` — из сквозного примера главы: managed network[^g-ad-network] (ad network, которая сама закупает media и продаёт advertiser готовый результат) перепродаёт за `$100` media, купленное за `$80`; полный разбор — в разделе «Путь учебных `$100`».

**Pricing basis** — договорное правило расчёта цены: за impression, click[^g-click], action, долю proceeds[^g-proceeds], период доступа к software или иной согласованный объект. **Billable amount** — начисленная по этому правилу сумма после counts, rates, validation и договорных adjustments. Она ещё не обязательно выставлена в invoice, признана как revenue или оплачена cash.

Эта декомпозиция объясняет всю главу: стороны выбирают не красивую метрику, а границу наблюдаемого события, цену и распределение риска; затем каждая сторона записывает результат в собственный ledger.

## CPM, CPC и outcome pricing: кто несёт риск до следующего события

Воронка от ad opportunity[^g-ad-opportunity] может остановиться после любого шага:

```text
opportunity → qualifying impression → qualifying click → install/lead/action → business value
```

Чем глубже billable event, тем дольше payee[^g-payee-payer] — сторона, ожидающая оплату, — финансирует delivery без гарантии charge. Но риск не «переезжает» целиком: после оплачиваемого события buyer всё ещё рискует качеством следующего результата.

| Модель оплаты | Договорный billable event | Риск payee до charge | Риск advertiser после charge | Что обязательно определить |
|---|---|---|---|---|
| **CPM** | Тысяча qualifying impressions | Получить и подтвердить выбранный impression event | Click, conversion[^g-conversion] и последующая ценность могут не возникнуть | `served`[^g-served-impression], `rendered`[^g-rendered-impression], `viewable`[^g-viewable-impression] или иная impression basis; filters и кто ведёт count |
| **CPC** | Qualifying click | Impressions могут не привести к click | Click может оказаться некачественным и не дать conversion | Click point, user initiation, deduplication, invalid-click filters |
| **CPA** | Согласованный action, например оплаченная подписка | Довести user до action и получить valid attribution[^g-attribution]/validation | Action может иметь низкую margin, retention или lifetime value[^g-ltv] | Точное имя action, attribution rule, validator, approval state |
| **CPI**[^g-cpi] | Valid attributed install | Delivery и clicks могут не привести к засчитанному install | Install может не запуститься, не удержаться и не монетизироваться | Install definition, кто проводит attribution/validation, reinstall policy |
| **CPL**[^g-cpl] | Qualifying lead | Traffic может не породить принятый lead | Lead может не пройти дальнейшую qualification или не стать customer | Поля и criteria lead, duplicate/rejection rules, кто принимает lead |

Таблица показывает сдвиг риска, а не его исчезновение: чем глубже billable event, тем больше delivery, conversion и measurement[^g-measurement] risk принимает payee, но advertiser сохраняет риск качества и монетизации результата. Fraud, attribution disputes и caps могут менять accepted count; их mechanics рассматриваются позднее.

`Billable event` задаётся contract policy, а не протоколом автоматически. В programmatic flow IAB Tech Lab различает auction win и событие, после которого auction становится billable. OpenRTB также разделяет win notice (`nurl`) и billing notice (`burl`): win не гарантирует delivery, а billing signal зависит от policy publisher[^g-publisher] или exchange[^g-ad-exchange]. Это programmatic-пример общего правила, не универсальный contract для любой рекламы.

Одинаковый учебный billable amount `$100` можно получить по пяти **альтернативным**, а не одновременным договорам:

| Договор | Объём qualifying-событий и ставка | Где проходит граница риска |
|---|---:|---|
| CPM | 10,000 impressions по `$10 CPM` → `$100` | Impression |
| CPC | 200 clicks по `$0.50 CPC` → `$100` | Click |
| CPI | 20 installs по `$5 CPI` → `$100` | Attributed install |
| CPL | 25 leads по `$4 CPL` → `$100` | Accepted lead |
| CPA | 10 subscriptions по `$10 CPA` → `$100` | Attributed subscription |

Равная сумма не означает равный риск. В CPM buyer уже должен `$100`, даже если подписок нет. В CPA за подписку payee не получает charge за impressions и clicks, которые не дошли до accepted action.

Модель выбирают по тому, кто какие события видит и чьему count доверяет. Publisher и SSP[^g-ssp] наблюдают impression в своих системах, но не видят install или подписку внутри приложения advertiser, поэтому обычно продают по CPM — billable event лежит внутри их границы измерения. Advertiser, который не доверяет качеству чужого traffic, но готов отдавать postback о конверсиях, переносит billable event глубже — на CPI или CPA — и перекладывает delivery risk на payee, обычно в обмен на более высокую цену за событие. Чем глубже событие, тем сильнее payee зависит от чужого count, поэтому договор обязан назвать validator и правила rejection.

### Billing, optimization и фактическая метрика — разные объекты

Представим product-specific flow: advertiser фактически оплачивает qualifying clicks, а bidding system оптимизирует решения под `target CPA`. После периода dashboard может вычислить фактические CPM, CPC и CPA из фактических spend и events.

```text
optimization target: target CPA по подписке
billing basis:       CPC за qualifying click
фактические метрики: observed CPM, CPC и CPA после периода
```

Здесь `target CPA` не превращает договор в CPA billing. `Bid` также выражает decision input или willingness to pay, а не доказывает фактический charge. Payment model устанавливает contract; фактическое среднее описывает уже случившееся; optimization target влияет на будущие decisions.

## Как зарабатывают intermediaries и software providers

Посредник может удерживать часть media transaction, перепродавать media с markup[^g-markup] или получать отдельную оплату за service/software. Эти модели нельзя складывать, пока не известны граница договора и база расчёта.

| Модель | Кто платит | Правило расчёта | Связь с media dollar | Основной риск или оговорка |
|---|---|---|---|---|
| **Revenue share**[^g-revenue-share] | Сторона, передающая proceeds по договору | Доля от названной revenue/proceeds base за период | Обычно делит сумму на конкретной media-границе | База, допустимые deductions и adjustments должны быть названы |
| **Fixed fee**[^g-fixed-fee] | Клиент service provider | Заранее согласованная сумма за период, объём работ или deliverable | Обычно полностью отдельная | Provider несёт риск, что согласованный объём потребует больше работы |
| **SaaS pricing**[^g-saas-pricing] | Customer software platform | Subscription, seats, usage tier или processed volume | Обычно отдельный software/service flow | Usage event не становится media event автоматически |
| **Markup** | Buyer платит selling price посреднику | Spread[^g-spread] относительно acquisition/base cost | Да, если посредник перепродаёт media | Процент считается от cost (acquisition cost в знаменателе), а не от selling amount |
| **Take rate**[^g-take-rate] | Зависит от границы | Retained amount / названный transaction flow | Обычно характеризует удержание на выбранной границе | Без numerator, denominator и включённых fees ставка несравнима |

### Revenue share: процент без базы не определён

**Proceeds** — сумма поступлений по transaction до согласованного распределения на выбранной границе. **Revenue share** — договорное распределение названной revenue или proceeds base. Договор должен ответить: чьи proceeds, на какой границе, за какой период, до или после каких согласованных adjustments и кто выполняет расчёт.

В основном примере SSP получает на своей границе `$80 gross proceeds` и по seller contract удерживает 15%:

```text
SSP retained amount = $12 / $80 SSP-boundary proceeds = 15%
publisher share      = $68 / $80 SSP-boundary proceeds = 85%
```

Numerator первого процента — `$12`, denominator — `$80`. Это не 15% исходного advertiser spend `$100`: относительно исходных `$100` те же `$12` составляют 12%. Слово `gross` здесь описывает transaction base до split, а не автоматически `gross revenue`[^g-gross-net-revenue] в финансовой отчётности.

### Markup, spread и take rate

**Spread** — абсолютная разница между selling amount и acquisition/downstream amount на названной границе. Если managed network покупает media за `$80` и продаёт advertiser за `$100`, spread равен `$20`.

**Markup** измеряет надбавку к base cost:

```text
network markup = $20 spread / $80 acquisition cost = 25%
```

**Take rate** измеряет retained amount относительно названного transaction flow на той же границе:

```text
network take rate = $20 retained / $100 advertiser spend = 20%
```

`25% markup` и `20% take rate` описывают один `$20 spread` с разными denominators. Ни один процент нельзя сравнивать с чужой ставкой без границы участника, numerator, denominator и перечня включённых fees. `Markup` также не равен gross margin[^g-gross-margin]: gross margin использует accounting revenue и cost of revenue[^g-cost-of-revenue], а не произвольно выбранные buy/sell amounts.

### Fixed fee и SaaS: отдельные money flows

**Fixed fee** не зависит от объёма media transaction. Типовые случаи: agency[^g-agency] retainer за ведение campaigns[^g-campaign]; setup или managed-service fee; minimum monthly commitment, который клиент платит даже при недоборе объёма; flat sponsorship fee за размещение на период. Её выбирают ради предсказуемости бюджета и чтобы снять конфликт incentives «fee растёт вместе со spend»: провайдеру с процентом от spend выгодно тратить больше. Риск распределяется иначе, чем в media-моделях: provider рискует тем, что согласованный объём работ потребует больше усилий, клиент — тем, что заплатит ту же сумму при низком объёме или слабом результате.

Рядом с media flow часто идёт SaaS-поток. Допустим, advertiser платит ad server[^g-ad-server] или measurement platform `$2,000/month` за software access. Договор оформляет это одним из двух способов: фиксированные `$2,000/month` независимо от объёма (fixed fee) или usage tier, где сумма зависит от числа обработанных impressions (usage pricing, а не fixed fee — но и не CPM-покупка inventory[^g-inventory]). В обоих вариантах сумма:

- является service/software charge по отдельному договору;
- не вычитается из учебных `$100 media flow`;
- не становится publisher payout[^g-publisher-payout] или intermediary take rate.

Включать `$2,000` в media dollar можно только если конкретный договор действительно объединяет эти charges. Иначе получатся два money flows: media transaction и SaaS subscription.

## Одна сделка, разные ledgers и моменты времени

**Ledger** — записи конкретной стороны о начисленных суммах и обязательствах. Один transaction не имеет единственной нейтральной денежной метки: вход одной стороны является выходом другой, а посредник одновременно продаёт upstream и покупает downstream. Одна и та же сумма меняет метку по цепочке:

```text
advertiser:    $100 spend / media cost
  → network:   $100 billed (receivable) | $80 downstream media cost (payable)
  → SSP:       $80 proceeds (receivable) | $68 publisher payout (payable)
  → publisher: $68 receivable
```

- **Advertiser spend** — сумма, начисленная advertiser за выбранный состав media/service. Dashboard может включать или исключать platform/data fees, taxes, credits и adjustments; состав нужно назвать.
- **Media cost** — стоимость приобретённого media для конкретной стороны: для advertiser в нашем узком примере `$100`, для network — downstream acquisition cost `$80`. Без указания владельца `media cost` не определён.
- **Publisher payout** — сумма, которую по seller contract должны перечислить publisher после share, fees и adjustments. Для SSP это payable; для publisher — receivable и часть его economics, а какую часть и в каком периоде он признаёт publisher revenue[^g-publisher-revenue], определяет его accounting policy.

**Receivable** — сумма, которую counterparty должна компании. **Payable** — сумма, которую компания должна поставщику или другой стороне. Эти слова описывают направление обязательства, не момент движения cash.

Полезно различать состояния:

```text
accrued  → qualifying events сверены; amount заработан или понесён по contract
billed   → amount включён в invoice; появился формальный запрос оплаты
settled  → обязательство погашено cash или иным согласованным способом
```

Taxes, credits, refunds и FX могут изменить invoiced или settled amount, но их mechanics здесь не рассматриваются.

### Поток событий и данных

```text
10,000 qualifying impressions
  → contract-specific billable count у network и SSP
  → participant event records с собственными measurement boundaries
  → period reconciliation
  → ledger amounts: $100, $80 и $68 на разных boundaries
```

Events могут идти от publisher-/sell-side systems к buyers и reporting systems асинхронно. Они доказывают basis для расчёта, но сами деньги по этому пути не передают.

### Поток invoice и cash

```text
network → invoice $100 → advertiser
SSP     → invoice $80  → network
SSP     → statement $68 → publisher   (или invoice publisher → SSP по договору)

позднее cash:
advertiser → $100 → network → $80 → SSP → $68 → publisher
```

Кто выставляет invoice и как устроен settlement, задаёт договор; путь событий, путь invoice и путь cash не обязаны совпадать по направлению, участникам или времени.

## Gross/net revenue и gross margin: отдельная граница учёта

**Отчитывающаяся компания** — та, чью финансовую отчётность мы читаем. **Recognized revenue** — сумма, которую она отражает как revenue по применимой accounting policy; это не любой invoice, collection или поступление cash. **Gross billings**[^g-gross-billings] — более широкая сумма, выставленная клиентам или прошедшая через collection до исключения supplier components; gross billings не синоним recognized revenue.

`Gross revenue` и `net revenue` — не «деньги до расходов» и «деньги после расходов». Представление в отчётности зависит от того, является ли компания **principal**[^g-principal-agent] или **agent** относительно конкретного обещанного товара или service:

- **Specified good/service** — конкретное обещание customer, которое оценивают: например, предоставить рекламную delivery или организовать доступ к supply[^g-supply].
- **Principal** контролирует specified good/service до передачи customer; при таком выводе согласованную оплату обычно показывают gross как revenue, а supplier component — отдельно по применимой cost policy.
- **Agent** организует предоставление specified good/service другой стороной; при таком выводе revenue обычно равен net fee или commission.
- **Control** здесь означает способность направлять использование и получать практически все выгоды до передачи, а не наличие API, invoice или названия продукта.

```text
Что компания обещала customer?
  → какой specified good/service передаётся?
  → контролировала ли компания его до передачи?
      вывод principal → обычно revenue показывают gross
      вывод agent     → обычно показывают net fee/commission
```

`Primary responsibility`, `inventory risk` и `pricing discretion` могут служить признаками, но не образуют механический балльный тест. Вывод делается для конкретного обещания и transaction: одна AdTech-компания[^g-adtech] может быть principal в одном flow и agent в другом.

### Одна экономика сделки, два взаимоисключающих представления

Возьмём только границу network: `$100 sell / $80 supplier component`. Таблица иллюстративная; в реальной отчётности нельзя выбрать представление ради более красивой margin.

| Иллюстративный вывод | Recognized revenue | Supplier component как cost of revenue | Gross profit до прочих CoR | Gross margin до прочих CoR |
|---|---:|---:|---:|---:|
| Principal / gross | `$100` | `$80` | `$20` | `20%` |
| Agent / net | `$20` fee | `$0` (supplier `$80` вне revenue и CoR) | `$20` | `100%` |

**Cost of revenue (CoR)** — расходы, которые отчитывающаяся компания классифицирует как непосредственно связанные с получением признанного revenue по своей policy. Это не любой cash outflow. **Gross profit** и **gross margin** считаются на одной компании и одной accounting basis:

```text
gross profit = recognized revenue − cost of revenue
gross margin = (recognized revenue − cost of revenue) / recognized revenue
```

В net row `100%` — механический результат учебной изоляции: `$20 recognized revenue` и `$0` прочих показанных cost of revenue. Это не benchmark и не утверждение, что platform работает бесплатно: реальная компания несёт infrastructure, data и operations расходы, часть которых может относиться к cost of revenue по её policy, а operating expenses, interest и taxes лежат ниже gross profit и тоже не превращают retained amount в profit.

Численное совпадение gross margin `20%` в gross row с network take rate `20%` тоже учебное: оба раза считается `$20 / $100`, потому что прочих cost of revenue нет. Определения разные: take rate делит retained amount на transaction flow, а gross margin — gross profit на recognized revenue той же компании; при представлении net та же экономика даёт `100%` margin при тех же `20%` take rate.

Публичные filings показывают contract-specific природу этой границы:

- Magnite в Form 10-K за 2025 год описывала представление net для большинства platform transactions — компания не контролирует inventory и не устанавливает auction price — и представление gross для некоторых insertion-order campaigns, где считает себя primary obligor по delivery.
- The Trade Desk в Form 10-K за 2025 год отделяла gross billings и связанные receivables/payables от net recognized revenue при выводе agent по supplier components.

Это примеры policies конкретных компаний и периода, не универсальная классификация SSP или DSP[^g-dsp]. ASC 606, IFRS 15, договор и профессиональное accounting judgment определяют реальный вывод; глава даёт mental model, а не accounting advice.

## Arbitrage: spread в обмен на принятый риск

**Arbitrage**[^g-arbitrage] в широком AdTech-смысле возникает, когда intermediary покупает media/traffic дешевле и продаёт дороже либо покупает на одной pricing basis, а продаёт на другой. Его economics зависят от spread и риска между границами.

Простой вариант:

```text
network покупает batch media за $80
network продаёт тот же agreed scope advertiser за $100
buy/sell spread = $20
```

В основном примере главы network покупает per-impression по `$8 CPM` и платит только за фактически доставленные impressions: volume risk она не несёт, остаётся price risk. Volume risk появляется при предоплаченном batch или guaranteed commitment: если network обязалась заплатить downstream `$80`, но не продала весь согласованный объём или customer не принял delivery, spread уменьшается или становится loss. Тогда она несёт inventory/volume, fulfillment и reconciliation risk в объёме, заданном contracts.

**Basis mismatch**[^g-basis-mismatch] добавляет performance risk. Intermediary может покупать impressions по CPM, а продавать clicks или actions по CPC/CPA. Его revenue тогда зависит от фактических CTR[^g-ctr]/CVR[^g-cvr] и validation. Если clicks или actions возникают хуже ожиданий, исходная media cost остаётся, а downstream billable amount не покрывает её.

Не любой intermediary fee является arbitrage, и arbitrage не автоматически означает злоупотребление. Прозрачные fee, revenue share или resale spread могут оплачивать aggregation, reach[^g-reach], service и принятый риск. Проблема opacity возникает, когда customer не понимает buy/sell basis, величину spread, функцию посредника или конфликт incentives. Исследование CMA 2020 года иллюстрирует этот механизм в UK open display, но его rates нельзя использовать как актуальный benchmark.

## Путь учебных `$100` от advertiser до publisher

Соберём слои в одном scenario. Subscription-app advertiser покупает media в mobile publisher app через managed network и SSP. Все числа **учебные**, не market benchmark и не заявление о типичной длине цепочки.

Допущения:

- 10,000 одинаковых qualifying billable impressions нужны только для изоляции economics;
- advertiser/network договор использует `$10 CPM`, network/SSP — `$8 CPM`;
- SSP/publisher договор делит `$80` proceeds: 15% SSP, 85% publisher;
- валюта — USD; taxes, FX, refunds, rebates, fraud adjustments и credit risk исключены;
- amounts accrued после reconciliation, но invoices и cash ещё не settled;
- отдельные `$2,000/month` SaaS в media flow не входят.

### Арифметика договоров

```text
Advertiser → network: 10,000 / 1,000 × $10 CPM = $100
Network → SSP:        10,000 / 1,000 ×  $8 CPM =  $80
Network spread:                                 =  $20
SSP retained share:             15% × $80       =  $12
Publisher payout:               85% × $80       =  $68
Проверка:                      $20 + $12 + $68   = $100
```

На одном исходном рекламном долларе contract economics составляют 20 центов retained network, 12 центов retained SSP и 68 центов publisher payout. В полном примере intermediary retained amount равен `$20 + $12 = $32`. Это разложение конкретных contracts, не отраслевой benchmark и не accounting profit.

### Знаменатели

```text
network markup on acquisition cost = $20 / $80  = 25%
network take on advertiser spend    = $20 / $100 = 20%
SSP take on its boundary            = $12 / $80  = 15%
SSP share of original spend         = $12 / $100 = 12%
combined intermediary share         = $32 / $100 = 32%
publisher payout share              = $68 / $100 = 68%
```

Каждая строка называет numerator и denominator; поэтому `SSP take = 15%` и `SSP share of original spend = 12%` одновременно верны и отвечают на разные вопросы.

### Ledger каждого участника

| Участник | Договорная basis | Поступление / receivable | Выплата / payable | Экономический остаток | Чего запись не доказывает |
|---|---|---:|---:|---:|---|
| Advertiser | `$10 CPM` × 10,000 | — | `$100` advertiser spend/media cost | — | Invoice date, cash date или business return |
| Managed network | Customer charge `$100`; downstream `$8 CPM` | `$100` billed/receivable | `$80` downstream media cost/payable | `$20` spread | Что `$100` — recognized revenue или `$20` — profit |
| SSP | Revenue-share base `$80` | `$80` proceeds на границе SSP/receivable | `$68` publisher payout/payable | `$12` retained amount | Что `$80` — recognized revenue или 15% относится к `$100` |
| Publisher | 85% proceeds на границе SSP | `$68` payout receivable | — | `$68` publisher economics | Что amount уже settled cash или как именно признан revenue |

Метки меняются не из-за несогласованности, а из-за разных отчитывающихся компаний и counterparties. `Transaction amount`, `retained amount`, `recognized revenue`, `gross profit`, `invoice` и `cash` отвечают на разные вопросы — о договоре, удержании, отчётности, прибыльности, предъявленном требовании и расчёте; ни одна запись не доказывает соседнюю.

### Чеклист анализа экономики vendor

1. Назовите customer, payer, payee, counterparties и обещанный product/service.
2. Зафиксируйте pricing basis, qualifying billable event, rate, того, кто проводит validation, и billable amount; отдельно — optimization target и фактические метрики.
3. Нарисуйте ledgers участников: где находятся advertiser spend, media cost, publisher payout, receivable и payable.
4. Для каждой fee или доли укажите абсолютную сумму, numerator, denominator, границу и допустимые adjustments; отделите media money от fixed/SaaS charge.
5. Проверьте accounting policy для конкретного transaction type: specified good/service, вывод principal/agent, recognized revenue и cost of revenue; затем считайте gross profit и gross margin.
6. Поставьте на timeline accrual, reconciliation, invoice и cash settlement; не выводите представление в отчётности из того, кто выставляет invoice, или из направления платежа.

## С чем это часто путают

- **Pricing model, optimization target и фактическая метрика — не одно и то же.** `Target CPA` может управлять bids при CPC billing, а observed CPA вычисляться только после периода.
- **Auction win не обязательно является billable event.** Charge возникает после события и validation, заданных договором; win notice и billing notice могут быть разными signals.
- **Процент без numerator и denominator не определён.** SSP share `15%` от `$80` — те же `$12`, что и 12% от исходных `$100`; один spread `$20` даёт `25% markup` на cost `$80` и `20% take rate` на spend `$100`.
- **Gross/net revenue — не «до/после расходов».** Представление следует contract-specific principal-agent assessment; invoice и gross billings сами по себе вывод не определяют.
- **Gross margin не равна take rate.** Первая использует recognized revenue и cost of revenue одной отчитывающейся компании; вторая — retained amount и названный transaction flow. В учебном gross row они совпадают численно (`20%`), но не по определению.
- **Любой посреднический доход не является arbitrage.** Arbitrage предполагает buy/sell spread или basis mismatch и соответствующий risk; прозрачная fee или revenue share могут оплачивать отдельную функцию.

## Что важно запомнить

1. Экономика начинается с договора: pricing basis и billable event определяют charge и распределяют риск; модель выбирают по тому, кто видит событие и чьему count доверяет.
2. Revenue share, markup и take rate сравнимы только после раскрытия numerator, denominator и границы участника.
3. Один flow `$100 → $80 → $68` одновременно создаёт advertiser spend, media cost посредника и publisher payout; retained `$20` и `$12` — transaction economics, а не автоматически recognized revenue или profit.
4. Fixed fee и SaaS pricing — отдельный money flow; media dollar они уменьшают только если договор их объединяет.
5. Представление gross или net определяется для specified good/service через principal-agent assessment, а не по названию продукта; gross profit и gross margin считаются на recognized revenue и cost of revenue одной компании.
6. Arbitrage приносит spread в обмен на volume, performance или reconciliation risk и может дать loss.
7. Поток событий, ledgers участников, поток invoice и cash settlement анализируются отдельно; учебное `$20 + $12 + $68 = $100` показывает метод, а не типичную рыночную долю.

## Проверьте себя

1. Advertiser оптимизирует campaign под `target CPA`, но платит за qualifying clicks. Какие здесь pricing basis, billable event, optimization target и фактическая метрика?
2. Почему `$20 / $80 = 25%` и `$20 / $100 = 20%` могут одновременно правильно описывать economics network?
3. Может ли компания выставить invoice на `$100`, признать `$20 net revenue` и позднее получить `$100 cash` без противоречия? Какие слои описывает каждая сумма?
4. Какие contract, ledger, accounting и settlement данные нужны, прежде чем сравнивать gross margin и take rate двух AdTech vendors?

## Источники и дополнительное чтение

1. [IAB Tech Lab — Programmatic Auction Definitions, Final](https://github.com/InteractiveAdvertisingBureau/programmatic-auction-definitions/blob/main/auction%20definitions.md) и [OpenRTB 2.x Implementation Guidelines, sections 7.8–7.9](https://github.com/InteractiveAdvertisingBureau/openrtb2.x/blob/main/implementation.md) — definitions `Billable Event`, transaction ledger и distinction между `nurl` и `burl`; protocol guidance не заменяет договорную billing policy.
2. [Google Ads — CPC](https://support.google.com/google-ads/answer/116495?hl=en), [CPM](https://support.google.com/google-ads/answer/6310?hl=en) и [Bidding basics](https://support.google.com/google-ads/answer/2459326?hl=en) — product-specific примеры pricing и optimization; это не vendor-neutral contract.
3. [FASB — Revenue from Contracts with Customers, Topic 606, paragraphs 606-10-55-36–55-40](https://asc.fasb.org/layoutComponents/getPdf?fileName=GUID-E90460CF-B750-4654-B149-5DD3F6B6DBA9.pdf&isSitesBucket=false) и [IASB — IFRS 15 PIR: Principal versus Agent Considerations, AP6B](https://www.ifrs.org/content/dam/ifrs/meetings/2024/february/iasb/ap6b-ifrs-15-pir-principal-vs-agent-considerations.pdf) — principal-agent mental model; применение зависит от reporting framework, договора и professional judgment.
4. [FASB — GAAP Taxonomy Implementation Guide: Revenue from Contracts with Customers](https://xbrl.fasb.org/impguidance/Rev2_TIG/revenue_2.pdf) — gross profit как difference между revenue и cost of revenue/cost of goods sold; состав cost of revenue остаётся company-specific.
5. [Magnite — Form 10-K за год, завершившийся 2025-12-31](https://www.sec.gov/Archives/edgar/data/1595974/000159597426000007/mgni-20251231.htm) — company-specific примеры percentage, fixed CPM/monthly pricing и разных gross/net presentations; не отраслевой benchmark.
6. [The Trade Desk — Form 10-K за год, завершившийся 2025-12-31](https://www.sec.gov/Archives/edgar/data/1671933/000167193326000014/ttd-20251231.htm) — distinction между platform fee, gross billings, receivables/payables и net revenue; выводы относятся к contracts и policy этой компании.
7. [UK Competition and Markets Authority — Appendix M: Intermediation in open display advertising](https://assets.publishing.service.gov.uk/media/5fe495c28fa8f56afaf406d4/Appendix_M_-_intermediation_in_open_display_advertising_WEB.pdf) и [official landing page](https://www.gov.uk/find-digital-market-research/online-platforms-and-digital-advertising-market-study-appendix-m-intermediation-in-open-display-advertising-2020-cma) — исторический анализ UK open display 2020 года; описывает mechanism arbitrage и fee opacity, но его rates нельзя использовать как current benchmark 2026 года.

Источники проверены 2026-08-28.
