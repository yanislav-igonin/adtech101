# Повторный аудит главы 5 «Как устроена рекламная кампания» (2026-10-09)

Входы: `chapters/ru/05-campaign-structure.md`, `chapters/en/05-campaign-structure.md`, `plans/ru/05-campaign-structure.plan.md`, `master-prompt.md` §3, §7 (Stage B «Контракт оформления главы»), §10 (строка `#### 5.`), `glossary.md`, `agents/auditor.md`, `agents/translation-auditor.md`. Режим — только чтение. Предыдущие аудиты (`audits/ru/*.audit.md`, `review-2026-10-09/ch05.md`) до вынесения вердиктов не читались; сравнение с §7 предыдущего отчёта вынесено в отдельный раздел в конце.

Объём чистой прозы RU (без front matter, таблиц, code blocks, заголовков): **≈2 510 слов** без раздела источников; ≈2 770 слов, если считать список источников.

---

# РОЛЬ 1 — Coverage & Accuracy Auditor (RU)

# Резюме аудита

По содержанию глава сильная: все 14 requirements TOC раскрыты на нужной глубине, пометки ракурса для 5.5, 5.8 и 5.9 соблюдены (placement как buy-side поле конфигурации с явным разведением с publisher-side slot, targeting axis главы 6 и формата главы 8; targeting вводно с передачей главы 6; bid strategy как policy с передачей математики главе 7). Фактических ошибок, устаревших утверждений или vendor-specific поведения, выданного за универсальное, не найдено: Google-/Meta-примеры везде помечены как product-specific. Causal chain, state-vector модель lifecycle и сквозной subscription-app пример согласованы между схемами, таблицами и прозой.

Вердикт определяется контрактом оформления: три группы IMPORTANT-нарушений — пропущенные глоссарные сноски (`bid`, `auction`, `publisher`, `payer`, `audience exclusion`; сноска `billing basis` стоит не при первом упоминании), английские нетерминологические заголовок и шапки таблиц (`## Execution tree…`, `Setting`, `Unit/basis`, `Creative promise`) и бытовые английские слова в prose (`boundary` ×5 — слово из явного списка контракта, плюс `result`, `interval`, `label`, `limits` и др.). Блокеров нет.

# Блокеры

None.

# Важные проблемы

1. **Глоссарные термины без сноски / сноска не при первом упоминании.** Контракт: «каждый термин, имеющий статью в `glossary.md`, получает сноску… при первом упоминании».
   - `bid` (`{#g-bid}`) — 15 упоминаний, сноски нет; первое в прозе — строка 78: «ad set обычно хранит audience, placements[^g-placement], optimization, bid, budget и schedule». Главы 2–4 сноску `[^g-bid]` ставят.
   - `auction` (`{#g-auction}`) — 3 упоминания, сноски нет; первое — строка 193: «policy, которая переводит optimization goal и ограничения в auction bids».
   - `publisher` (`{#g-publisher}`) — строка 182: «на publisher side placement — конкретный slot», сноски нет (главы 1–4 и 6 её ставят).
   - `payer` (`{#g-payee-payer}`) — строка 40: «С ним связаны payer, billing profile…», сноски нет (глава 4 ставит).
   - `audience exclusion` (`{#g-audience-exclusion}`) — таблица, строка 186: «Geo `DE`, mobile devices, keyword category, audience exclusion», сноски нет (глава 6 ставит).
   - Упоминания `identity` (строки 84, 40 — «advertiser identity», «billing identity») не относятся к `{#g-identity-provider}` и нарушением не считаются. Сноска `[^g-billable-event]` (строка 176) стоит в абзаце с первым упоминанием термина `billable event`, то есть правило «при первом упоминании» соблюдено; но маркер прикреплён к фразе «Billing basis», а не к самому термину — см. OPTIONAL 1.

