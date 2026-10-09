---
id: ch-02
type: chapter
part: I
chapter: 2
slug: adtech-ecosystem-participants
title: "Участники рекламной экосистемы"
language: ru
status: reviewed
toc_requirements: ["2.1", "2.2", "2.3", "2.4", "2.5", "2.6", "2.7", "2.8", "2.9", "2.10", "2.11", "2.12", "2.13", "2.14", "2.15", "2.16", "2.17"]
prerequisites: [ch-01]
---

# Участники рекламной экосистемы

## Суть: роли, а не коробки

В первой главе мы увидели две экономические стороны рынка: `advertiser`[^g-advertiser] создаёт demand[^g-demand], а `publisher`[^g-publisher] — supply[^g-supply]. Между ними может быть много систем, но карта AdTech[^g-adtech] становится понятной, если смотреть не на названия компаний, а на **роли** — логические функции в рекламной сделке.

`Role`, `company` и `product` — разные уровни:

- **role** — функция, которую здесь выполняют;
- **company** — организация, с которой заключают договор; она может выполнять несколько ролей;
- **product** — конкретное предложение компании: UI, API, managed service или набор инструментов.

Поэтому логотип нельзя навсегда поставить в одну клетку карты: один product suite может покупать media, продавать доступ к inventory[^g-inventory], доставлять рекламу и строить отчётность, а одну роль advertiser может распределить между собственной командой и несколькими providers.

Для разбора любой роли используйте одну карточку (role card):

| Вопрос | Что он проясняет |
|---|---|
| Какую проблему решает роль? | Причина её существования |
| Кто customer? | Кто использует продукт или услугу |
| Кто beneficiary? | Кто получает экономическую пользу |
| Кто payer?[^g-payee-payer] | Кто оплачивает media или сервис по договору |
| Какие данные входят и выходят? | Технические границы функции |
| Какое решение принимается или исполняется? | Реальная работа, а не marketing label |
| Как движутся деньги? | Media money, отдельная fee или отсутствие платежа в этом flow |

Customer, beneficiary и payer могут не совпадать: media buyer[^g-media-buyer] работает в UI платформы, пользу получает advertiser, а invoice оплачивает agency[^g-agency]. Без этого различия трудно читать договоры, data flows и отчёты.

Заполним карточку для главного экономического участника. Advertiser хочет изменить знание или поведение аудитории, финансирует campaign[^g-campaign], передаёт цель, бюджет и **creative**[^g-creative] — сам рекламный материал: изображение, видео или текст — и получает outcomes и отчётность. Advertiser обычно является beneficiary и источником денег, но операционную работу и оплату конкретных счетов может делегировать agency. В конкретной campaign некоторых ролей не будет, а другие скроются за одним договором — поэтому карточка полезнее линейной схемы из семнадцати обязательных коробок.

## Кто ставит цель и кто выполняет покупку

**Advertiser** — организация, которая финансирует рекламу ради business outcome. Для приложения с платной подпиской outcome может быть немедленным — trial или оплаченная подписка — либо более отложенным: знание продукта и готовность рассмотреть его позже. Advertiser определяет цель, допустимый spend, аудиторию и критерии успеха; сам или через подрядчиков решает, где покупать media.

Отсюда появляются две рекламные ориентации:

- **brand advertising**[^g-brand-advertising] в первую очередь меняет awareness, consideration или perception — знание, рассмотрение и отношение к продукту;
- **performance advertising**[^g-performance-advertising] управляется вокруг измеримого действия или outcome и стоимости его получения: регистрации, trial, установки или покупки.

Это не два взаимоисключающих вида компаний. Один subscription app может одновременно показывать video campaign для знакомства с брендом и acquisition campaign, оптимизированную на trial. Более того, один пользователь может сначала познакомиться с продуктом через brand-рекламу, а позже отреагировать на performance-рекламу. Различаются прежде всего цель, горизонт оценки и ожидаемые доказательства результата.

**Publisher** — организация, которая владеет или управляет media-средой, где возникают рекламные opportunities[^g-ad-opportunity]: сайтом, приложением, игрой или видеосервисом. Publisher задаёт placements[^g-placement] и правила показа, предоставляет контекст и доступ к inventory, получает сведения о delivery и зарабатывает publisher revenue[^g-publisher-revenue]. Его интерес — продать opportunities достаточно выгодно, сохранив качество продукта и опыт user.

