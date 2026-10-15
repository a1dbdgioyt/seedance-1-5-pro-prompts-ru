# Seedance 1.5 Pro Prompts — 8 Tested Recipes With Outputs

<!-- conv-kit:v1 -->

<p align="center">
  <img src="assets/badges/price.svg" alt="observed unit price"> <img src="assets/badges/billing.svg" alt="billing model"> <img src="assets/badges/compat.svg" alt="OpenAI-compatible endpoint">
</p>

<p align="center">
  <img src="assets/01-product-ad-ceramic-mug-thumb.jpg" width="820" alt="Sample video frame generated through APIMart">
</p>

> **from $0.0104 per second** on the APIMart route (billed by resolution tier) — одна OpenAI-совместимая конечная точка на `https://api.apimart.ai/v1`, ежемесячный тариф не нужен. *(данные на 2026-10-12)*

**[Get an API key](https://go.apimart.ai/k-ba9124)** · **[Live pricing](https://go.apimart.ai/k-ac986c)** · **[Model page](https://go.apimart.ai/k-2cca2d)** · [⚡ 60-second quickstart](#quickstart)

**Почему команды используют Seedance 1.5 Pro (`seedance-1.5-pro`) через APIMart**

- **Один ключ — весь каталог.** Тот же base URL `https://api.apimart.ai/v1` и тот же заголовок `Authorization` дают доступ к Seedance 1.5 Pro (`seedance-1.5-pro`) и ещё 300+ моделям для изображений, видео и языка — менять нужно поле `model`, а не клиент.
- **Минимум $1, оплата по факту.** Ни подписки, ни предоплаченного тарифа, который нужно заранее рассчитать: пополняйте от $1 и расходуйте на вызовы.
- **Сумма списания возвращается в ответе.** Каждая завершённая задача сообщает списанную сумму (`cost` / `credits_cost`); задача со статусом `failed` возвращается на баланс.
- **Асинхронность по умолчанию.** Отправьте задачу, получите `task_id`, опрашивайте `GET /v1/tasks/{id}` — пакетная обработка и повторы это обычная работа с очередью, а не отдельная интеграция.

<!-- /conv-kit:v1 -->

**Также известен как:** Сиденс · Сиданс · Сидэнс

Four **Seedance 1.5 Pro prompts** listed with an example render, the duration, and what the call costs on this route. Copy a recipe, keep the structure, swap the subject.

- Model: `seedance-1.5-pro`
- Recipes: **4** (machine-readable in [`data/prompts.json`](data/prompts.json), table in [`PROMPTS.md`](PROMPTS.md))
- Effective price used below: **$0.0104 per second** — estimated cost of the whole set: **$0.0416**

## What separates a usable recipe from a wasted call

Three rules held up across every render in this set:

1. **Name the material, not the adjective.** "Frosted glass", "matte ceramic", "layered paper" steer rendering far more
   than "beautiful" or "high quality".
2. **Set the light explicitly.** "Single softbox from the left", "golden hour backlight", "focus-stacked studio light"
   remove the guesswork the model would otherwise do for you.
3. **Pin the framing.** Ratio plus lens language (`85mm`, `24mm`, `macro`, overhead flat lay) decides whether the output
   drops into a layout unchanged.

## Prompt structure cheat-sheet

| Slot | What to write | Example |
| --- | --- | --- |
| Subject | one concrete object or person, with material | *frosted glass perfume bottle* |
| Light | direction + quality | *single softbox from the left* |
| Framing | ratio + lens or distance | *3:4, medium format look* |
| Setting | surface, backdrop, environment | *wet black stone slab* |
| Finish | render or film character | *commercial product photography* |

## The gallery

Each row is one recipe: example render, category, duration, cost on this route and the exact prompt.

| Output | Recipe | Duration | Cost | Prompt |
| --- | --- | --- | --- | --- |
| <img src="assets/01-product-ad-ceramic-mug-thumb.jpg" width="220" alt="Sample video frame generated through APIMart"> | Product ad | 5s | $0.0104 | `Slow 180° orbit around a matte ceramic mug on a dark stone plinth, steam rising, soft key light from camera left, shallow depth of field, product commercial` |
| <img src="assets/02-cinematic-rainy-street-thumb.jpg" width="220" alt="Sample video frame generated through APIMart"> | Cinematic | 5s | $0.0104 | `Rain soaked street at night, camera pushes in slowly past neon reflections, a lone figure with an umbrella walks away from camera, 35mm anamorphic, film grain` |
| <img src="assets/03-food-ad-steam-thumb.jpg" width="220" alt="Sample video frame generated through APIMart"> | Food commercial | 5s | $0.0104 | `Overhead view tilting down to 45° onto a steaming bowl of ramen, chopsticks lift the noodles, warm practical light, macro detail, appetising commercial grade` |
| <img src="assets/04-architecture-flythrough-thumb.jpg" width="220" alt="Sample video frame generated through APIMart"> | Architecture | 5s | $0.0104 | `Slow aerial flythrough of a concrete villa at dusk, camera pushes across the infinity pool toward warm interior light, 24mm, ultra sharp` |

## Run a recipe yourself

```bash
export APIMART_API_KEY=...
python examples/run_recipes.py --dry-run                 # list the recipes, no network
python examples/run_recipes.py --limit 2                 # generate two of them
```

```bash
curl --request POST --url https://api.apimart.ai/v1/videos/generations \
  --header "Authorization: Bearer $APIMART_API_KEY" --header 'Content-Type: application/json' \
  -d '{"model":"seedance-1.5-pro","prompt":"<paste a prompt>","duration":5,"resolution":"720P","size":"16:9"}'
```

Result links expire 72 hours after completion, so store the outputs; the completed task carries `cost` for reconciliation.

## FAQ

**Are these prompts free to reuse?**

Yes — the prompt text in this repository is MIT licensed. The generated images and any third-party marks they contain remain your responsibility, and you should check the model vendor's terms before publishing commercial work.

**Why do the recipes use different aspect ratios?**

Because ratio is a layout decision, not a style one: 1:1 for catalogue and icons, 16:9 for hero and video thumbnails, 3:4 or 2:3 for portraits and print. Pinning it up front avoids cropping later.

**How much does one recipe cost to run?**

**from $0.0104 per second** on the APIMart route (billed by resolution tier). Every completed task reports the exact amount in its `cost` field; a failed task is refunded.

**Can I use a recipe as a template for another subject?**

That is the point. Keep the structure (subject + light + framing + setting + finish) and replace the subject; changing everything at once makes it impossible to tell which phrase moved the output.

## Attributed links (how this repository is measured)

| Purpose | Attributed link | Target |
| --- | --- | --- |
| Model page | <https://go.apimart.ai/k-2cca2d> | `apimart.ai/ru/model/doubao-seedance-1-5-pro` |
| Live pricing | <https://go.apimart.ai/k-ac986c> | `apimart.ai/ru/pricing` |
| Get an API key | <https://go.apimart.ai/k-ba9124> | `apimart.ai/ru/keys` |

Outbound APIMart links are minted through the promo link API; hand-made tracking parameters are rejected by
`tools/check_links.py` in CI.

## Disclosure

Seedance 1.5 Pro is a third-party model served through APIMart. This repository publishes prompts, example renders and
cost logic; it does not claim official status for any vendor, and model names and documentation belong to their owners.

## Repository map

```text
README.md              gallery, prompt structure and FAQ
PROMPTS.md             every recipe in one table
data/prompts.json      machine-readable recipes with per-unit cost
examples/run_recipes.py  batch runner (dry-run safe for CI)
tools/check_links.py   attribution guard
assets/                example renders via the APIMart image API (JPEG)
```

## License

MIT — see [LICENSE](LICENSE).