2. **Английские нетерминологические заголовок и шапки таблиц.** Контракт: «заголовки секций и шапки таблиц — по-русски; английский в них только как established term».
   - Строка 71: `## Execution tree: campaign, ad group/ad set, ad и creative` — «execution tree» не устоявшийся термин (аналог запрещённого контрактом примера `## Contract arithmetic`). Остальные заголовки (`### Bid strategy`, `### Objective и optimization event`, `## Lifecycle без ложной линейности`) проходят как термины.
   - Строка 217: шапка `| Setting | Возможная scope | Unit/basis | …` — `Setting`, `Unit/basis` бытовые слова.
   - Строка 277: шапка `| Creative promise | Destination | Наблюдаемый event | …` — `Creative promise` бытовая фраза (`Destination` — термин, допустим).

3. **Бытовые английские слова в prose.** Контракт (§3) прямо называет `boundary` нарушением; в главе оно встречается 5 раз вне кода: строка 64 («Product, access и billing boundary»), 75 («промежуточная scope boundary»), 252 («attribution configuration boundary»), 366 («product/access/billing boundary»), 376 («administrative boundary»). Того же рода: `result` (163: «наблюдаемый result, вероятность или value»), `interval` (213: «spend за весь interval»), `label` (128, 157, 176), `limits` (367: «Parent settings и limits меняют behavior children»), `rules`/`children`/`descendants`/`parent` (73, 84, 130, 367). Инженерный жаргон (`policy`, `payload`, `mapping`, `override`, `tenant`) и AdTech-термины не оспариваются.

# Необязательные улучшения

1. Терминологический дрейф с главой 4: глава 4 использует термин `pricing basis` (`{#g-pricing-basis}`), глава 5 — `billing basis` (строки 174, 176, 368, 386), причём маркер `[^g-billable-event]` на строке 176 прикреплён к фразе «Billing basis», а не к термину `billable event` в конце того же абзаца. Лучше либо единый термин со сноской на `g-pricing-basis`, либо перенести маркер на слово `billable event`.
2. Объём прозы ≈2 510 слов — на ~4 % выше ориентира 2 400; не «материальное» превышение, но при правках по пп. 1–3 текст не стоит наращивать.
3. «С чем это часто путают» (6) + «Что важно запомнить» (8) = 14 пунктов — верхняя граница контракта; пять пар дублируют друг друга по сути (account ≠ company ↔ п. 2; campaign ≠ папка ↔ п. 2; objective/event/billing ↔ п. 4; enabled/learning ↔ п. 8; tracking URL ≠ landing page ↔ п. 7). Формулировки комплементарны (отрицательная/положительная), но один-два пункта можно сократить. Раздел «Как читать любую campaign» также частично повторяет выводы.
4. Аббревиатуры `CTA` (строка 84) и `CRO` (строка 283) не расшифрованы; для технически сильного читателя без AdTech-фона `CRO` неочевидна.
5. Строка 82: «insertion order и line item (главы 11 и 16)» — в TOC главы 11 есть `order`/`line item`, в главе 16 insertion order не заявлен; ссылку на главу 16 стоит проверить при финальной сборке перекрёстных ссылок.

# Проверка корректности

Ошибок не найдено. Проверенные утверждения:

- Иерархия подана как scope/inheritance model, а не как единый industry schema; расположение budget/targeting/optimization везде привязано к Google-like/Meta-like модели (строки 75–80, 92–97).
- Google Ads parallel tracking описан верно и явно помечен как implementation Google, а не гарантия для любой platform/MMP (строка 273).
- Статусы Google (`Eligible` campaign + `Learning` bidding strategy) и Meta (active ad set в learning phase) соответствуют официальным моделям и помечены как product-specific (строка 320).
- Список significant edits Meta (targeting, creative, optimization event, состав ads, bid strategy, длительная пауза; budget — в зависимости от масштаба) соответствует текущей документации Meta и явно не переносится на Google/DSP/ad network (строка 342).
- Billing basis ≠ optimization event ≠ tracked event — continuity с главой 4 без переобъяснения экономики (строки 174–176).
- Placement размежёван по четырём ракурсам (publisher-side slot — главы 1 и 10; buy-side sites/apps — глава 6; Meta positions; формат — глава 8), что соответствует пометке TOC 5.5 (строка 182).
- Namespace IDs: campaign/ad IDs уникальны «как минимум» в контексте platform/account; click ID и event ID отнесены к главам 21–23 — соответствует TOC (22.6 click ID, 21.11 event ID).
- Daily budget как «жёсткий cap, average daily target или иная форма» — корректное обобщение без ложной универсальности (строка 212).
- Learning как под-состояние active delivery, обратимость pause, completion по end condition — верно (строки 297–311, 350).

