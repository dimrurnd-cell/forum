# Баннер форума

Пять размеров одного макета, все в фирменной палитре лендинга.

| Артборд | Размер | Для чего |
|---|---|---|
| `Main.dc.html`  | 1200 × 630  | соцсети, превью ссылки в мессенджерах, шапка письма |
| `Wide.dc.html`  | 1920 × 480  | шапка сайта, экран в холле |
| `Strip.dc.html` | 1200 × 300  | узкая полоса, врезка в письмо или статью |
| `Square.dc.html` | 330 × 330  | квадратная врезка в сайдбар |
| `Post.dc.html`  | 1080 × 1350 | вертикальный пост: Instagram, VK, Telegram |

Канвас со всеми пятью: https://claude.ai/code/artifact/7a020096-6187-40de-ad82-bb12a8ded60e
PNG выгружается из панели Export у каждого артборда.

## Как устроено

- `*.dc.html` — исходники артбордов. Правите их и пересобираете канвас.
- `canvas.json` — раскладка артбордов на холсте.
- `*.jpg` — фотографии спикеров, 420×420, пережаты для баннера.
- `banner-foruma-prodazh-nedvizhimosti.html` — собранный канвас (2,9 МБ).
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
  --artboard Square.dc.html --artboard Post.dc.html \
  --image gelevey.jpg --image ulickaya.jpg --image arharova.jpg --image shabarov.jpg \
  --image klimenko.jpg --image delibaltidis.jpg --image guseva.jpg \
  --canvas canvas.json
```

## Пост 1080 × 1350

Формат 4:5 — самый высокий, который соцсети показывают в ленте целиком.
Текст занимает верхнюю половину, фасад со спикерами — нижнюю: в ленте
превью обрезается снизу, и заголовок с датой остаются видны всегда.

Текст под пост лежит в `post-text.md` рядом — с вариантом для Telegram
и коротким вариантом для сторис.