Между бизнес-целью advertiser и технической покупкой часто стоят люди и сервисные организации:

- **agency** — компания-подрядчик, которая планирует или выполняет marketing- и media-работу от имени advertiser. Она может разрабатывать стратегию, готовить creatives, выбирать каналы, запускать campaigns, вести отчётность и иногда управлять платежами;
- **media buyer** — человек, команда или функция, которая выбирает media, platforms и условия покупки, распределяет spend и настраивает campaigns. Media buyer может работать внутри advertiser, внутри agency или другой buying organization.

Agency и media buyer — не синонимы: первая является организацией и contractual role, второй — операционной функцией. Media buyer также не является DSP[^g-dsp]: человек формулирует и настраивает решения, а DSP исполняет часть buying workflow в масштабе.

| Роль | Проблема и beneficiary | Типичный payer | Входные данные | Решение или результат |
|---|---|---|---|---|
| Advertiser | Достичь business outcome; пользу получает сам advertiser | Источник media spend[^g-media-spend] и многих service fees | Бизнес-цель, ограничения, customer data | Цель campaign, бюджет, критерии успеха |
| Publisher | Монетизировать media environment; пользу получает publisher | Обычно не payer в media sale; может платить technology providers | Placements, контекст, inventory rules | Доступные opportunities, delivery rules, publisher revenue |
| Agency | Выполнить работу, для которой advertiser не строит команду или экспертизу | Advertiser; иногда agency выступает плательщиком по downstream invoices | Brief, бюджет, creatives, результаты | План, настройки, execution и отчётность |
| Media buyer | Превратить цель и бюджет в конкретные покупки | Не отдельный payer как функция; оплачивается employer/client | Campaign goals, доступные каналы, reports | Выбор media и platforms, allocation и настройки |

Advertiser может покупать media собственной командой (in-house), полностью передать покупку agency или разделить ответственность. От этого зависит граница контроля: кто имеет доступ к account, raw data и договору, кто отвечает за ошибки настройки и кто может перераспределить spend.

## Кто соединяет demand и supply

Ни advertiser, ни publisher не могут вручную договариваться о каждом короткоживущем показе у тысяч контрагентов. Следующая группа ролей решает проблему масштаба, но делает это с разных сторон:

```text
advertiser ───────────── direct buying ─────────────→ publisher
advertiser ───────────── ad network ────────────────→ publisher
advertiser / buyer → DSP ⇄ exchange / SSP functions → publisher

advertiser ad server и publisher ad server могут поддерживать разные ветви;
ни одна строка не является обязательным универсальным pipeline.
```

**Ad network**[^g-ad-network] агрегирует supply и/или demand и продаёт управляемое media offering. Покупатель обычно выбирает доступное предложение, цель и ограничения, а network берёт на себя заметную часть распределения трафика и отношений с publishers. Ценовая ось принадлежит network: обычно она сама назначает цену покупателю и сама решает, у какого publisher и по какой цене взять показ, поэтому цена закупки для покупателя непрозрачна. Network обычно принимает media money и рассчитывается с supply partners; конкретная коммерческая модель зависит от договора.

**DSP (Demand-Side Platform)** — buying platform, которая помогает media buyer оценивать и покупать opportunities из нескольких supply sources по правилам campaigns. Customer — advertiser, agency или другой buyer. Ключевой признак: решение принимается по каждой поступающей opportunity отдельно и в реальном времени — в programmatic[^g-programmatic] это ставка (bid[^g-bid]) в auction[^g-auction]; глубокое сравнение с network — глава 16, механика аукциона — глава 18.

**SSP (Supply-Side Platform)**[^g-ssp] — sell-side platform для publisher. Она описывает доступные opportunities, предоставляет demand sources доступ к inventory и помогает управлять его продажей. Publisher — основной customer и beneficiary, хотя SSP нередко получает свою оплату в рамках settlement[^g-settlement] media — фактического расчёта деньгами между участниками, в отличие от invoice как выставленного требования.