# Проверка границ и плотности

- Повтора главы 4 нет: billing basis использован только как distinction, без путей денег и take rate.
- Targeting ограничен обзором (geo/device/context/audience/keyword/exclusions) с передачей главы 6; bid strategy — policy boundary с передачей главы 7; формат/compatibility — глава 8; attribution mechanics, postbacks, privacy — отложены (строка 254). Границы Planner Brief соблюдены.
- Нет лишней истории и vendor-minutiae: enum-значения приведены только как примеры.
- Проза ≈2 510 слов (ориентир 2 400) — см. OPTIONAL 2; закрывающие списки на верхней границе 14 пунктов — см. OPTIONAL 3.

# Проверка контракта оформления

| Пункт контракта | Результат |
|---|---|
| Ровно один H1 | ✅ строка 14 |
| Вводная секция `## Суть` | ✅ строка 16 |
| Хвост: `## С чем это часто путают`, `## Что важно запомнить`, `## Проверьте себя`, `## Источники и дополнительное чтение` — уровень `##`, порядок | ✅ строки 364, 373, 384, 391 |
| Заголовки секций по-русски / только established terms | ❌ `## Execution tree: …` (строка 71) — IMPORTANT 2 |
| Шапки таблиц по-русски / только termы | ❌ `Setting`, `Unit/basis` (217), `Creative promise` (277) — IMPORTANT 2 |
| Бытовые английские слова в prose | ❌ `boundary` ×5 и др. — IMPORTANT 3 |
| Каждая `[^g-id]` существует в `glossary.md` | ✅ 36/36 якорей разрешаются |
| Один термин — одна сноска | ✅ все 36 сносок по одному разу |
| Сноска при первом упоминании | ✅ все 36 сносок при первом упоминании термина (ранние вхождения `destination`, `creative`, `inventory`, `bid strategy` — только внутри code blocks); `[^g-billable-event]` стоит в абзаце первого упоминания `billable event` (176), хотя прикреплён к фразе «Billing basis» — OPTIONAL 1 |
| Каждый глоссарный термин имеет сноску | ❌ `bid`, `auction`, `publisher`, `payer`, `audience exclusion` — IMPORTANT 1 |
| Нет дат проверки / research-пометок в prose | ✅ даты `2026-09-07`/`2026-09-14` (строки 234–235) — учебные значения schedule в code block, не research-даты; «проверено»/«на дату» в prose нет |
| YAML front matter полный и согласован с TOC | ✅ `id: ch-05`, `toc_requirements` 5.1–5.14, `language: ru`, `prerequisites: [ch-01..ch-04]` |

# Coverage Table

