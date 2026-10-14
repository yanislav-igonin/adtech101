---
id: glossary
type: glossary
chapter: 99
slug: glossary
title: "Глоссарий"
language: ru
---

# Глоссарий

Определения ключевых терминов курса. В главах такие термины помечены сноской; здесь — полное описание с примером.

### RTB (real-time bidding) {#g-rtb}

**RTB (real-time bidding)** — механизм programmatic-покупки, при котором отдельная рекламная возможность (`opportunity`) выставляется на автоматический аукцион и продаётся за доли секунды — пока страница или приложение ещё не показали рекламу. Покупатели отправляют ставки, как правило, через DSP; торги идут на ad exchange или внутри SSP с auction-функцией. RTB — не синоним programmatic и тем более AdTech: это один из механизмов автоматизированной покупки внутри более широкого стека.

**Пример:** user открывает новостное приложение. Publisher через SSP выставляет показ на аукцион; несколько DSP, играя за разных advertisers, за ~100 мс возвращают ставки; победившая реклама доставляется в приложение до того, как user увидит контент.

### Bid {#g-bid}

**Bid (ставка)** — предложение buyer заплатить определённую цену за конкретную ad opportunity, обычно выраженное как CPM. Bid — это решение до события: он не равен итоговой цене (clearing price) и не равен billable amount; в programmatic bid формируется DSP на каждый bid request отдельно.

**Пример:** DSP оценивает запрос из игрового приложения и отвечает bid `$12 CPM`; аукцион может закрыться по `$10`, а advertiser по договору заплатит за qualifying impressions.

### Auction {#g-auction}

**Auction (аукцион)** — механизм выбора победителя среди нескольких bids на одну ad opportunity и определения цены (clearing price) по правилам аукциона — first-price, second-price и их варианты. Auction win — событие выбора победителя; оно не равно показу и не делает impression billable само по себе.

**Пример:** на один показ пришли bids `$12`, `$10` и `$7`; при first-price победитель платит `$12`, при second-price — цену второго bid (или floor), и только после доставки creative событие может стать billable.

### Agency {#g-agency}

**Agency** — компания-подрядчик, которая планирует и выполняет marketing- и media-работу от имени advertiser: разрабатывает стратегию, готовит `creative`, выбирает каналы, запускает `campaign` и ведёт отчётность. Advertiser может держать покупку media in-house, отдать её agency целиком или разделить ответственность. Agency — организация и договорная роль, в отличие от media buyer — операционной функции, которая может работать и внутри advertiser.

**Пример:** производитель кроссовок выходит на рынок Германии. Agency получает brief и бюджет, планирует каналы, настраивает `campaign` в DSP и отчитывается по результатам. Advertiser видит один consolidated invoice от agency, хотя внутри деньги распределяются по нескольким договорам — media, платформы, fees.

### Ad network {#g-ad-network}

**Ad network (рекламная сеть)** — посредник, который агрегирует рекламные возможности (`inventory`) от многих publisher и продаёт их advertiser как единый упакованный продукт: сеть берёт на себя подбор supply, ценообразование и показ, а покупатель получает одно управляемое предложение вместо десятка отдельных договоров. Цены внутри сети обычно непрозрачны для покупателя. Исторически многие ad network добавили аукционные механики и перестроились в ad exchange, поэтому под одним брендом часто совмещаются обе функции.

**Пример:** небольшому advertiser проще купить «100 000 показов в игровых приложениях за CPM $X» у одной сети, чем договорываться с каждым publisher отдельно. Сеть сама решает, из чьих приложений взять показы и по какой цене она купила их у publisher.

### Ad exchange {#g-ad-exchange}

**Ad exchange (рекламная биржа)** — transaction-слой, который соединяет покупателей и продавцов в автоматизированной сделке, обычно через аукцион в реальном времени (RTB). Отличие от ad network в прозрачности: покупатель видит описание отдельной `opportunity` и сам решает, сколько за неё платить, а цену определяет аукцион, а не прайс-лист сети. Exchange не обязательно отдельная компания между DSP и SSP: exchange- и SSP-функции часто объединены в одном продукте.

**Пример:** DSP за advertiser видит от exchange описание показа: приложение, формат, примерный контекст — и за миллисекунды решает, делать ли ставку и сколько платить. Проигравший платит ничего; победитель получает показ по цене аукциона.

### AdTech {#g-adtech}

**AdTech (advertising technology)** — совокупность технологий, которые координируют покупку, продажу, выбор, доставку, измерение и расчёты за рекламу между advertiser, publisher и посредниками: от ad server и DSP/SSP до measurement- и verification-систем. Programmatic — лишь часть AdTech: direct deals, reserved buying и закрытые платформы тоже работают на AdTech. С MarTech граница проводится по основной задаче: AdTech координирует paid media, MarTech — customer lifecycle.

**Пример:** приложение с подпиской покупает установки через DSP, publisher продаёт показы через SSP, сделка проходит через exchange, ad server доставляет creative, а MMP измеряет установки — все пять систем относятся к AdTech.

### Digital advertising {#g-digital-advertising}

**Digital advertising** — оплачиваемая коммуникация, с помощью которой advertiser пытается повлиять на знание, отношение или действие аудитории в цифровой среде. Это рынок координации между advertiser (demand), publisher (supply) и user, а не просто доставка баннера: ценности и цели сторон конфликтуют, и значительная часть AdTech существует для управления этими конфликтами.

**Пример:** контентное приложение показывает рекламу между статьями; подписочный сервис платит за возможность обратиться к его аудитории, а user получает контент «в обмен» на внимание к рекламе.

### Advertiser {#g-advertiser}

**Advertiser (рекламодатель)** — участник рынка, который финансирует рекламу ради бизнес-результата: установок, покупок подписки, роста узнаваемости. Он покупает не человека, а возможность обратиться к аудитории в определённом контексте; создаёт demand и задаёт цели, бюджет и creative.

**Пример:** стриминговый сервис выделяет бюджет на привлечение подписчиков: его DSP ищет показы в приложениях целевой аудитории и платит за каждую возможность показать рекламу.

### Publisher {#g-publisher}

**Publisher (издатель)** — владелец или управляющий media-средой, где возникают рекламные возможности: сайт, мобильное приложение, видеосервис, игра. Монетизирует среду рекламой, создаёт supply и решает, какие placement, форматы и покупателей допускать, балансируя revenue с пользовательским опытом.

**Пример:** новостное приложение выделяет баннер и полноэкранный блок после статьи и через SSP открывает их programmatic-покупателям, сохраняя лимит на частоту показов.

### Demand {#g-demand}

**Demand (спрос)** — бюджеты и намерение advertiser купить подходящие рекламные возможности; сторона рынка, вокруг которой группируются `buy side` / `demand side` — люди и системы, помогающие планировать и покупать media (agency, DSP). Demand — это сторона рынка, а не конкретная технология: платформы нельзя путать со сторонами.

**Пример:** advertiser закладывает $500 000 на привлечение пользователей в трёх странах — это demand; DSP, через которую он покупает media, относится к demand side.

### Supply {#g-supply}

**Supply (предложение)** — доступные рекламные возможности publisher; сторона рынка, вокруг которой группируются `sell side` / `supply side` — люди и системы, помогающие описывать, продавать и доставлять рекламу (SSP, publisher ad server). Supply — это совокупность inventory на продажу, а не название платформы. Ad network агрегирует и supply, и demand, поэтому стоит между сторонами, а не внутри одной из них.

**Пример:** игровое приложение с двадцатью рекламными местами и правилами их показа — supply; SSP, через которую оно открывает доступ покупателям, — supply side.

### Advertising inventory {#g-inventory}

**Advertising inventory (рекламный инвентарь)** — множество доступных или прогнозируемых возможностей показать рекламу, ограниченное средой, местом, форматом, временем, правилами publisher и допустимым контекстом аудитории. Inventory — не список пользователей и не склад заранее произведённых показов: opportunity возникает и исчезает в момент использования продукта.