**Ad exchange**[^g-ad-exchange] — transaction layer или функция, которая соединяет buyers и sellers и выполняет matching либо auction. Exchange не обязательно является отдельной компанией между DSP и SSP: exchange- и SSP-функции часто объединены в одном продукте. Полезное различие такое: SSP представляет sell-side workflow publisher, а exchange выполняет саму функцию автоматизированной сделки между сторонами.

**Ad server**[^g-ad-server] выбирает, доставляет и регистрирует рекламу по заданным campaign- или inventory-правилам. Это не просто CDN с файлами: CDN может отдать bytes creative, а ad server применяет правила и создаёт наблюдаемую точку delivery.

- Advertiser ad server помогает стороне buyer управлять creatives, их доставкой и регистрацией событий независимо от конкретного места покупки.
- Publisher ad server сопоставляет доступные demand sources и управляет delivery на inventory publisher.

Подробные `order`, `line item`, приоритеты и serving mechanics появятся в главе 11.

| Роль | Основной customer | Входные данные | Решение или результат | Денежная связь |
|---|---|---|---|---|
| Ad network | Advertiser/agency; также нужны supply partners | Campaign constraints, creatives, агрегированный supply | Managed distribution и reporting | Обычно principal[^g-principal-agent]: назначает покупателю свою цену, принимает media money и сама рассчитывается с publishers по непрозрачной для покупателя цене |
| DSP | Advertiser, agency, media buyer | Campaign settings, creatives, opportunity signals | Buying decision, доступ к supply, reports | Платит buyer: media cost плюс platform fee, обычно процент от spend |
| SSP | Publisher | Inventory rules, opportunity и context signals | Доступ к demand, sale decision metadata, reports | Платит seller side: обычно удерживает долю (revenue share[^g-revenue-share]) из clearing price (итоговой цены аукциона) до выплаты publisher |
| Ad exchange | Buyers и sellers или их platforms | Описания opportunities и buying responses | Matching/transaction result | Обычно доля из clearing price на sell side; если exchange объединён с SSP, это одно удержание, а не два |
| Ad server | Advertiser или publisher | Campaign/inventory rules, creatives, delivery signals | Выбор, delivery и event registration | Обычно отдельная license или usage fee от своего customer; media money через ad server обычно не проходит |

## Кто измеряет и проверяет

Платформа, продавшая или купившая media, видит только собственные measurement[^g-measurement] points и одновременно заинтересована в результате сделки. Поэтому advertiser и publisher могут подключать поперечные providers. Они не являются обязательным звеном коммерческой цепочки, хотя их код может исполняться внутри доставки creative: integrations получают события и возвращают отдельные выводы.

**Attribution provider**[^g-attribution] сопоставляет доступные рекламные touchpoints — например, impression[^g-impression] или click[^g-click] — с outcomes вроде регистрации или покупки и применяет правила назначения credit. Результат отвечает на вопрос «какому источнику по выбранным правилам приписана эта conversion[^g-conversion]?», а не «была ли реклама истинной причиной действия?» Attribution не доказывает causality.

**MMP (Mobile Measurement Partner)**[^g-mmp] — mobile-specialized категория measurement и attribution providers для app acquisition, installs и in-app outcomes. Основная роль — сопоставлять доступные acquisition signals с событиями приложения и давать advertiser согласованную картину по всем media sources. Мотив понятен: без независимой стороны каждая сеть сама приписывает себе установку по собственным правилам, и сумма self-reported installs как правило превышает реальное число; MMP применяет единые правила ко всем источникам. MMP не является синонимом product analytics: product analytics прежде всего изучает поведение внутри продукта, тогда как MMP связывает acquisition с рекламными источниками. Технические детали SDK, install matching, postbacks и platform privacy restrictions относятся к главам 27–29.

**Verification provider**[^g-verification] создаёт отдельную точку оценки условий и качества доставки рекламы. В зависимости от интеграции он может анализировать доступные delivery, render, placement, context и quality signals и возвращать verification results рекламодателю, publisher или platform. Verification шире одной fraud detection — вопросы могут относиться и к среде показа, — но не абсолютная истина: полнота вывода зависит от среды, доступных signals и методологии.

