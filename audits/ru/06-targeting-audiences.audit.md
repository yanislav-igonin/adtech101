<!-- Повторный аудит после редакторского прохода 2026-10-09. Предыдущий аудит доредакционной версии заменён; независимое ревью, по которому делались правки, — review-2026-10-09/ch06.md -->

# Повторный аудит главы 6 «Targeting и Audiences» (после правок 2026-10-09)

Входы: `master-prompt.md` §10 (строка «#### 6.», пункты 6.1–6.19), `plans/ru/06-targeting-audiences.plan.md`, `chapters/ru/06-targeting-audiences.md`, `chapters/en/06-targeting-audiences.md`, `glossary.md`, контракт оформления (§7 Stage B) и языковой контракт (§3). Режим — только чтение. Предыдущее ревью `review-2026-10-09/ch06.md` открыто только после вынесения вердикта (см. Приложение).

---

# Часть 1. Coverage & Accuracy Auditor (RU)

# Резюме аудита

Содержательно глава готова: все 19 TOC-требований раскрыты на нужной глубине, включая добавленные сегодня 6.18 (first-party data vs first-party identity, строка 177 + bullet в «С чем это часто путают») и 6.19 (addressability как caveat с forward refs на главы 24 и 40–42, строки 153 и 204). Фактических ошибок, перепутанных ролей и устаревших утверждений, поданных как текущие, не найдено; vendor-примеры (Google advanced location options, Customer Match, optimized targeting, Demand Gen Lookalike; Meta Advantage+ audience) корректно помечены как product-specific. Данные и деньги разведены (строки 59–75). Все 37 сносок `[^g-…]` резолвятся в `glossary.md`, каждая стоит один раз и при первом упоминании.

Вердикт `PASS` блокируют три нарушения контракта оформления/языка (все — механические, правятся локально без изменения смысла):

1. бытовая латиница, прямо названная в §3 как нарушение: `entity/entities` (~25 употреблений в прозе) и `boundary/boundaries` (5);
2. пять терминов с статьёй в глоссарии без сноски: `bid`, `auction`, `conversion rate`, `optimization event`, `measurement`;
3. дата в vendor-примере в прозе: «с марта 2024 года» (строка 179).

# Блокеры

None.

# Важные проблемы

1. **Бытовые английские слова из явного списка §3.** Контракт перечисляет `entity` и `boundary` как слова, которые пишутся по-русски. В прозе главы `entity/entities` встречается ~25 раз (строки 39, 79, 118, 153, 155, 156, 159, 175, 183, 204, 209, 218, 229, 246, 249–250, 253, 255, 273, 307, 317, 330), `boundary/boundaries` — 5 раз (строки 110 «strict boundary», 200 «match boundary», 242 «suggestion, а не boundary», 281 «audience boundaries», 287 «остаются boundaries»). В большинстве мест замена безболезненна: «сущность», «объект», «граница». Замечание: `entity` используется и в статьях `glossary.md` (`g-audience-segment`, `g-third-party-audience`, `g-audience-exclusion`), а предыдущее ревью (§7 п. 6) предлагало «оставить как термин с пояснением» — это противоречит §3, и оркестратору стоит выбрать одно решение для главы и глоссария сразу. Пока контракт звучит так, как записан, это нарушение.
2. **Термины с статьёй в глоссарии без сноски** (контракт: «каждый термин, имеющий статью в glossary.md, получает сноску»):
   - `bid` — строка 75 («не определяет bid, budget[^g-budget] или pacing[^g-pacing]»), статья `{#g-bid}`;
   - `auction` — строка 273 («семантика auction и dedup зависит от платформы»), статья `{#g-auction}`;
   - `conversion rate` — строка 227 («высокий conversion rate может отражать уже существовавший intent»), статья `{#g-cvr}`;
   - `optimization event` — строка 311 («Какой optimization event направляет ranking?»), статья `{#g-optimization-event}` (при этом `optimization target` на строке 55 сноску имеет);
   - `measurement` — строка 204 («для targeting и measurement — главы 40–42»), статья `{#g-measurement}`.
3. **Дата vendor-примера в прозе.** Строка 179: «с марта 2024 года отдельные варианты activation на partner inventory ограничены в EEA, UK и Switzerland». §3: «В учебном тексте vendor-примеры приводятся без даты; если актуальность критична — „на момент написания“». Соседний пример про Demand Gen (строка 240) оформлен правильно («На момент написания…»). Дата должна остаться только в источнике 5.

# Необязательные улучшения

1. **Объём.** Чистая проза без front matter, таблиц, code blocks, заголовков и раздела источников — 2 780 слов (с источниками 2 985; основной текст до служебных секций — 2 496). Ориентир контракта — до 2 400. Превышение ~16 %, не «материальное», но кандидаты на сокращение есть: строка 57 (повтор про scope campaign/ad set из главы 5 — план разрешал одно предложение, здесь абзац), строка 135 (overloaded-смысл `placement` дословно дублирует статью `g-placement`), строка 290 и строка 303 (повторяют строку 75 про отнесение bids/budget/pacing к главе 7).
2. **`segment` до сноски.** Строка 73 «внешний data provider может добавить segment» употребляет слово за 80 строк до `Audience segment[^g-audience-segment]` (строка 153). Формально это не тот же термин, но для читателя — тот же; либо написать на строке 73 «audience segment» со сноской, либо оставить как есть.
3. **Шапка таблицы и подзаголовки.** Шапка «Hard controls» (строка 279) и подзаголовки «Geography (география)», «Demographics (демография)» — английский первым. Как established terms допустимы, но «Жёсткие controls» / «География (geography)» ближе к букве контракта.
4. **Прочая латиница вне явного списка §3**, где русский ничего не теряет: `composition` и `precedence` (строки 149, 246), `observability` (253), `leakage` (253, 297), `granularity` (98), `availability` (179), `outcome` (многократно). Это уже стилистика, не контракт.
5. **UA reduction** (строка 98): «браузеры урезают версию OS и browser в User-Agent» — точнее: Chrome замораживает версию OS и обнуляет minor-версию браузера, major-версия остаётся. Одно уточняющее слово («точную minor-версию и версию OS»).
6. **`brand-safety controls`** (строки 277, 287) используется без расшифровки и без ссылки на главу — одна скобка «(глава 37)» или полслова пояснения.
7. **Дублирование служебных секций.** «С чем это часто путают» п. 1 (Targeting ≠ optimization) и «Что важно запомнить» п. 1 говорят одно и то же; п. 5 обеих секций пересекаются (first-party / addressability). Суммарно 8 + 6 = 14 пунктов — на верхней границе лимита 12–14.

# Проверка корректности

- **Targeting vs optimization** (строки 16–55, 275–303): eligibility-предикат и delivery_score разделены корректно; явно сказано, что формула учебная. Верно.
- **Data flow / money flow** (строки 59–75): участники названы правильно (publisher/platform описывает opportunity, advertiser даёт controls/seeds/exclusions, data provider — segment, DSP/closed platform — matching/eligibility/ranking); деньги: targeting не задаёт pricing model, data fee отдельна, bid/budget/pacing — глава 7. Верно.
- **Geography** (88–92): presence vs interest, inferred nature, Google как product-specific пример — соответствует документации Google Ads. Верно.
- **Device/OS/browser** (94–98): разные оси, разная доступность, `unknown` — верно. UA reduction описан с небольшим упрощением (см. OPTIONAL 5).
- **Demographics** (100–110): declared/observed/inferred, `Unknown` не редкость, зависимость от policy — верно; юридика отложена.
- **Interest/behavior/contextual/keyword/placement** (112–149): contextual без cross-site identity — верно; две семантики keyword (search query vs content) — верно; keyword ≠ universal exact match — верно; `placement` как overloaded term с publisher-side/buy-side смыслом — согласуется с `g-placement` и с ракурсами 8.3/10.4.
- **Audience segment** (151–161): пять характеристик; observation window отделён от attribution window — верно и согласовано с `g-observation-window`.
- **First-party** (163–179): match/onboarding объяснён (что с чем сопоставляется); «first-party ≠ consent/legal basis/100 % match» — верно; Customer Match EEA/UK/CH ограничение на partner inventory — соответствует источнику 5.
- **Third-party** (181–214): DMP как контейнер, data fee поверх media cost, IAB Audience Taxonomy и Data Transparency Standard как nomenclature/disclosure, а не quality score — верно.
- **Retargeting** (216–227): remarketing как vendor-синоним; retargeting ≠ attribution ≠ incrementality — верно.
- **Lookalike** (229–242): seed → model → prospects; size vs similarity; lookalike не обязана включать seed; Demand Gen suggestion mode помечен «на момент написания» и ограничен одним campaign type; Meta Advantage+ — верно по источникам 7–8.
- **Exclusion/overlap** (244–273): precedence negative над positive; leakage из-за stale/unmatched/suggestion; Jaccard-формула и требование одной entity definition/universe/snapshot — верно; «overlap ≠ double charge» — верно.
- **Broad/algorithmic** (275–290): broad ≠ без правил; expansion только там, где input — suggestion; Google optimized targeting (Display vs Video/Demand Gen signals, Video placements как boundaries) и Meta controls/suggestions — соответствуют документации.
- **Current vs legacy:** Privacy Sandbox/Chrome cookies не упоминаются как текущая основа — верно по плану; «доступность identifiers … в последние годы менялась» без устаревших деталей.
- **Спорные пары из чеклиста:** Tracking vs Attribution, Attribution vs Incrementality, Identity vs Tracking — различены корректно (161, 177, 227, 320–321). Остальные пары главой не затрагиваются.

Материально неверных определений нет.

# Проверка границ и плотности

- **Границы плана соблюдены:** bid/budget/pacing — ссылки на главу 7 (75, 303); форматы/ad units — глава 8 (133); identity-механика — глава 24 (204); privacy/consent/addressability-последствия — главы 40–42 (108, 204). Campaign hierarchy из главы 5 упомянута одним абзацем (57) — на грани допустимого «короткого напоминания».
- **Повторы внутри главы:** лейтмотив `control ≠ signal` звучит ~12 раз (29, 41, 57, 240, 242, 277, 285–290, 299, 316, 328, 339) — педагогически оправдано, но вместе с итоговым walkthrough (292–303) и «шестью вопросами» (305–312) даёт ~16 % превышения ориентира по объёму. См. OPTIONAL 1.
- **Повтор соседних глав:** нет; упоминание learning phase (301) — уместная ссылка на главу 5.
- **Rabbit holes:** нет; vendor-детали ограничены двумя bullets (287–288).
- **Плотность:** высокая, но читаемая; таблицы (5), схемы (11 code blocks) согласованы с прозой; pseudo-JSON помечен «не vendor API».
- Плотность «С чем это часто путают» vs «Что важно запомнить» — см. OPTIONAL 7.

# Проверка контракта оформления

| Проверка | Результат |
|---|---|
| Ровно один H1 | ✅ строка 14 |
| `## Суть` (с подзаголовком через двоеточие) | ✅ строка 16 |
| Закрывающие секции `##` в фиксированном порядке и с фиксированными названиями | ✅ строки 314, 325, 334, 341 |
| Все секции `##`, подсекции `###` | ✅ |
| Заголовки секций по-русски / english только как термин | ✅ с оговоркой: «Geography (география)», «Demographics (демография)», «Subscription app: flow целиком» — термины, допустимо (OPTIONAL 3) |
| Шапки таблиц по-русски | ✅ с оговоркой: «Hard controls» (279) и «First-party/Third-party audience» (206) — термины (OPTIONAL 3) |
| Бытовые английские слова в прозе | ❌ `entity` ×~25, `boundary` ×5 — IMPORTANT 1 |
| Каждая `[^g-id]` резолвится в `{#g-id}` | ✅ 37/37 |
| Сноска при первом упоминании | ✅ для всех 37 (ранние вхождения `placement`, `data provider` — только в code blocks; `retargeting`, `prospects`, `overlap` — только в заголовках) |
| Один термин — одна сноска | ✅ все 37 по одному разу |
| Термины с статьёй в глоссарии имеют сноску | ❌ `bid`, `auction`, `conversion rate`, `optimization event`, `measurement` — IMPORTANT 2 |
| Даты проверки / research-пометки в прозе | ❌ «с марта 2024 года» (179) — IMPORTANT 3; «На момент написания» (240) — допустимая форма |
| YAML front matter полон и согласован с TOC | ✅ `toc_requirements` 6.1–6.19, `prerequisites` ch-01…ch-05, `part: II`, `language: ru` |
| Чистая проза ≤ ~2 400 слов | 🟡 2 780 (без источников) — ориентир, не жёсткое правило (OPTIONAL 1) |
| «Путают» и «Запомнить» не дублируют друг друга, ≤ 12–14 пунктов | 🟡 14 пунктов, одно явное пересечение (OPTIONAL 7) |

# Coverage Table

| Requirement | Status | Evidence / Explanation |
|---|---|---|
| 6.1 geography | ✅ COVERED | Таблица (83) + §Geography (88–92): country/region/city/postal/radius, likely/regular presence vs interest, best-effort inference, Google `Presence or Interest` как product-specific пример |
| 6.2 device | ✅ COVERED | Таблица (84) + §Device (96–98): device class vs model, Android tablet проходит OS rule и не проходит `phone only`, coarsening/spoofing/`unknown` |
| 6.3 OS/browser | ✅ COVERED | Строки 85, 96–98: OS family vs version vs browser family; in-app без browser attribute; explicit browser targeting может отсутствовать; UA reduction объяснён |
| 6.4 demographics | ✅ COVERED | Строки 86, 100–110: declared/observed/inferred, `age=25–34` как classification signal, `Unknown` сокращает eligible set, зависимость от policy, два вопроса перед добавлением |
| 6.5 interests | ✅ COVERED | Таблица (118) + строка 125: устойчивая affinity hypothesis, declared/inferred/partner, interest ≠ intent, source/recency/confidence |
| 6.6 behavior | ✅ COVERED | Таблица (119) + строка 127: named event + observation window[^g-observation-window], `viewed_boots within 14 days` vs `active shopper`, не гарантирует покупку |
| 6.7 contextual | ✅ COVERED | Таблица (120) + строка 129: topic/смысл/category текущего content, работает без cross-site identity, «читает сейчас» vs «интересуется вообще» |
| 6.8 keyword | ✅ COVERED | Таблица (121–122) + строка 131: search query/intent vs content keyword, не universal exact match, stemming/expansion/negative — по контракту продукта |
| 6.9 placement (ракурс: targeting axis) | ✅ COVERED | Таблица (123) + строки 133–135: явный «где» (property/app/site/channel/video/slot), отличие от contextual selection, overloaded publisher-side/buy-side, форматы — глава 8; JSON-пример (139–149) и AND/OR caveat |
| 6.10 first-party audiences | ✅ COVERED | Строки 163–179: источники (CRM, events, subscriptions), pipeline normalize→rule→match→addressable, что такое match/onboarding, first-party ≠ consent/ownership/100 % match, Customer Match как пример смены availability; сравнительная таблица 206–214 |
| 6.11 third-party audiences | ✅ COVERED | Строки 181–214: внешний provider, DMP как контейнер, data fee, flow originators→modeling→label→match→activation, чеклист из 6 пунктов, IAB Taxonomy/Data Transparency Standard ≠ quality score, таблица |
| 6.12 retargeting | ✅ COVERED | Строки 216–227: named interaction + window, remarketing как синоним, re-engagement vs prospecting, схема, ≠ attribution/incrementality |
| 6.13 lookalikes | ✅ COVERED | Строки 229–242: seed→features→similar prospects, seed quality, size vs similarity, не включает seed/не гарантирует conversion, Demand Gen suggestion mode и Meta Advantage+ как dated/product-specific примеры |
| 6.14 suppression/exclusion | ✅ COVERED | Строки 244–253 (+ таблица 39): negative predicate с precedence, acquisition/re-engagement/regulated примеры, leakage из-за stale/unmatched/suggestion |
| 6.15 overlap | ✅ COVERED | Строки 255–273: пересечение memberships в одной совокупности addressable entities, диагностика A∩B/A∩C/B∩C, Jaccard-доля с требованием одной entity definition/universe/snapshot, overlap ≠ double charge |
| 6.16 broad и algorithmic targeting | ✅ COVERED | Строки 275–290: broad ≠ отсутствие правил, таблица manual/broad/algorithmic, expansion только за suggestion, Google optimized targeting и Meta controls/suggestions без рекомендации |
| 6.17 targeting vs optimization | ✅ COVERED | Строки 16–55 (цепочка + `eligible(o)`/`delivery_score(o)`), 292–303 (walkthrough), 305–312 (шесть вопросов), bullet 316 |
| 6.18 first-party data vs first-party identity | ✅ COVERED | Строка 177: определения обоих, почему advertiser имеет и то и другое, но активация требует match с identity платформы показа; bullet 320 |
| 6.19 addressability как ограничение (caveat) | ✅ COVERED | Строка 153 (определение addressable[^g-addressable] inline), строка 204 (зависимость от среды browser/mobile OS, один segment активируем в одной платформе и пуст в другой; механика — глава 24, последствия — главы 40–42), п. 5 «Что важно запомнить» |

# Вердикт

**REVISION REQUIRED** — исключительно из-за трёх нарушений контракта оформления/языка (IMPORTANT 1–3). По coverage и корректности глава проходит; правки локальные и не требуют перевода заново — только синхронной правки EN (сноски и замена `entity/boundary` на EN не влияют, дата в строке 179 EN подлежит той же правке, если RU меняется).

---

# Часть 2. Translation Auditor (RU ↔ EN)

SOURCE_FILE: `chapters/ru/06-targeting-audiences.md`; TRANSLATION_FILE: `chapters/en/06-targeting-audiences.md`.

## Механическая сверка

| Проверка | RU | EN | Результат |
|---|---|---|---|
| Заголовки (количество/уровни/порядок) | 19 (1 H1, 13 H2, 5 H3) | 19 (1 H1, 13 H2, 5 H3) | ✅ идентичны по уровням и порядку |
| Служебные секции EN | — | `## The Core Idea: …`, `## Common Confusions`, `## What to Remember`, `## Check Yourself`, `## Sources and Further Reading` | ✅ |
| Code blocks | 11 | 11 | ✅ те же языки (`text`/`json`), тот же порядок |
| Строки таблиц | 31 | 31 | ✅ |
| Пункты списков | 54 | 54 | ✅ |
| Ссылки `](http` | 8 | 8 | ✅ одинаковые URL |
| Сноски `[^g-…]` | 37 (все ×1) | 37 (все ×1) | ✅ множество и счётчики побайтно совпадают |
| Абзацы прозы (непустые строки вне таблиц/кода/заголовков) | 110 | 110 | ✅ |
| Front matter | — | — | ✅ отличаются только `title` («Targeting and Audiences») и `language: en` |
| Кириллица в EN | — | нет | ✅ |
| Числа/единицы/примеры (`DE`, `14d`, `7d`, `€50`, `90-day`, `25–34`, даты источников) | — | — | ✅ скопированы точно |

## Findings

- `[MINOR]` строка 127 — RU: «само по себе ещё не задаёт тактику повторного обращения» (автор намеренно избегает слова retargeting до его введения на строке 218). EN: «does not by itself define a retargeting tactic» — термин появляется за 90 строк до своей сноски `[^g-retargeting]`; якоря не затронуты, смысл сохранён, но принцип «сноска при первом упоминании» в EN формально нарушен переводом. Рекомендация: «a tactic for re-engaging them».
- `[MINOR]` строка 108 — RU: «исключив users с `unknown`» (значение в code-форматировании). EN: «by excluding the unknown population» — code-форматирование `unknown` потеряно; смысл сохранён.
- `[MINOR]` строка 149 — RU: «Контракт продукта должен явно определять composition и precedence». EN: «The contract must explicitly define…» — опущено «продукта». Пренебрежимо, но это единственное место, где слово выпало.
- `[MINOR]` строка 75 — RU: «Money flow при этом не превращается в новую pricing model. Targeting меняет…» EN: «Targeting does not change the pricing model that governs the money flow. It changes…» — перефразировано (объединены два предложения), смысл сохранён.

Проверено на отсутствие добавлений/смягчений: различия current vs legacy («На момент написания» → «At the time of writing», строка 240), universal vs product-specific («Это не универсальный default отрасли» → «This is not a universal industry default», 92), caveats (253, 273, 290) сохранены. Терминология консистентна: eligible set, suppression/exclusion, re-engagement, prospecting, provenance («Происхождение (provenance)» → «Provenance»), onboarding, addressable. Сравнение с `glossary.en.md` не требовалось — определения в главе inline-парафразы, а не цитаты статей.

## Вердикт

**PASS** — FAIL-находок нет; 4 MINOR не блокируют.

---

# Приложение. Сопоставление с `review-2026-10-09/ch06.md` §7 (после вердикта)

| IMPORTANT из предыдущего ревью | Статус в текущей версии |
|---|---|
| 1. Унифицировать retargeting-правило | ✅ Исправлено: `trial_started ≥ 7d ago AND no paid_subscription since trial_started` одинаково в строках 170, 218, 298 |
| 2. Добавить `first-party data vs first-party identity` | ✅ Исправлено: строка 177 + bullet 320 (= TOC 6.18) |
| 3. Addressability caveat + forward refs | ✅ Исправлено: строка 204 (главы 24, 40–42) (= TOC 6.19) |
| 4. Объяснить `match` и определить `addressable` при первом употреблении | ✅ Исправлено: строки 175 (hashed email / device ID / account ID ↔ identifiers платформы; onboarding) и 153 |
| 5. Структурный контракт (H1 источников, «С чем это часто путают», склейка абзацев 129–130) | ✅ Исправлено: `## Источники и дополнительное чтение` (341), «## С чем это часто путают» (314), абзацы 133/135 разделены в RU и EN |
| 6. Русифицировать шапки таблиц и бытовую латиницу | 🟡 Частично: шапки таблиц русифицированы («Семантика», «Измерение», «Входной признак», «Режим»); `product`/`contract`/`semantics` в основном переведены; `entity` (~25) и `boundary` (5) остались — предыдущее ревью само предлагало «entity оставить как термин», но §3 master-prompt называет оба слова нарушением. **Остаётся как IMPORTANT 1 текущего аудита.** |

NICE-TO-HAVE из §7: п. 7 (таблица first-party vs third-party) ✅, п. 8 (remarketing, DMP) ✅, п. 9 (`[^g-inventory]`, `[^g-reach]`) ✅, п. 10 (`g-targeting` расширен) ✅, п. 11 (UA reduction) ✅, п. 12 (prospecting/re-engagement/Demand Gen) ✅, п. 13 (разбить абзац Google/Meta; убрать «на 2 сентября 2026» из прозы) ✅ — но дата «с марта 2024 года» (строка 179; была и в версии HEAD, строка 174) предыдущим ревью не отмечалась и остаётся (IMPORTANT 3), п. 14 (learning phase в шаге 6) ✅, п. 15 (unknown, distinct reach) ✅, п. 16 (новые статьи глоссария) ✅ — `g-seed-audience`, `g-prospecting`, `g-addressable`, `g-observation-window` существуют и используются.

Находки, которых не было в предыдущем ревью: сноски `bid`/`auction`/`conversion rate`/`optimization event`/`measurement` (IMPORTANT 2) и дата в строке 179 (IMPORTANT 3; текст в этом месте существовал и до сегодняшних правок).

# Число слов

Чистая проза RU (без front matter, таблиц, code blocks, заголовков и раздела источников): **2 780**; с разделом источников — 2 985; только основной текст до служебных секций — 2 496.