**Пример:** игра прогнозирует 10 млн полноэкранных показов на следующий месяц — это inventory; конкретная возможность возникает только когда игрок завершает уровень.

### Placement {#g-placement}

**Placement (рекламное место или selectable media scope)** — overloaded product term. На publisher side это заранее заданный ad slot или правило появления рекламы, которое порождает ad opportunities по мере использования продукта. На buy side placement может означать явно выбранную среду показа — site, app, channel, video, section или отдельный slot. Уровень сущности нужно уточнять из product contract.

**Пример:** «полноэкранный блок после уровня» — publisher-side placement; настройка campaign «показывать только в outdoor-news app» — buy-side selectable placement.

### Ad opportunity {#g-ad-opportunity}

**Ad opportunity (рекламная возможность)** — конкретная возможность выбрать и показать рекламу, возникшая, когда user дошёл до placement. Короткоживущее событие: в цифровой среде оно может исчезнуть быстрее, чем человек успеет принять решение, поэтому обрабатывается системами за миллисекунды, а в programmatic выставляется на торги как отдельная единица.

**Пример:** игрок завершил уровень — приложение отправляет запрос с описанием контекста, и до отрисовки экрана системы успевают выбрать и вернуть рекламу.

### Impression {#g-impression}

**Impression (показ)** — событие доставки или показа выбранной рекламы, зарегистрированное системой по определённому правилу; единица подсчёта, а не факт восприятия человеком. `Served`, `rendered` и `viewable` — разные состояния доставки, поэтому счётчики разных участников одной сделки могут не совпадать.

**Пример:** ad server засчитал 100 000 impressions по правилу «баннер загружен», а measurement-провайдер — 82 000 по правилу «видимая площадь не менее секунды»; оба правы по своим правилам.

### DSP (Demand-Side Platform) {#g-dsp}

**DSP (Demand-Side Platform, платформа стороны спроса)** — платформа, которая автоматизирует покупку рекламных возможностей для advertiser: агрегирует доступ к нескольким supply-источникам, оценивает каждую opportunity и решает, делать ли ставку и сколько платить. Относится к demand side не потому, что «создаёт demand», а потому, что действует в интересах покупателя.

**Пример:** advertiser загружает в DSP бюджет, цель и аудитории; DSP участвует в аукционах на десятках exchange и SSP и покупает показы, укладываясь в целевую стоимость установки.

### SSP (Supply-Side Platform) {#g-ssp}

**SSP (Supply-Side Platform, платформа стороны предложения)** — платформа, которая помогает publisher управлять продажей inventory: задаёт правила доступа покупателей, подключает programmatic demand (DSP, exchange), проводит или передаёт аукцион. SSP- и exchange-функции часто объединены в одном продукте.

**Пример:** новостной сайт задаёт в SSP минимальные цены и запрет на отдельные категории рекламы; SSP открывает показы сотням DSP и выбирает лучшее предложение.

### Ad server {#g-ad-server}

**Ad server (рекламный сервер)** — система, которая выбирает, доставляет и регистрирует рекламу по заданным правилам. Бывает publisher-стороны (сопоставляет прямые кампании, сети и programmatic-спрос, управляет delivery) и advertiser-стороны (хранит creative, считает показы и клики); термин обозначает функцию, а не сторону рынка.

**Пример:** publisher ad server получает решение от SSP, прямую кампанию и резерв сети — и решает, чью рекламу вернуть в этом запросе; advertiser ad server тем временем отдаёт creative и логирует показ.

### Programmatic {#g-programmatic}

**Programmatic (программатик)** — автоматизированная покупка и продажа рекламы: решение по каждой opportunity принимают системы, а не люди. RTB — лишь один из его механизмов; programmatic также включает автоматизированные reserved- и direct-механики без аукциона. Programmatic — часть AdTech, но не весь AdTech.

**Пример:** гарантированная сделка «показы из спортивного раздела по фиксированной цене через автоматизированный договор» — programmatic без аукциона в реальном времени.

### Creative {#g-creative}

**Creative (креатив)** — рекламный материал, который доставляется и показывается user: баннер, видео, нативный формат, playable. Наряду с правилами targeting является объектом доставки и должен соответствовать формату и правилам среды publisher; в кампании обычно готовят несколько creatives.

**Пример:** для кампании готовят вертикальное видео на 15 секунд и playable-версию и загружают их в DSP с metadata о формате и размере.

### Campaign {#g-campaign}

**Campaign (рекламная кампания)** — организованный набор рекламной активности advertiser с целью, бюджетом, правилами доставки и creatives. До показа её условия сообщаются системам покупки; объекты и события связываются identifiers вроде `campaign_id`.

**Пример:** осенняя кампания подписочного сервиса: цель — установки, бюджет $200 000, три creatives, ограничение частоты — всё настраивается в DSP до первого показа.

### Measurement {#g-measurement}

**Measurement (измерение)** — функция регистрации и агрегации рекламных событий (impressions, clicks, outcomes) для отчётности и оптимизации. Measurement-провайдеры дают независимую точку наблюдения; у разных участников разные timestamps и правила подсчёта, поэтому отчёты не обязаны совпадать идеально. В mobile выделенная категория — MMP.

**Пример:** advertiser сверяет показы у себя, у ad server и у measurement-провайдера — счётчики расходятся из-за разных точек наблюдения и правил.

### MMP (Mobile Measurement Partner) {#g-mmp}

**MMP (Mobile Measurement Partner, мобильный измерительный партнёр)** — специализированная категория measurement-провайдеров для mobile: измеряет установки и in-app события, проводит attribution и предоставляет независимые данные сторонам сделки. Не синоним любой системы measurement.

**Пример:** приложение подключает MMP, чтобы связать клик из рекламы с установкой из app store и последующей покупкой подписки.

### Verification {#g-verification}

**Verification (верификация)** — независимая оценка качества и условий показа: видимость, окружение, fraud, соответствие правилам. Verification-провайдеры подключаются поперёк цепочки и не участвуют в принятии коммерческого решения о сделке.

**Пример:** verification-провайдер помечает 4% показов как невидимые и 1% как fraud — advertiser вычитает их из оплаты.

### Intermediary {#g-intermediary}

**Intermediary (посредник)** — участник, который соединяет стороны рынка или выполняет специализированную функцию: agency, DSP, ad network, exchange, SSP, ad server, measurement-, verification- и data-провайдеры. Оправдан, когда ценность его функции (reach, aggregation, interoperability, скорость, measurement, контроль риска) выше стоимости и сложности; не обязан присутствовать в каждой сделке и не обязательно удерживает долю media money — часть посредников получает отдельный service или SaaS fee.

**Пример:** небольшой advertiser покупает показы у ad network, потому что не готов вести десятки интеграций с publisher напрямую, — функция агрегации оправдывает fee.

### Media spend {#g-media-spend}

**Media spend (рекламные расходы)** — деньги, которые advertiser выделяет и тратит на покупку рекламы. Проходят через продавцов media и в итоге образуют publisher revenue, уменьшаясь по пути на fees; не синоним publisher revenue и не синоним intermediary fee — это разные суммы одной цепочки.

**Пример:** из $100 media spend network удерживает $20, SSP — $12, publisher получает $68; MMP и ad server получают отдельные SaaS fee вне media money.

### Publisher revenue {#g-publisher-revenue}

**Publisher revenue (выручка publisher)** — сумма, которую publisher признаёт выручкой по своим правилам учёта из медиаплатежей за своё inventory; в простом случае равна publisher payout, но признание (accrued / billed / settled) следует policy publisher, а не моменту платежа. Отличается от advertiser spend на сумму всех fees в цепочке; service- и SaaS-fee участников вне media money к ней не относятся.