| Requirement | Status | Evidence / Explanation |
|---|---|---|
| 5.1 advertiser account | ✅ COVERED | «Зачем кампании нужна иерархия»: account как tenant, пять границ (ownership/access, billing identity, currency/time zone, namespace, shared configuration), legal entity ≠ account, manager account как administrative layer, дерево и таблица «Объект / Что представляет / Чего нельзя заключить», сквозной EU account (строки 33–69) |
| 5.2 campaign | ✅ COVERED | «Execution tree»: верхнеуровневый delivery container для одного intent/flight, объединяет objective, limits, channel/type; pause/schedule родителя останавливает descendants; строка таблицы Campaign (73, 94, 130) |
| 5.3 ad group/ad set | ✅ COVERED | Промежуточная scope boundary; Google-like (related ads + keywords) vs Meta-like (audience, placements, optimization, bid, budget, schedule); явный запрет универсальных утверждений; IO/line item как аналог в DSP/ad server (75–82, 95) |
| 5.4 ad/creative | ✅ COVERED | Ad как исполняемая delivery-единица (parent, identity, creative, destination, tracking, status), creative как message + assets, inline vs reusable; схема creative/ad; JSON-дерево с `cr_video_a` в двух ads (84–130) |
| 5.5 placement (ракурс: поле конфигурации campaign) | ✅ COVERED | «Targeting и placement»: определение «в каком media environment и slot»; четыре ракурса термина с ссылками на главы 1/10, 6, 8; таблица осей; «API может хранить placements внутри `targeting`» (182–189) |
| 5.6 campaign objective | ✅ COVERED | «Objective и optimization event»: high-level intent/setup guidance, platform предлагает types/defaults, objective ≠ предсказываемое событие; volatility названий `App promotion`/`Sales` (157–161, таблица 170) |
| 5.7 optimization event | ✅ COVERED | Наблюдаемый result, вероятность/value которого увеличивает delivery system; conversion action, primary/secondary; trade-off install vs paid subscription (volume, delay, event source); таблица слоёв (163–176) |
| 5.8 targeting (вводно) | ✅ COVERED | Eligibility rules и inputs модели; обзор geo/device/context/audience/keyword/exclusions; передача источников данных, identity и privacy главе 6; таблица осей (180, 184–189) |
| 5.9 bid strategy (ракурс: policy) | ✅ COVERED | Policy, переводящая goal и ограничения в bids; четырёхчастная схема strategy / target-cap / actual bid / price-charge; `target CPA` ≠ bid ≠ billable amount; математика → глава 7 (191–204) |
| 5.10 budget | ✅ COVERED | Daily vs lifetime/campaign-total, scope campaign/shared/group, allocation; таблица «что ограничивает / чего не гарантирует»; `€700` на 7 дней ≠ `€100/day`, ≠ `€350` на группу (206–224) |
| 5.11 schedule | ✅ COVERED | Start/end, account time zone, dayparting; пример `Europe/Berlin`; `pending` до start, `ended/completed` после end при недотраченном бюджете; взаимодействие budget/schedule/status (226–238) |
| 5.12 tracking settings | ✅ COVERED | Инвентарь: IDs, URL parameters/macros/template/suffix, pixel/SDK/S2S/MMP как event source, conversion actions, attribution boundary; две схемы путей; учебный URL; parallel tracking как Google-пример; MMP mapping caveat (246–285) |
| 5.13 landing page | ✅ COVERED | Landing page/destination/final URL как первая поверхность (web, store listing, deep link), часть user path, не tracking record; таблица creative promise → destination → event → проверка согласованности; CRO вне scope (244, 277–283) |
| 5.14 lifecycle: draft → learning → active → paused → completed | ✅ COVERED | Мнемоника дана и сразу аннотирована по пяти состояниям; state graph; таблица четырёх осей (configured/effective/review/learning); Google и Meta примеры; change scenario с возвратом в learning при `active`; pause не обязателен перед completion (287–350) |

# Вердикт

**REVISION REQUIRED** — блокеров и проблем покрытия нет, но три группы нарушений контракта оформления (IMPORTANT 1–3) блокируют PASS по правилу Stage C.

---

## Сравнение с предыдущим аудитом (`review-2026-10-09/ch05.md`, §7) — прочитано после вынесения вердикта

Все пять IMPORTANT предыдущего отчёта исправлены:

| № | Рекомендация §7 | Статус в текущем тексте |
|---|---|---|
| 1 | Служебные секции `###` → `##` | ✅ строки 352, 364, 373, 384 — `##` |
| 2 | `# Sources and Further Reading` → `## Источники и дополнительное чтение` | ✅ строка 391 |
| 3 | Развести `optimization event` и `optimization target` в глоссарии, переключить сноску | ✅ `{#g-optimization-event}` существует, сноска `[^g-optimization-event]` на строке 163; `g-optimization-target` содержит оговорку «не путать с параметром стратегии» |
| 4 | Строка о DSP/ad-server naming (insertion order / line item) | ✅ строка 82 |
| 5 | Нейтрализовать generic «ad set» | ✅ «группе (ad group/ad set)» (215), «в Meta-like setup — два ad sets» (224), «Strategy/ad set» (318) |