Для одной рекламы приложения системы могут получить частично пересекающиеся события:

```text
impression / click signals ─┬→ buying и selling platform reports
                            ├→ attribution provider / MMP
delivery / context signals ─┴→ verification provider

install / subscription events → MMP и systems advertiser, если интеграции это позволяют
```

Расхождения между отчётами — не обязательно ошибка. Platform reporting отвечает, что наблюдала сама platform; MMP применяет свои attribution rules к acquisition и app events; verification provider оценивает доступные ему условия delivery. Это разные вопросы и разные границы измерения.

## Кто поставляет, организует и связывает данные

Слово `data` скрывает несколько разных задач. Поставка внешнего набора, управление audience segment[^g-audience-segment], хранение customer record и сопоставление identifiers не являются одной ролью. Отдельная операция — **activation**[^g-activation]: передача данных или сегмента в систему, которая применит их к реальным показам, например в buying platform для targeting[^g-targeting]; до activation сегмент остаётся записью в хранилище.

| Роль | Customer и входные данные | Хранимое состояние | Результат и activation | Чего роль сама по себе не делает |
|---|---|---|---|---|
| **Data provider**[^g-data-provider] | Advertiser, publisher или platform; собственные либо собранные datasets | Dataset, attributes или segments | Данные для разрешённых activation, decisioning или analysis | Не обязана хранить customer record заказчика или принимать media decision |
| **DMP**[^g-dmp] | Advertising/marketing team; audience data и campaign signals | Audience profiles и segments в выбранной модели продукта | Segmentation и activation через рекламные integrations | Не обязана быть system of record для полного customer lifecycle |
| **CDP**[^g-cdp] | Advertiser; first-party events и customer data из product, CRM и других systems | Persistent unified customer record | Доступные downstream systems customer profiles, events и segments | Не обязана покупать media или назначать attribution credit |
| **Identity provider**[^g-identity-provider] | Advertiser, publisher или platform; identifiers из разрешённых источников | Mapping или identity graph в рамках конкретного решения | Связанные или переведённые identifiers для activation и measurement | Не создаёт consent, не регистрирует все events и не доказывает identity реального человека |

**Data provider** продаёт или предоставляет datasets, attributes либо audience segments. Customer платит за дополнительный signal: например, классификацию контекста или audience attribute, который можно законно и технически использовать.

**DMP (Data Management Platform)** — advertising-oriented система для управления, сегментации и activation audience data. **CDP (Customer Data Platform)** отвечает за persistent unified customer record и доступность customer data downstream systems. Историческое правило «DMP — только cookies и anonymous data, CDP — только PII» ненадёжно: современные продукты и deployment models пересекаются. Рабочая граница проходит по главной задаче и record model — рекламная audience activation против устойчивого customer record.

**Identity provider** связывает или переводит identifiers для разрешённых activation, measurement и смежных use cases. Например, одна integration может знать customer ID advertiser, другая — platform-specific ID; identity function помогает установить допустимое соответствие.

Различайте четыре операции:

```text
identity    → связывает пользователей, устройства или их identifiers
tracking    → регистрирует events
attribution → назначает conversion credit по правилам
consent     → выражает разрешение или выбор в отдельном governance/legal context
```

Identity provider не создаёт legal permission самим фактом matching. Конкретные identifiers, алгоритмы resolution и privacy rules будут разобраны в главах 24 и 40–42.

В running example subscription app отправляет first-party события trial и подписки в CDP, чтобы поддерживать customer record. DMP или platform integration может сформировать и активировать допустимый audience segment. Identity provider помогает связать необходимые identifiers между разрешёнными environments, а внешний data provider может обогатить segment дополнительным attribute.

## Одна campaign: отдельно данные и деньги

Соберём роли на одном сценарии. Subscription app рекламируется внутри mobile game. Advertiser нанял agency; media buyer в agency запускает acquisition через DSP. Publisher игры предоставляет opportunity через SSP, в продукте которой также есть exchange function (в mobile in-app эту sell-side роль часто исполняет mediation platform или SDK network — глава 12). MMP измеряет mobile acquisition, verification provider опционально оценивает delivery, а data/identity functions подключаются только там, где они нужны и допустимы.