**Пример:** advertiser потратил $100; network удержала $20, SSP — $12; publisher получил payout $68 и признал их своей revenue за period, в котором состоялись показы.

### Settlement (accrued / billed / settled) {#g-settlement}

**Settlement (расчёт)** — фактическое движение денег между участниками по итогам периода, в отличие от invoice (выставленного требования) и от начисления. Одна сумма проходит три состояния: `accrued` — начислена по событиям, `billed` — выставлена в invoice или statement, `settled` — оплачена; на каждом шаге сумма может измениться из-за adjustments, fraud filtering, credits и FX. Для одной стороны это receivable (ожидаемое поступление), для другой — payable.

**Пример:** publisher видит в dashboard accrued `$68` за сентябрь; statement от SSP приходит в октябре на `$66` после вычета invalid traffic; оплата (settlement) поступает через 60 дней.

### Publisher payout {#g-publisher-payout}

**Publisher payout (выплата publisher)** — сумма, которую по договору продавца должны перечислить publisher после revenue share, fees и adjustments; для SSP или network это payable, для publisher — receivable. Payout — договорная и платёжная величина; какую часть и в каком периоде publisher признаёт выручкой, определяет его accounting policy (см. publisher revenue).

**Пример:** из $80, полученных SSP от network, после удержания 15% publisher причитается payout $68.

### MarTech {#g-martech}

**MarTech (marketing technology)** — технологии для более широкого управления marketing и customer lifecycle: customer data, коммуникациями и собственными каналами advertiser (CRM, marketing automation, CDP, email/push-платформы). Пересекается с AdTech в measurement, attribution, identity и activation, поэтому границу проводят по основной задаче системы, а не по ярлыку vendor.

**Пример:** покупка подписки — outcome signal для AdTech measurement и одновременно триггер email-цепочки удержания в MarTech.

### Data provider {#g-data-provider}

**Data provider (поставщик данных)** — провайдер, который продаёт или предоставляет datasets, attributes или готовые audience segments для targeting, measurement и enrichment. Работает параллельно цепочке покупки, а не «между» двумя обязательными соседями; за third-party segments обычно платит buyer — часто как data CPM, начисляемый через buying platform поверх media cost. Не путать с identity provider: тот не поставляет данные, а устанавливает соответствие identifiers.

**Пример:** DSP подключает сегмент «интерес к фитнесу» от внешнего data provider; за каждую тысячу показов по этому сегменту к media CPM добавляется data fee провайдера.

### Media buyer {#g-media-buyer}

**Media buyer** — человек, команда или функция, которая выбирает media, platforms и условия покупки, распределяет spend и настраивает campaigns. Это операционная роль, а не организация: media buyer может работать внутри advertiser, внутри agency или другой buying organization. Не синоним agency (организация-подрядчик) и не синоним DSP: человек формулирует и настраивает решения, платформа исполняет часть buying workflow в масштабе.

**Пример:** media buyer в agency получает план каналов и бюджет, заводит campaign в DSP, задаёт аудитории и ставки, а по ходу месяца перераспределяет spend между platforms по результатам отчётов.

### Vertical integration {#g-vertical-integration}

**Vertical integration (вертикальная интеграция)** — ситуация, когда одна компания занимает несколько ролей цепочки (например, DSP, exchange и SSP, или ad network и MMP) и совмещает их в одном продукте или бренде. Даёт customer удобство и единый invoice, но создаёт конфликты интересов: компания одновременно представляет buyer и seller, сама себя измеряет или управляет аукционом, в котором участвует. Отраслевой термин для того, что в курсе также называется совмещением ролей.

**Пример:** платформа продаёт advertiser managed media, при этом владеет exchange, через который продаёт собственный inventory, и отчитывается о результатах собственным measurement — три роли на одной карте экосистемы.

### Brand advertising {#g-brand-advertising}

**Brand advertising (brand-реклама)** — ориентация рекламы, которая в первую очередь меняет awareness, consideration или perception аудитории: знание, рассмотрение и отношение к продукту. Оценивается по отложенным показателям, а не по немедленному действию. Это ориентация, а не вид компании: один advertiser может сочетать brand- и performance-активность.

**Пример:** стриминговый сервис показывает video campaign для знакомства с брендом и оценивает её по подъёму awareness и intention, а не по установкам за неделю.

### Performance advertising {#g-performance-advertising}

**Performance advertising (performance-реклама)** — ориентация рекламы, управляемая вокруг измеримого действия и стоимости его получения: регистрации, trial, установки, покупки. Оценивается через attribution и стоимость результата. Это ориентация, а не вид компании и не синоним «измеримой рекламы»: цель, горизонт оценки и ожидаемые доказательства результата отличаются от brand advertising.

**Пример:** acquisition campaign приложения оптимизирована в DSP на стоимость установки: ставка корректируется по каждому источнику, чтобы укладываться в целевой CPI.

### Attribution {#g-attribution}

**Attribution (атрибуция)** — правила, по которым доступные рекламные touchpoints (impression, click) сопоставляются с outcomes (установка, регистрация, покупка) и получают credit за конверсию. Attribution отвечает на вопрос «какому источнику по выбранным правилам приписано действие», а не «была ли реклама истинной причиной»: credit не доказывает causality. Провайдеры attribution — отдельная поперечная категория; в mobile — MMP.

**Пример:** user увидел видео в игре, на следующий день кликнул по баннеру и подписался; MMP по правилу «последний клик» назначает credit баннеру, и остальные источники остаются без credit, даже если участвовали.

### DMP (Data Management Platform) {#g-dmp}

**DMP (Data Management Platform)** — advertising-oriented система для управления, сегментации и activation audience data: собирает campaign signals и внешние datasets, строит audience profiles и segments и активирует их через рекламные интеграции. Не обязана быть system of record для полного customer lifecycle. Историческое правило «DMP — только cookies и anonymous data» ненадёжно; рабочая граница с CDP проходит по главной задаче — рекламная audience activation против устойчивого customer record.

**Пример:** media team собирает в DMP сегмент «играли в казуальные игры, видели рекламу, но не устанавливали приложение» и активирует его в DSP для acquisition campaign.

### CDP (Customer Data Platform) {#g-cdp}

**CDP (Customer Data Platform)** — система, которая собирает first-party события и customer data из product, CRM и других систем в persistent unified customer record и делает profiles, events и segments доступными downstream-системам. Не покупает media и не назначает attribution credit; относится к управлению customer lifecycle, что делает её частью MarTech.

**Пример:** subscription app отправляет в CDP события trial и подписки; CDP собирает единый профиль и отдаёт сегмент «прошёл trial, не оплатил» в рекламные и email-системы.

### Identity provider {#g-identity-provider}

**Identity provider** — провайдер, который связывает или переводит identifiers из разрешённых источников для activation, measurement и смежных use cases: например, сопоставляет customer ID advertiser с platform-specific ID. Не создаёт consent и не доказывает identity реального человека: matching в рамках одного решения не равен legal permission. Отличается от data provider задачей — не поставляет datasets, а устанавливает соответствие identifiers.

**Пример:** advertiser и publisher используют разные идентификаторы одного пользователя; identity-провайдер переводит их в общий identifier, чтобы частота показов считалась по человеку, а не дважды.

### Activation {#g-activation}

**Activation (активация)** — передача данных или audience segment в систему, которая может их использовать для targeting, suppression, personalization или measurement: из CDP/DMP в DSP, из CRM advertiser в walled garden, из identity graph в SSP. До activation данные — запись в хранилище; после — правило, влияющее на реальные показы. Activation требует match identifiers между источником и принимающей платформой и разрешённого правового основания.

**Пример:** список trial-пользователей без оплаты загружен в buying platform и после matching стал retargeting-аудиторией — это activation сегмента.

### Metric contract {#g-metric-contract}