NICE-TO-HAVE: выполнены 6 (предложение про deduplication удалено), 7 (сноски `g-cpc`, `g-cpa`, `g-inventory`), 8 («длительную паузу ad set»), 9 (пояснение `review`), 11 (мост о многозначности `placement`), 13 («CPM или CPC»), 14 (`## Суть`), 15 («Юридическое лицо»). Частично — 12: `Conversion action` в глоссарии есть, `Configured status / effective status` и `Significant edit` статьями не добавлены (глава определяет их inline, нарушением контракта это не является). Не выполнено — 10: дублирование «С чем это часто путают» / «Что важно запомнить» сохраняется (см. OPTIONAL 3 выше).

Новые IMPORTANT текущего аудита (сноски `bid`/`auction`/`publisher`/`payer`/`audience exclusion`, английские заголовок и шапки таблиц, бытовые английские слова) в предыдущем отчёте не поднимались — они следуют из добавленной сегодня секции «Formatting and Language Contract».

---

# РОЛЬ 2 — Translation Auditor (RU ↔ EN)

SOURCE_FILE: `chapters/ru/05-campaign-structure.md`; TRANSLATION_FILE: `chapters/en/05-campaign-structure.md`.

## Проверки

- **Полнота и структурный паритет.** Заголовки 17/17 с идентичными уровнями и порядком; code blocks 15/15 с теми же языками (`text`/`json`), в 7 текстовых блоках переведены только слова, числа и структура строк сохранены; строки таблиц 40/40; элементы списков 56/56; абзацы 54/54; ссылки 12/12 с идентичными URL; inline-code спаны 43/43 с идентичным набором; выделения `**…**` 46/46.
- **Front matter.** Отличия только `title: "How an Ad Campaign Is Structured"` и `language: en`; `id`, `toc_requirements`, `prerequisites`, `status`, `slug` идентичны.
- **Якоря.** 36 сносок `[^g-…]` — тот же набор, каждая ровно один раз в обоих файлах, без переименований и добавлений.
- **Числа и примеры.** `€700`, `€350`, `€100/day`, даты `2026-09-07`/`2026-09-14`, `Europe/Berlin`, все ID (`cmp_subscriptions_42`, `ad_7`, `cr_video_a`…), URL `https://example.com/app?campaign_id=…` — побайтно совпадают.
- **Русский текст в EN.** Кириллицы в теле нет.
- **Служебные секции.** `## The Core Idea`, `## Common Confusions`, `## What to Remember`, `## Check Yourself`, `## Sources and Further Reading` — названия и уровень корректны.
- **Терминология.** Термины, оставленные в RU на английском, сохранены; маппинг консистентен: ad set/ad group, flight, destination/landing page/final URL, optimization event/performance goal, learning phase, significant edit, material change — по одному английскому эквиваленту на понятие по всему файлу. Различения current/legacy и universal/platform-specific сохранены (parallel tracking — «Google's implementation»; Meta significant edits — «cannot be transferred to Google Ads, a DSP, or an ad network»).

## Findings

```text
[MINOR] строка 73 («согласованного flight — периода размещения с датами начала и конца») — переведено как "a coherent flight — a placement period with a start and an end date"; слово "placement" коллидирует с термином placement, определяемым ниже в той же главе; точнее "a run period" / "a delivery window".
[MINOR] строка 94 (таблица, «Objective и, при выбранной модели, campaign-level budget») — "Objective and, for the chosen model, a campaign-level budget" читается неестественно; смысл RU — «когда выбрана такая модель» ("when that model is selected").
[MINOR] строка 311 («learning может быть под-состоянием active delivery, а не предшествующим запретом показов») — EN: "rather than a stage preceding the permission to show"; RU говорит, что learning не является предшествующим *запретом* показов, EN — что это не этап *перед разрешением*; смысл («learning не блокирует delivery») сохранён, нюанс сдвинут.
```

## Вердикт

**PASS** — FAIL-находок нет; три MINOR не блокируют.