Это один возможный состав, а не обязательная цепочка: advertiser мог купить media напрямую или через ad network, а несколько ролей могли принадлежать одной компании либо отсутствовать.

### Поток данных

```text
advertiser / media buyer
  ── campaign goal, settings, creative metadata ──→ buying и serving systems

publisher app
  ── opportunity, placement, format, разрешённый context ──→ sell-side и decision systems

decision systems
  ── выбранная реклама + delivery metadata ──→ publisher app

publisher app и participating systems
  ── impression / click / delivery events ──→ reporting, MMP, verification

subscription app / advertiser backend
  ── install, trial, subscription events ──→ MMP, CDP и advertiser reporting
```

Не каждый участник получает каждое событие: набор зависит от integrations, среды, договора и privacy/platform restrictions. Event flow часто двунаправлен и asynchronous; он не обязан повторять ни путь creative, ни финансовые отношения.

### Поток денег

Направление то же, что на карте главы 1: media spend advertiser идёт через канал покупки к продавцам media и образует publisher revenue, а technology providers получают отдельные fees. Новое здесь — кто именно и кому платит в типичном programmatic-составе:

| Кто платит | Кому | За что | Тип денег |
|---|---|---|---|
| Advertiser | Agency | Планирование и ведение campaigns | Обычно fee или процент от spend; иногда внутри media invoice |
| Advertiser или agency | DSP | Купленные media и использование платформы | Media cost плюс platform fee, обычно процент от spend |
| DSP | Exchange / SSP | Выигранные opportunities по clearing price | Media money |
| Exchange / SSP | Publisher | Проданные opportunities | Publisher payout[^g-publisher-payout]: clearing price минус sell-side revenue share |
| Advertiser | MMP | Attribution и измерение acquisition | SaaS[^g-saas-pricing] или usage fee |
| Advertiser | Verification provider | Оценка условий доставки | Usage fee, обычно по объёму измеренных impressions |
| Publisher или advertiser | Свой ad server | Выбор, доставка и регистрация рекламы | Usage или SaaS fee |
| Advertiser или agency | Data provider | Audience segments или attributes | Часто data CPM[^g-cpm] — надбавка к media cost, начисляемая через DSP |

Advertiser — экономический источник media spend, но contractual payer по invoice DSP нередко agency: advertiser видит один consolidated invoice, а деньги далее расходятся по нескольким договорам. Invoice и settlement тоже различаются: первый — выставленное требование, второй — фактический расчёт, и суммы могут не совпасть из-за adjustments. Удержания intermediaries[^g-intermediary] на каждом шаге и путь условных `$100` — тема главы 4.

Наконец, **invoice path**, реальный **settlement path**, путь доставки creative и HTTP/event path могут иметь разные endpoints: creative может прийти с ad server или CDN, а conversion event асинхронно уйти в MMP и не вернуться через SSP.

## Почему одна компания занимает несколько мест на карте

Компании совмещают роли из-за acquisitions, общей инфраструктуры и data, желания предложить managed service, единый workflow, reporting и contract. Когда одна компания контролирует несколько последовательных уровней value chain, это называют **vertical integration**[^g-vertical-integration] (вертикальная интеграция); в курсе мы также говорим о совмещении ролей.

Для customer совмещение ролей означает меньше integrations, ниже operational overhead, быстрее обмен данными и один UI для настройки и отчётов. Но те же свойства создают риски:

- конфликт incentives, если одна сторона одновременно представляет buyer и seller;
- непрозрачность границ fees и внутренних money transfers;
- преимущество собственного supply или demand в decisioning;
- self-measurement, когда исполнитель сделки сам оценивает её качество;
- сложность выгрузки data и сравнения внешних alternatives.

Представим условную Platform X: она продаёт упакованный media package, даёт media buyer настройки в духе DSP, доставляет creatives и показывает attribution report в одном UI. Называть её только «DSP» недостаточно. Разложим suite на функции:

| Функция Platform X | Отдельная карточка роли |
|---|---|
| Упаковывает и продаёт доступ к media | Ad network-like managed offering |
| Выбирает opportunities по campaign rules | DSP-like buying/decisioning |
| Доставляет creative и регистрирует delivery | Ad serving |
| Связывает touchpoints с outcomes | Attribution/measurement |