**Metric contract (контракт метрики)** — полное определение метрики, по которому её число можно воспроизвести и интерпретировать: event definition, measurement point, filters и deduplication, numerator/denominator, dimensions, period и окна, currency, perspective и ledger boundary. Название метрики без контракта не задаёт смысла: одна и та же формула на разных contracts отвечает на разные вопросы.

**Пример:** `CTR = 2%` от ad server по rendered impressions и filtered clicks — не то же число, что `CTR = 2%` от платформы по served impressions и всем clicks: названия совпадают, contracts различаются.

### Click {#g-click}

**Click (клик)** — qualifying user-initiated interaction с рекламой, зарегистрированная по правилу конкретной системы. Даже одно действие имеет несколько measurement points: initiated, measured (click tracker), received (destination) и resolved (landing page) clicks не обязаны совпадать из-за обрывов соединения, redirect-цепочек и filters.

**Пример:** user кликнул по баннеру, но соединение оборвалось на redirect: click tracker засчитал measured click, а destination не получил request — счётчики расходятся, и оба честны по своим правилам.

### Conversion {#g-conversion}

**Conversion (конверсия)** — valuable action или outcome, который advertiser определил как значимый (install, trial, первая оплата, renewal, purchase) и который система засчитала по measurement и attribution rules. Conversions нельзя складывать без явного counting rule: один click может привести к нескольким conversions. Observed conversion — зарегистрированное событие; attributed conversion — событие, которому attribution rule назначил credit; ни то ни другое не доказывает causality.

**Пример:** click привёл к install, затем к trial и оплате подписки — по правилам отчёта это три conversions одного interaction, и итоговая сумма зависит от режима подсчёта (одна или каждая conversion на interaction).

### Served impression {#g-served-impression}

**Served impression (отданный показ)** — impression, засчитанный по факту того, что ad server или selling platform отдала creative (или ссылку на него) в ответ на запрос; доказывает отправку, но не загрузку, не отрисовку и не видимость. Самое раннее и самое крупное число в лестнице `served → rendered → viewable`.

**Пример:** ad server вернул 100,000 ответов с creative — 100,000 served impressions, хотя часть пользователей закрыла экран до загрузки баннера.

### Rendered impression {#g-rendered-impression}

**Rendered impression (отрисованный показ)** — impression, засчитанный после того, как creative загрузился и был отрисован на устройстве пользователя (обычно по сигналу от клиентского кода: pixel или SDK-событие после render). Доказывает отрисовку, но не то, что creative попал в видимую область экрана или был замечен; MRC-стандарт для display считает impression именно по факту загрузки/render на стороне клиента.

**Пример:** из 100,000 served impressions 92,000 отправили render pixel — 92,000 rendered impressions; сколько из них оказались viewable, покажет отдельное измерение.

### Viewable impression {#g-viewable-impression}

**Viewable impression (видимый показ)** — impression, выполнивший применимые geometry/time criteria viewability (классический MRC benchmark: не менее 50% пикселей creative на экране одну continuous second для display и две для video). Viewable означает standardized opportunity to see, а не внимание человека; non-viewable (measurement состоялся, criteria не выполнены) не равно non-measurable (статус определить не удалось).

**Пример:** баннер загрузился и отрисовался, но половина area осталась вне вьюпорта дольше порога — measurement помечает его non-viewable, хотя rendered impression состоялся.

### Reach {#g-reach}

**Reach (охват)** — de-duplicated число unique entities (person, device, household, account или modeled audience), получивших хотя бы одну qualifying exposure за период, либо доля таких entities в явно заданной population: `reach rate = reached unique entities / declared universe × 100%`. Сравним только при одинаковых entity definition, exposure rule, population, de-dup scope и period.

**Пример:** кампания достигла 20,000 de-duplicated persons из universe 200,000 — reach count 20,000 и reach rate 10%; те же показы, посчитанные по device IDs, дали бы другие числа.

### Frequency {#g-frequency}

**Frequency (частота)** — среднее число qualifying exposures на reached unique entity за тот же период: `frequency = qualifying impressions / reached unique entities`. Это среднее, а не распределение: оно не означает, что каждый человек видел рекламу одинаковое число раз.

**Пример:** 60,000 qualifying viewable impressions на 20,000 de-duplicated persons — average frequency 3, хотя у части пользователей один показ, а у других — пятнадцать.

### CTR (Click-Through Rate) {#g-ctr}

**CTR (Click-Through Rate)** — доля выбранных impressions, после которых зарегистрированы выбранные clicks: `CTR = qualifying clicks / counted impressions × 100%`. Число зависит от click/impression basis (served или rendered, filtered или все) и population; высокий CTR сам по себе не означает качественный traffic, conversions или causal lift.

**Пример:** 160 clicks на 8,000 counted impressions — CTR 2%; замена served impressions на rendered изменит знаменатель и результат.

### CVR (Conversion Rate) {#g-cvr}

**CVR (Conversion Rate)** — доля qualifying conversions в declared eligible precursor events: `CVR = qualifying conversions / declared eligible precursor events × 100%`. Голый CVR скрывает переход: сравнимы только названные переходы вроде click-to-install или install-to-trial; значение выше 100% возможно при нескольких conversion actions на один interaction.

**Пример:** 24 attributed subscriptions на 160 eligible clicks — click-to-subscription CVR 15%; тот же campaign имеет другой click-to-install CVR, и сравнивать их напрямую нельзя.

### CPM (Cost per Mille) {#g-cpm}

**CPM (Cost per Mille)** — стоимость тысячи counted impressions для buyer: `CPM = advertiser cost or spend / counted impressions × 1,000`. Термин неоднозначен без контракта: может означать pricing basis, rate, bid или observed average CPM post-fact; observed CPM отвечает на вопрос «сколько buyer потратил на тысячу counted impressions».

**Пример:** $96 spend на 8,000 counted impressions — observed CPM $12, даже если ставки в аукционе были другими.

### eCPM (effective CPM) {#g-ecpm}

**eCPM (effective CPM)** — признанный revenue seller на тысячу counted impressions: `eCPM = recognized revenue / counted impressions × 1,000`. Обычно publisher-перспектива; позволяет сравнивать demand, оплачиваемый по CPM, CPC или CPA, на общей realised-revenue basis. Не синоним CPM: numerators принадлежат разным ledger boundaries.

**Пример:** seller получил $800 recognized revenue за 80,000 counted impressions — eCPM $10, хотя покупатели платили по разным моделям: один по CPM, другой по CPC, третий по CPA.

### CPC (Cost per Click) {#g-cpc}

**CPC (Cost per Click)** — cost или spend на qualifying clicks по disclosed rule: `CPC = cost / qualifying clicks`. Bid/target CPC не равен фактическому average CPC: первый — ставка или цель оптимизации, второй — post-fact среднее.

**Пример:** $96 на 160 qualifying clicks — average CPC $0.60, независимо от того, какие bids выставлялись по ходу периода.

### CPA (Cost per Action) {#g-cpa}

**CPA (Cost per Action)** — cost на advertiser-defined qualifying actions: `CPA = cost / qualifying actions`. Action определяется контрактом кампании — trial, order, lead или subscription, не обязательно новый customer, поэтому CPA нельзя читать без имени action и сравнивать между кампаниями напрямую.

**Пример:** $96 на 24 attributed subscriptions — CPA $4 при action = attributed subscription; для соседней кампании action — lead, и её CPA с этим числом несопоставим.

### CPI (Cost per Install) {#g-cpi}

**CPI (Cost per Install)** — cost mobile acquisition на qualifying installs: `CPI = cost / qualifying installs`. Install count зависит от measurement и attribution rules, поэтому CPI сравним только при названных правилах подсчёта установок.

**Пример:** $5,000 spend на 2,500 attributed installs — CPI $2 по правилам выбранного MMP; другой attribution window даст другой install count и другой CPI.

### CPL (Cost per Lead) {#g-cpl}

