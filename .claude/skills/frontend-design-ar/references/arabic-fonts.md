# Arabic typefaces

All of these are free on Google Fonts. Load only the weights you use: `https://fonts.googleapis.com/css2?family=Readex+Pro:wght@400;600&display=swap`.

Choose from the subject, not the list order. Faces in the **overused** group are fine, but only when you can say why they fit this brief better than the alternatives.

## Sans, for UI and body text

| Face | Personality | Weights | Latin pairing |
|---|---|---|---|
| **IBM Plex Sans Arabic** | Engineered, neutral, corporate-technical. Good for dashboards and developer tools. | 100–700 | IBM Plex Sans / Plex Mono (the same family, so it matches exactly) |
| **Readex Pro** | Geometric and slightly rounded, friendly-tech. Very legible at small sizes. | 160–700 variable | Built in (it ships its own Latin) |
| **Alexandria** | Geometric, confident, contemporary. Strong in big headlines. | 100–900 | Built in |
| **Noto Sans Arabic** | Quiet and neutral, with very wide coverage. The safe workhorse when another face should be the star. | 100–900 | Noto Sans, or any neutral grotesque |
| **Mada** | Light, open and airy. Suits calm consumer apps. | 200–900 | Built in |
| **Changa** | Condensed with Kufi structure. Sporty and energetic: gaming, sports, events. | 200–800 | Built in |
| **El Messiri** | Elegant, with gently calligraphic terminals. Hospitality, culture, premium. | 400–700 | Built in |

**Overused** (the "Inter" of Arabic): **Cairo**, **Tajawal**, **Almarai**. They are competent and familiar, and they make the page look like every other Arabic site.

## Naskh, for editorial and long reading

| Face | Personality | Weights | Notes |
|---|---|---|---|
| **Noto Naskh Arabic** | Traditional and bookish, with a calm rhythm | 400–700 | Comfortable for long reading |
| **Markazi Text** | Contemporary Naskh with literary warmth | 400–700 | Ships a Latin serif, which suits bilingual editorial work |
| **Amiri** | Classical, in the Bulaq press tradition: formal and literary | 400, 700 | Books, poetry, religious or heritage content |
| **Scheherazade New** | Traditional, with full diacritic support | 400–700 | Use it when text carries heavy tashkeel |

## Kufi and display, for headlines, logos and posters only

| Face | Personality | Weights |
|---|---|---|
| **Noto Kufi Arabic** | Structured, architectural Kufi. Also holds up at UI sizes. | 100–900 |
| **Reem Kufi** | Geometric Kufi, modern-heritage | 400–700 |
| **Kufam** | Bold Kufi with a matching Latin | 400–900 |
| **Aref Ruqaa** | Ruqaa calligraphy: handwritten, warm, traditional | 400, 700 |
| **Lalezar** | Heavy, punchy and playful. Posters, food, kids. | 400 |
| **Lemonada** / **Marhey** | Rounded and bubbly, for playful consumer brands | 300–700 |
| **Rakkas** / **Jomhuria** | Very heavy display, for loud campaign headlines | 400 |
| **Blaka** | Sharp, blackletter-like Arabic. Unusual and edgy. | 400 |

Never set body text in a display face. A display face is for one memorable element on the page.

## Pairing patterns

- **One family that ships both scripts** (Readex Pro, Alexandria, IBM Plex): the safest choice for bilingual UI, because both scripts share metrics and feel.
- **Kufi display with a Sans body**: structured headlines over calm text. For example, Noto Kufi Arabic + IBM Plex Sans Arabic.
- **Naskh display with a Sans body**: literary warmth over a modern UI. For example, Markazi Text headlines + Readex Pro body.
- **Calligraphic accent**: one Aref Ruqaa or Lalezar moment, such as a logo or hero line, with everything else in a quiet sans.

## CSS starting point for bilingual work

```css
:root {
  --font-ar: "Readex Pro", "Noto Sans Arabic", system-ui, sans-serif;
  --font-en: "Readex Pro", system-ui, sans-serif;
}
:lang(ar) { font-family: var(--font-ar); line-height: 1.8; letter-spacing: 0; }
:lang(en) { font-family: var(--font-en); line-height: 1.5; }
/* Tracking is only ever applied to Latin text */
:lang(en) .label { letter-spacing: 0.02em; }
```
