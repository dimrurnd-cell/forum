# Баннер форума

Три размера одного макета, все в фирменной палитре лендинга.

| Артборд | Размер | Для чего |
|---|---|---|
| `Main.dc.html`  | 1200 × 630  | соцсети, превью ссылки в мессенджерах, шапка письма |
| `Wide.dc.html`  | 1920 × 480  | шапка сайта, экран в холле |
| `Strip.dc.html` | 1200 × 300  | узкая полоса, врезка в письмо или статью |

Канвас со всеми тремя: https://claude.ai/code/artifact/7a020096-6187-40de-ad82-bb12a8ded60e
PNG выгружается из панели Export у каждого артборда.

## Как устроено

- `*.dc.html` — исходники артбордов. Правите их и пересобираете канвас.
- `canvas.json` — раскладка артбордов на холсте.
- `*.jpg` — фотографии спикеров, 420×420, пережаты для баннера.
- `banner-foruma-prodazh-nedvizhimosti.html` — собранный канвас (2,8 МБ).
  Файл собирается из перечисленного выше, в репозитории не хранится.

Шрифт Jost вшит в каждый артборд как `@font-face` с base64. Без этого
экспорт в PNG подставил бы запасную гарнитуру: шрифты с Google Fonts
в выгрузку не попадают.

Пересобрать после правок:

```
cd banner
node "<каталог скилла design>/seed-canvas.mjs" \
  --template "<тот же каталог>/payload.template.html" \
  --out banner-foruma-prodazh-nedvizhimosti.html \
  --title "Баннер форума продаж недвижимости" \
  --artboard Main.dc.html --artboard Wide.dc.html --artboard Strip.dc.html \
  --image gelevey.jpg --image ulickaya.jpg --image arharova.jpg --image shabarov.jpg \
  --image klimenko.jpg --image delibaltidis.jpg --image guseva.jpg \
  --canvas canvas.json
```