**CPL (Cost per Lead)** — cost на business-defined qualifying leads: `CPL = cost / qualifying leads`. Lead definition и качество различаются между бизнесами, и lead ещё не customer, поэтому низкий CPL бесполезен без qualification.

**Пример:** $2,000 на 100 отправленных форм — CPL $20; если четверть leads не проходит qualification, эффективная стоимость заметно выше.

### CAC (Customer Acquisition Cost) {#g-cac}

**CAC (Customer Acquisition Cost)** — allocated acquisition costs бизнеса на новых customers: `CAC = allocated acquisition costs / new customers`. Шире platform CPA: в numerator могут входить media, agency, sales и onboarding costs, а new customer определяется бизнес-правилом (например первая подтверждённая оплата). Platform CPA нельзя переименовать в CAC, пока customer event, period, cost allocation и refunds не согласованы.

**Пример:** platform report показывает $4 CPA за подписку, но бизнес включил в acquisition costs media, agency и onboarding и признаёт customer с первой оплаты — его CAC оказался $7.

### Revenue {#g-revenue}

**Revenue (выручка)** — сумма, признанная выбранной entity по её правилам учёта на её ledger boundary. Estimated dashboard value, invoiced amount, settled amount и recognized revenue могут быть разными состояниями одной цепочки; для сравнения нужно согласовать period, timezone, currency conversion, taxes/refunds и participant. Сколько из прошедших через платформу денег она признаёт revenue, зависит от её роли principal или agent (gross/net presentation), а не от размера invoice.

**Пример:** через network прошли $100 advertiser, publisher получил $68. При gross presentation network признаёт $100 revenue, при net — только свои $20; обе записи корректны для своей boundary и своей accounting conclusion.

### Cost {#g-cost}

**Cost (затраты)** — расходы той entity, чью экономику анализируют, в выбранном scope: для advertiser — media cost, для platform — downstream cost, для бизнеса — более широкий набор расходов. Не синоним spend: spend — расход buyer на media, cost может включать неплатёжные и вне media составляющие и всегда привязан к perspective.

**Пример:** advertiser потратил $96 media spend, но его полный cost с delivery продукта, agency и operations — $600; ROI считается по второй сумме.

### ROAS (Return on Ad Spend) {#g-roas}

**ROAS (Return on Ad Spend)** — media efficiency: attributed conversion value или revenue на ad spend: `ROAS = attributed conversion value or revenue / ad spend`; записывается как `5.0x` или `500%`. Attribution-dependent: зависит от attribution rules и выбранного value field и без causal design не доказывает incremental return. Высокий ROAS совместим с отрицательным ROI.

**Пример:** $480 attributed conversion value при $96 ad spend — ROAS 5.0x; но при полном cost $600 тот же campaign убыточен.

### ROI (Return on Investment) {#g-roi}

**ROI (Return on Investment)** — прибыльность более широкого investment scope: `ROI = net profit / total relevant investment cost = (return − total relevant cost) / total relevant cost`. В отличие от ROAS использует полный выбранный cost scope, а не только ad spend.

**Пример:** return $480 при полном cost $600 — net profit −$120 и ROI −20%, хотя ROAS по media spend равен 5.0x.

### ARPU (Average Revenue per User) {#g-arpu}

**ARPU (Average Revenue per User)** — selected revenue на всех eligible users выбранной population или cohort за период: `ARPU = selected revenue / all eligible users`. Требует user definition, revenue categories (purchase, subscription, ad), period и cohort/population; включает non-paying users.

**Пример:** 1,000 active users принесли $1,000 recognized revenue за месяц — ARPU $1; о lifetime это число ничего не говорит без cohort и horizon.

### ARPPU (Average Revenue per Paying User) {#g-arppu}

**ARPPU (Average Revenue per Paying User)** — revenue на paying users: `ARPPU = selected revenue от payers / paying users`. Делит только на payers и требует payer event, состав revenue (purchase, subscription), правил refunds и period. Обычно выше ARPU той же population, но не всегда: если ARPU включает ad revenue от неплатящих users, а ARPPU — только purchase revenue, соотношение может перевернуться; какой revenue входит в numerator — часть contract метрики.

**Пример:** те же $1,000 purchase revenue от 100 платящих из 1,000 users — ARPPU $10 при ARPU $1.

### LTV (Lifetime Value) {#g-ltv}

**LTV (Lifetime Value)** — cumulative observed или predicted value cohort members: `LTV = cumulative observed or predicted value / cohort members`. Требует cohort, horizon, identity rule, value basis (revenue или contribution) и статуса observed/predicted; revenue LTV не вычитает расходы, contribution LTV считается на оговорённой маржинальной basis. Без этих определений «LTV пользователя» — не определённый scalar.

**Пример:** observed 30-day revenue LTV cohort установок — $4.20; predicted 12-month contribution LTV по модели — $6.80: это разные метрики, а не одно число с разной точностью.

### Fill rate {#g-fill-rate}

**Fill rate** — доля eligible ad requests, на которые нашёлся ответ с рекламой (fill), например `filled responses / eligible ad requests`. Publisher/ad server metric перехода request → fill; безопасного vendor-neutral denominator нет — product может делить filled responses, matched bids или counted impressions на requests, opportunities или ad units, и это разные метрики. Fill — не конечный outcome: filled response может не render-иться и не стать counted impression, поэтому fill rate на response basis выше доли реально доставленных показов. Не синоним match, response и delivery rate.

**Пример:** 80,000 filled responses на 100,000 eligible ad requests — fill rate 80%; если 78,000 из них стали counted impressions, доля доставленных показов — 78%, и product может называть fill rate любую из двух величин.

### Win rate {#g-win-rate}

**Win rate** — доля submitted eligible bids, выигравших аукцион: `winning bids / submitted eligible bids`. Buyer/deal metric перехода bid → auction win; требует раскрытия population. Win notice ещё не delivery и не billing event: аукцион может выбрать bid победителем, но creative не будет доставлен или impression не станет billable.

**Пример:** 9,000 wins на 45,000 bids — win rate 20%, при этом counted/billable impressions 8,000: win и billing — разные event points, расхождение не ошибка.

### Ledger boundary {#g-ledger-boundary}

**Ledger boundary (граница учёта)** — граница, внутри которой entity признаёт и регистрирует суммы и события по собственным правилам: одна и та же сумма является revenue на одной boundary и downstream media/traffic cost на другой. Из-за разных ledger boundaries отчёты advertiser, platform и publisher об одной сделке закономерно не совпадают и не обязаны совпадать.

**Пример:** advertiser потратил $100; network на своей boundary записала $100 billed и $80 payable (признав revenue $100 или $20 в зависимости от gross/net presentation); publisher увидел $68 receivable — числа разные, потому что каждая запись живёт в своём ledger.

### Pricing basis {#g-pricing-basis}

**Pricing basis** — договорное правило расчёта цены: объект, за который buyer платит, — impression, click, action, install, lead, доля proceeds, период доступа к software или иной согласованный результат. Название метрики в интерфейсе (`CPM`, `CPC`, `CPA`) не задаёт basis само по себе: одно и то же имя может быть договорной ценой, bid или фактическим средним после событий, поэтому денежное обязательство создаёт только названная в договоре basis.

**Пример:** договор «`$10 CPM`, billable event — rendered impression» и договор «`$10 CPA`, billable event — подписка» дают одинаковую цифру цены, но разное распределение риска вдоль воронки.

### Billable event {#g-billable-event}

**Billable event** — qualifying-событие, определённое договором, после которого payee вправе начислить billable amount — сумму по pricing basis после counts, rates, validation и договорных adjustments; она ещё не обязательно выставлена в invoice, признана revenue или оплачена. Событие задаётся contract policy, а не протоколом автоматически: auction win, win notice и billing notice — разные точки, и win не гарантирует delivery или charge.

