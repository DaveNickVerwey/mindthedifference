# Fonts installeren

De site verwacht 5 font-bestanden in een `/fonts/` map naast `index.html`:

```
/mindthedifference
  index.html
  /fonts
    akzidenz-grotesk-regular.woff2
    akzidenz-grotesk-bold.woff2
    futura-book.woff2
    futura-medium.woff2
    futura-bold.woff2
```

## Weights & gebruik

| Bestand | Font | Weight | Waar gebruikt |
|---|---|---|---|
| `akzidenz-grotesk-bold.woff2` | Akzidenz-Grotesk | 700 | Alle titels (h1, h2, h3), logo, hoofdlettering |
| `akzidenz-grotesk-regular.woff2` | Akzidenz-Grotesk | 400 | Reserve — nu nergens actief gebruikt, maar handig om erin te hebben |
| `futura-book.woff2` | Futura | 400 | Body tekst, alinea's, hulpteksten |
| `futura-medium.woff2` | Futura | 500 | Subtitels, iets sterker geaccentueerde tekst |
| `futura-bold.woff2` | Futura | 700 | Nadruk (`<strong>`), knoppen, labels, badges |

## Zijn je bestanden geen .woff2?

Als je `.otf`, `.ttf`, of `.woff` hebt, converteer ze eerst — dat scheelt veel laadtijd.
Gratis tool: [transfonter.org](https://transfonter.org) → upload je bestanden → kies WOFF2 → download.

## Fallback

Als de fonts niet laden (bijv. tijdens de eerste render, of bij offline), valt de site terug op:
- **Titels:** Helvetica Neue → Arial (dichtst in de buurt van Akzidenz)
- **Body:** Trebuchet MS → system-ui (dichtst in de buurt van Futura)

Alles blijft leesbaar, alleen zonder de exacte huisstijl-look.