Общий login и общий invoice не делают эти функции одной ролью. Это и есть способ анализировать незнакомую AdTech-компанию: сначала перечислить выполняемые роли, затем заполнить для каждой `problem → customer → payer → data in/out → decision → money` и спросить, где возникает fee и с чьими интересами она может конфликтовать. Только после этого имеет смысл сравнивать vendors по labels.

## С чем это часто путают

- **«Brand advertiser и performance advertiser — разные виды компаний».** Нет: это ориентации activity. Одна компания может вести обе.
- **«Ad network — старое название DSP».** Network продаёт управляемую агрегацию media по своей цене; DSP оставляет решение по каждой opportunity правилам buyer. Реальные suites могут совмещать обе функции.
- **«SSP и exchange обязаны быть разными компаниями» или «это полные синонимы».** Обе крайности неверны: sell-side workflow и transaction function различимы, но часто объединены в одном продукте.
- **«MMP знает истинную причину установки, а verification provider видит абсолютную истину показа».** Оба работают с доступными measurement points и методологиями. Attribution credit не равен causality, verification result ограничен интеграцией.
- **«Data provider, DMP, CDP и identity provider — четыре названия базы пользователей».** Они соответственно поставляют data, организуют audience activation, поддерживают customer record и связывают identifiers.

## Что важно запомнить

1. Карта AdTech описывает логические роли, а не обязательный список компаний.
2. Advertiser финансирует рекламу ради outcome; publisher создаёт media environment и opportunities.
3. Brand и performance — ориентации целей и измерения, которые один advertiser может сочетать.
4. Ad network продаёт media по своей цене; DSP решает по каждой opportunity ставкой по правилам buyer и берёт с buyer platform fee; SSP обслуживает sell-side workflow и обычно удерживает долю из clearing price; exchange выполняет transaction function.
5. Advertiser-side и publisher-side ad servers применяют разные наборы правил, хотя обе роли выбирают, доставляют и регистрируют рекламу.
6. MMP/attribution, verification, data и identity — поперечные функции, а не обязательные звенья коммерческой цепочки; они обычно получают fee за функцию, а не долю media money.
7. Data flow, delivery path, invoice path и settlement path не обязаны совпадать.
8. Одна company может выполнять несколько roles; vertical integration снижает integration friction, но создаёт вопросы о incentives, fees, границах данных и независимости measurement.

## Проверьте себя

1. Почему subscription app может одновременно быть brand- и performance-advertiser?
2. Чем media buyer отличается от agency и DSP?
3. Для чего publisher может использовать SSP и publisher ad server в одном flow, не считая их одной ролью?
4. Вымышленный suite предлагает publishers SSP, publisher ad server и verification в одном UI по одному invoice. Какие отдельные role cards нужно заполнить и где у такого сочетания возникает конфликт интересов?

## Источники и дополнительное чтение

1. [IAB Tech Lab — Programmatic Auction Definitions](https://iabtechlab.com/programmatic-auction-definitions/)
2. [UK Government — Online Advertising Programme consultation](https://www.gov.uk/government/consultations/online-advertising-programme-consultation/online-advertising-programme-consultation)
3. [Competition and Markets Authority — Intermediation in open display advertising](https://www.gov.uk/find-digital-market-research/online-platforms-and-digital-advertising-market-study-appendix-m-intermediation-in-open-display-advertising-2020-cma)
4. [Adjust — What is a Mobile Measurement Partner](https://www.adjust.com/glossary/mobile-measurement-partner-mmp/)
5. [IAB Tech Lab — Open Measurement SDK](https://iabtechlab.com/standards/open-measurement-sdk/)
6. [IAB Tech Lab — Identity Solutions Guidance and Recommended Practices](https://iabtechlab.com/wp-content/uploads/2024/05/Identity-Solutions-Guidance-FINAL.pdf)
7. [CDP Institute — What is a CDP?](https://www.cdpinstitute.org/what-is-a-cdp/)
8. [Oracle Marketing Cloud — CDP vs CRM vs DMP](https://blogs.oracle.com/marketingcloud/cdp-vs-crm-vs-dmp)