**Пример:** в OpenRTB win notice (`nurl`) и billing notice (`burl`) разделены — аукцион выбрал bid победителем, но начисление возникает только после договорного события, например rendered impression.

### Payee / payer {#g-payee-payer}

**Payee / payer** — две стороны одного платёжного обязательства: payer платит за billable event, payee получает оплату. В pricing model распределение риска описывается через них: при CPM payee получает право на charge раньше воронки, а post-impression risk несёт payer; при CPA payee принимает на себя весь риск до конверсии. Одна компания может быть payee в одном договоре и payer в другом.

**Пример:** в сделке advertiser → network → SSP → publisher network — payee по договору с advertiser и payer по договору с SSP.

### Revenue share {#g-revenue-share}

**Revenue share** — договорное распределение названной revenue или proceeds base между сторонами в заданной доле. Без раскрытия базы не определён: нужно знать, чьи proceeds, на какой ledger boundary, за какой период, до или после каких agreed adjustments и кто выполняет расчёт; доля от одной boundary не равна доле от исходного advertiser spend.

**Пример:** SSP удерживает 15% от `$80` proceeds на своей boundary — `$12`; относительно исходного `$100` advertiser spend те же `$12` составляют 12%.

### Fixed fee {#g-fixed-fee}

**Fixed fee** — заранее согласованная сумма за period, scope или deliverable, не зависящая от объёма media transaction: agency retainer, setup или managed-service fee, minimum monthly commitment, flat sponsorship fee. Обычно это отдельный от media money поток: он не вычитается из media dollar и не становится publisher payout или take rate — если только конкретный договор не объединяет software и media charges в один invoice. Выбирают ради предсказуемости и чтобы снять конфликт «fee растёт вместе со spend»; provider несёт риск, что согласованный scope потребует больше работы.

**Пример:** `$2,000/month` за доступ к ad server — service charge по отдельному договору; если сверх этого действует usage tier по числу обработанных impressions, это уже usage pricing, а не fixed fee.

### SaaS pricing {#g-saas-pricing}

**SaaS pricing** — модель оплаты software-платформы: subscription, seats, usage tier или processed volume за доступ к продукту. Образует отдельный software/service flow: usage event платформы не становится media event автоматически, а SaaS charge не превращает отношение в покупку inventory.

**Пример:** платформа тарифицирует `$2,000/month` плюс tier по числу processed impressions; рост объёма меняет tier, но не делает этот платёж стоимостью media.

### Markup {#g-markup}

**Markup** — надбавка к base cost, выраженная долей от cost denominator: `markup = (selling amount − acquisition cost) / acquisition cost`. Не равен spread (абсолютной разнице) и gross margin (которая использует accounting revenue и cost of revenue reporting entity); сравним только при названных buy/sell amounts.

**Пример:** сеть покупает media за `$80` и продаёт advertiser за `$100`: spread `$20` — это 25% markup на acquisition cost и одновременно 20% take rate относительно spend.

### Take rate {#g-take-rate}

**Take rate** — retained amount относительно названного transaction flow на выбранной boundary: `take rate = retained amount / named transaction flow`. Сравним только при раскрытых numerator, denominator и included fees: одна и та же сумма даёт разные ставки относительно boundary proceeds и исходного advertiser spend.

**Пример:** SSP удерживает `$12` из `$80` proceeds — take rate 15% на своей boundary, но 12% относительно исходного `$100` spend.

### Spread {#g-spread}

**Spread** — абсолютная разница между selling amount и acquisition/downstream amount на названной boundary. Экономическое ядро resale- и arbitrage-моделей посредника; markup и take rate вычисляются из одного spread с разными denominators и без named boundary несравнимы.

**Пример:** покупка media за `$80` и продажа за `$100` — spread `$20`; это 25% markup на cost и 20% take rate на spend одновременно.

### Proceeds {#g-proceeds}

**Proceeds** — сумма transaction inflow до согласованного распределения на выбранной boundary. Слово `gross` рядом с proceeds описывает base до split, а не автоматически `gross revenue` в финансовой отчётности: для расчёта долей важны boundary, период и допустимые deductions.

**Пример:** SSP-boundary proceeds `$80` делятся на `$12` retained и `$68` publisher share; относительно исходного `$100` advertiser spend это другие проценты.

### Retained amount {#g-retained-amount}

**Retained amount** — часть transaction flow, остающаяся у participant на его boundary до его собственных costs. Характеризует transaction economics, но не является recognized revenue или profit: accounting presentation и расходы определяются отдельной policy entity.

**Пример:** в разложении `$100 → $80 → $68` network retained `$20`, SSP retained `$12` — обе суммы являются остатками flow, а не accounting profit.

### Gross/net revenue presentation {#g-gross-net-revenue}

**Gross/net revenue (presentation)** — вариант отражения revenue reporting entity: gross показывает согласованную оплату целиком, net — только fee или commission. Выбор следует contract-specific principal-agent assessment для конкретного specified good/service, а не логике «деньги до/после расходов»: label продукта, invoice или gross billings сами по себе вывод не определяют.

**Пример:** network с `$100` sell и `$80` supplier component при principal conclusion показывает revenue `$100` и cost of revenue `$80`; при agent conclusion — только net fee `$20`.

### Gross billings {#g-gross-billings}

**Gross billings** — сумма, выставленная клиентам или прошедшая через collection до исключения supplier components; более широкая величина, чем recognized revenue, и не его synonym. Billings описывают биллинг, а не accounting conclusion principal/agent.

**Пример:** платформа при agent conclusion показывает gross billings `$100` с receivables/payables, а recognized revenue — только net fee `$20`.

### Cost of revenue {#g-cost-of-revenue}

**Cost of revenue (CoR)** — расходы, которые reporting entity классифицирует как непосредственно связанные с получением признанного revenue по своей policy. Не любой cash outflow: состав определяется policy компании, а operating expenses, interest и taxes находятся ниже gross profit.

**Пример:** при gross presentation supplier component `$80` показывается как cost of revenue рядом с recognized revenue `$100`.

### Gross margin {#g-gross-margin}

**Gross margin** — доля recognized revenue, остающаяся после cost of revenue той же reporting entity на той же accounting basis: `gross margin = (recognized revenue − cost of revenue) / recognized revenue`; gross profit — числитель этой формулы. Не равна take rate, который делит retained amount на named transaction flow.

**Пример:** gross presentation: revenue `$100`, CoR `$80` — gross profit `$20`, margin 20%; тот же business в net presentation показывает margin 100% при тех же `$20` economics — margin зависит от presentation.

### Principal / agent {#g-principal-agent}

**Principal / agent** — accounting assessment роли reporting entity относительно конкретного обещанного specified good/service: principal контролирует его до передачи customer и показывает оплату gross, agent организует предоставление другой стороной и показывает net fee/commission. Control — способность направлять использование и получать существенные benefits до transfer; `primary responsibility`, `inventory risk` и `pricing discretion` — evidence, а не механический score; одна компания может быть principal в одном flow и agent в другом.

**Пример:** AdTech-платформа при agent conclusion признаёт net fee по platform transactions, но может быть principal по отдельным insertion-order campaigns, где сама обязуется поставить delivery.

### Arbitrage {#g-arbitrage}

**Arbitrage** — модель intermediary, которая покупает media/traffic дешевле и продаёт дороже либо покупает на одной pricing basis, а продаёт на другой. Экономика держится на spread в обмен на принятый риск: volume/fulfillment, basis mismatch и reconciliation risk могут обратить spread в loss. Не любой intermediary fee — arbitrage, и arbitrage не автоматически злоупотребление; проблема — opacity buy/sell basis и spread для customer.

**Пример:** network обязалась купить batch media за `$80`, но продала advertiser только часть согласованного scope — непроданный остаток cost ложится на неё, spread уменьшается или становится loss.

### Basis mismatch {#g-basis-mismatch}

**Basis mismatch** — покупка и продажа одной media на разных pricing basis, например покупка impressions по CPM и продажа clicks или actions по CPC/CPA. Добавляет performance risk к arbitrage: revenue посредника зависит от realised CTR/CVR и validation, а исходная media cost остаётся, если downstream billable amount не покрывает её.

**Пример:** посредник купил impressions за `$80` в расчёте на 100 clicks, зарегистрировано 60 — выручка по CPC не покрывает media cost.

### Optimization event {#g-optimization-event}

**Optimization event** — наблюдаемое событие, под которое система доставки обучается и оптимизирует показы: install, trial start, paid subscription, purchase. Выбирается advertiser в настройках campaign (у разных platforms — conversion action, conversion goal, performance goal). Не равно campaign objective (бизнес-намерение), не равно billable event (за что платят) и не равно параметру стратегии вроде `target CPA`. Более глубокое событие даёт меньше сигналов и дольше learning.

**Пример:** objective «рост paid subscriptions», optimization event сначала `install` (много сигналов), затем переключён на `paid_subscription`; billing при этом остался CPM.

### Optimization target {#g-optimization-target}

**Optimization target** — outcome, под который bidding system настраивает будущие решения: чаще всего это optimization event (install, paid subscription) плюс цель по нему. Не путать с параметром стратегии: `target CPA $4` — это ограничение bid strategy, а не событие, которое система предсказывает. Не превращает договор в CPA billing: payment model устанавливает contract, realized metrics описывают случившееся post-fact, optimization target влияет только на decisions до события.

**Пример:** advertiser платит CPC за qualifying clicks, а система оптимизируется под paid subscription с ограничением `target CPA $4` — billing basis, optimization event и параметр стратегии сосуществуют в одной кампании.

### Ad account (advertiser account) {#g-ad-account}

**Ad account (advertiser account, рекламный аккаунт)** — tenant на advertising platform, внутри которого существуют campaigns и связанные настройки; образует сразу несколько границ: ownership и access (роли и permissions операторов), billing identity, currency и time zone, namespace идентификаторов и shared configuration (data sources, brand assets, defaults). Юридическая компания advertiser и ad account — не одно и то же: у одной компании может быть несколько accounts под регионы, бренды и валюты, а один account может обслуживать несколько инициатив одной legal entity.

**Пример:** Subscription App Ltd. ведёт ad account EU (EUR, time zone Europe/Berlin) и отдельный ad account US (USD); agency получает delegated доступ к обоим, но owner и billing identity остаются у advertiser.

### Manager account {#g-manager-account}

**Manager account** — административный слой platform, который даёт agency или внутренней группе централизованный delegated доступ к нескольким ad accounts. Это administrative access, а не дополнительный delivery-уровень: manager account не участвует в delivery-иерархии каждой campaign.

**Пример:** agency получает manager-доступ к ad accounts десяти клиентов — операторы заходят через один вход, но budget, targeting и отчётность каждого account остаются раздельными.

### Ad {#g-ad}

**Ad (объявление)** — исполняемая delivery-единица кампании: связывает parent group (ad group или ad set), advertiser identity, creative, destination, tracking и status. Ad — не то же, что creative: один creative может исполняться в нескольких ads с разными parent rules, destinations и состояниями.

**Пример:** video creative переиспользуется двумя ads: один ведёт в store listing для новых users, второй — deep link в приложение для установивших; у каждого ad свой ID, status и tracking settings.

### Ad group / ad set {#g-ad-set}

**Ad group / ad set** — промежуточный уровень иерархии кампании между campaign и ad, группирующий ads с общими execution rules. Названия и состав полей vendor-specific, универсальной schema нет: в Google-like модели ad group объединяет близкие ads и triggering criteria (например related keywords), в Meta-like модели ad set хранит audience, placements, optimization, bid, budget и schedule.

**Пример:** в Meta-кампании ad set «US» содержит audience, placements и budget, а внутри него — три ads с разными creatives; в Google Ads ту же роль middle layer играет ad group с keywords.

### Campaign objective {#g-campaign-objective}

**Campaign objective (цель кампании)** — high-level business intent или setup guidance, сообщённый platform при создании кампании: awareness, traffic, leads, app promotion, sales. Objective предлагает campaign types, features и defaults, но не обязан совпадать с событием, которое optimizer непосредственно предсказывает: optimization event выбирается отдельно.

**Пример:** подписочный сервис выбирает objective `App promotion`, а optimization event — `paid_subscription`: objective описывает intent, наблюдаемый signal для delivery определяется отдельно.

### Targeting {#g-targeting}

**Targeting (таргетинг)** — правила кампании о том, кому и где может быть показана реклама: hard controls (eligibility rules — geo, device, context, audience/keyword criteria, exclusions), которые ограничивают множество допустимых opportunities, и signals/hints, которые в algorithmic products лишь направляют delivery, не сужая eligible set. Targeting отвечает на вопрос «для каких opportunities/users/contexts возможен показ», в отличие от placement («где именно») и optimization («какой из допустимых показов выбрать»); даже если API хранит их в одном объекте, это разные оси.

**Пример:** ad set ограничен geo `DE`, мобильными устройствами и exclusion «уже установили приложение» (hard controls); seed-аудитория ценных подписчиков передана как signal — система может показывать и вне неё, но внутри `DE + mobile`.

### Bid strategy {#g-bid-strategy}

**Bid strategy (стратегия ставок)** — policy, которая переводит optimization goal и ограничения (target или cap) в auction bids. Strategy, её target/cap, actual bid на конкретную opportunity и billable price — четыре разные сущности: один числовой `target CPA` не является actual bid, а actual bid не определяет billable amount сам по себе.

**Пример:** стратегия «maximize conversions с target CPA $4» сама решает, сколько предложить за каждый показ; фактическая ставка может быть $1 или $9, а charge определит pricing basis договора.

### Budget {#g-budget}

**Budget (бюджет)** — ограничение доступного spend на заданной scope (campaign, ad set, shared pool нескольких campaigns) и time basis. Распространены daily budget (жёсткий календарный cap, average daily target или иная форма — определяет product) и lifetime/flight budget на весь interval. Budget ограничивает расход, но не гарантирует inventory, conversions, равномерный расход или точный invoice amount.

**Пример:** campaign получила lifetime budget €700 на семидневный flight с двумя ad sets — нельзя заключить ни €100/день, ни €350 на каждый ad set: allocation зависит от opportunities и product configuration.

### Pacing {#g-pacing}

**Pacing (темп расхода)** — политика распределения spend во времени внутри budget-ограничений: тратить ли равномерно, ускоряться на дешёвых или качественных opportunities или придерживать бюджет. Pacing распределяет ресурс, но не обещает равномерный расход: доступные opportunities и allocation меняются.

**Пример:** при lifetime budget €700 на неделю система может потратить €180 в первый день на дешёвый inventory и меньше в остальные — pacing оптимизирует результат, а не календарную равномерность.

### Schedule (flight) {#g-schedule}

**Schedule (flight, расписание кампании)** — временная eligibility кампании: start и end, account time zone, в которой интерпретируются даты, и при поддержке product — dayparting (допустимые дни недели и часы). До start кампания может быть enabled, но иметь effective status `pending`; после end она завершается, даже если часть budget не потрачена.

**Пример:** campaign enabled со start 2026-09-07 00:00 Europe/Berlin — до этой даты показов нет, а dayparting «только рабочие часы» делает её временно ineligible внутри активного flight.

### Destination (landing page) {#g-destination}

**Destination (landing page, final URL)** — первая целевая поверхность после interaction с рекламой: web page, App Store/Google Play listing или deep link в app. Это часть user path, а не tracking record: tracking template и URL parameters управляют measurement path, но landing page не являются.

**Пример:** ad обещает premium-функции и ведёт в store listing — destination должна описывать тот же product и offer, иначе обещание creative и то, что видит user, расходятся.

### Tracking settings {#g-tracking-settings}

**Tracking settings (настройки отслеживания)** — configuration observability кампании: передаваемые identifiers (campaign/group/ad IDs), URL parameters, macros, tracking template и final URL suffix, event sources (pixel, app SDK, server-to-server integration, MMP), выбранные conversion actions и attribution configuration boundary. Tracking settings управляют measurement path и не заменяют destination; имена URL-параметров не являются industry standard.

**Пример:** tracking template ведёт click через measurement-домен с macros `{campaignid}` и `{creative}`: platform подставляет фактические IDs в момент click, а user идёт к destination своей дорогой.

### Conversion action {#g-conversion-action}

**Conversion action** — настроенное на платформе определение события, которое считается conversion для отчётности и optimization: источник (pixel, SDK, S2S, импорт), имя события, правила counting (одна или каждая на interaction), value и окно. Platform может иметь несколько conversion actions на account; какие из них primary (используются для optimization) и какие secondary (только отчётность) — часть конфигурации campaign.

**Пример:** в account настроены conversion actions `install`, `trial_started` и `paid_subscription`; campaign оптимизируется под primary `paid_subscription`, остальные видны в отчёте как secondary.

### Learning phase {#g-learning-phase}

**Learning phase (learning status, фаза обучения)** — состояние optimizer, в котором delivery/bidding model собирает evidence после запуска или material configuration change: прежние данные хуже описывают новые решения. Learning — одна из осей operational state наряду с configured, effective и review status, а не противоположность active: показы и spend идут, а vendor-specific significant edits (targeting, creative, optimization event, состав ads, bid strategy) могут вернуть optimizer в learning без изменения configured status.

**Пример:** ad set со stable delivery по installs переводят на optimization event `paid_subscription` — configured status остаётся `active`, но optimizer снова в learning, пока не соберёт достаточно данных по новому событию.


### Audience segment {#g-audience-segment}

**Audience segment** — addressable set entities, membership которого задают named rule, data source/provenance, observation window и platform matching/activation contract; entity может быть user, account, device, browser, household или modeled profile, поэтому segment не обязательно является списком известных людей.

**Пример:** segment `trial_started AND no paid_subscription within 7d` содержит только те platform-addressable entities, которых удалось сопоставить с подходящими product events.

### Observation window {#g-observation-window}

**Observation window (окно наблюдения)** — период, за который событие учитывается при формировании audience segment: «trial начат за последние 7 дней», «посещал страницу цен за 30 дней». Определяет свежесть membership и размер сегмента. Не путать с attribution/lookback window (за какой срок до conversion учитывать touchpoint) и с conversion window (сколько ждать conversion после click): это окна разных механизмов.

**Пример:** сегмент `trial_started ≥ 7d ago AND no paid_subscription` — observation window отбирает пользователей, у которых trial начался не менее недели назад.

### Addressable {#g-addressable}

**Addressable (адресуемый)** — пользователь, устройство или домохозяйство, которые платформа способна опознать по доступному identifier и доставить им конкретный показ; addressability — доля inventory или аудитории, для которой это возможно. Зависит от среды (browser, iOS, Android, CTV), consent и доступных identifiers, поэтому один и тот же сегмент может быть активируемым на одной платформе и пустым на другой.

**Пример:** список из 100,000 email-адресов после matching дал 40,000 addressable users в одной платформе и 25,000 — в другой: остальных платформы опознать не смогли.

### First-party audience {#g-first-party-audience}

**First-party audience** — audience segment, построенный из data, собранных advertiser или publisher в direct relationship: CRM/customer records, site/app events, subscriptions и purchases. `First-party` описывает provenance, но не гарантирует consent, legal basis, ownership, accuracy или полноту platform match.

**Пример:** subscription app передаёт platform собственный segment пользователей, начавших trial, но ещё не оформивших платную подписку.

### Third-party audience {#g-third-party-audience}

**Third-party audience** — audience segment, поставляемый внешним data provider независимо от direct relationship advertiser с entity; для оценки segment нужны provenance, collection method, recency, membership criteria, modeling metadata, permissions и activation coverage, поскольку label сам по себе не доказывает состав или точность.

**Пример:** provider продаёт segment `likely subscription buyers`; advertiser проверяет происхождение, окно наблюдения и долю modeled membership до activation в DSP.

### Contextual targeting {#g-contextual-targeting}

**Contextual targeting** — выбор ad opportunities по текущему content или media context: topic, semantics, page/app/video category и связанным signals. Он описывает среду показа и не требует утверждения, что известна устойчивая cross-site identity user.

**Пример:** реклама hiking boots допускается в статьях о зимних походах независимо от того, известна ли platform история конкретного читателя.

### Retargeting {#g-retargeting}

**Retargeting** — targeting entities, ранее выполнивших named interaction или event в заданном observation window, чтобы обратиться к ним повторно; это delivery tactic, а не attribution rule и не доказательство causal effect.

**Пример:** user начал trial, но не купил subscription за семь дней, поэтому входит в segment для повторного показа premium-offer.

### Seed audience {#g-seed-audience}

**Seed audience (исходная аудитория)** — набор известных entities (например, платящие подписчики с высокой ценностью), который advertiser передаёт платформе как образец для построения lookalike или как signal для algorithmic delivery. Качество и размер seed определяют качество модели: слишком маленький seed даёт шум, слишком широкий — размывает признаки. Seed сам по себе не является целевой аудиторией показа; многие платформы по умолчанию исключают его из lookalike.

**Пример:** seed — `paid subscribers with 90-day value > €50`; платформа строит по нему lookalike из новых пользователей с похожими признаками.

### Prospecting {#g-prospecting}

**Prospecting (привлечение новых)** — направление кампании на пользователей, у которых ещё не было взаимодействия с advertiser: lookalike, interest, contextual или broad targeting. Противоположность retargeting и re-engagement, которые обращаются к уже известным пользователям. Для prospecting характерны меньшая конверсия и большая ценность incremental результата, поскольку пользователь не пришёл бы сам.

**Пример:** campaign с lookalike по seed платящих подписчиков и exclusion всех текущих пользователей приложения — prospecting; campaign на trial-пользователей без оплаты — retargeting.

### Lookalike audience {#g-lookalike-audience}

**Lookalike audience** — modeled audience новых prospects, найденных по similarity или predicted relevance к seed audience; результат зависит от seed quality и platform model, а использование lookalike в delivery может быть hard constraint или suggestion согласно product contract.

**Пример:** high-value subscribers образуют seed, по которому platform ищет новых prospects, не обязанных входить в исходный segment.

### Audience exclusion / suppression {#g-audience-exclusion}

**Audience exclusion / suppression** — отрицательное targeting rule, предназначенное не допустить entities с named membership или status; фактическая полнота exclusion ограничена identity match, freshness, propagation latency и semantics конкретной platform.

**Пример:** acquisition campaign исключает current paid subscribers, но поздно пришедшее subscription event может временно оставить нового customer вне suppression segment.

### Audience overlap {#g-audience-overlap}

**Audience overlap** — пересечение memberships нескольких audience segments в одной activation universe и на одном snapshot; оно влияет на distinct reach, reporting и segmentation design, но само по себе не доказывает duplicate billing или self-competition.

**Пример:** часть entities одновременно входит в `trial_no_purchase` и `existing_paid`, что указывает проверить event freshness и membership rules.

### Algorithmic / broad targeting {#g-algorithmic-targeting}

**Algorithmic targeting** — delivery mode, в котором model использует optimization goal, context, audience seeds и другие signals для поиска и ранжирования opportunities, потенциально за пределами suggested segments, но внутри заявленных hard controls и exclusions. **Broad targeting** — setup с минимумом positive audience restrictions, а не отсутствие constraints.

**Пример:** system ищет likely subscribers вне lookalike seed, сохраняя hard controls `DE + mobile` и exclusion current paid subscribers.

