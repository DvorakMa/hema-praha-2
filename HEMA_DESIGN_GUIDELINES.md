# Design Guidelines — HEMA Praha (hema-praha.cz)

> Extrahovány přímou analýzou HTML/CSS kódu stránky postavené v Next.js + Tailwind CSS.

---

## 1. FONTY

### Primární rodina fontů

Stránka používá **dvě řezy** fontu Proxima Nova (self-hosted jako .woff2/.woff):

---

### Font 1: `Proxima Nova` — tělo textu, navigace, UI
```css
font-family: "Proxima Nova", -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto,
             Helvetica, Arial, sans-serif, "Apple Color Emoji", "Segoe UI Emoji",
             "Segoe UI Symbol", ui-sans-serif, system-ui, "Helvetica Neue",
             "Noto Sans", "Noto Color Emoji";
```

**Dostupné váhy:**
| Váha | Název souboru |
|---|---|
| 100 | ProximaNovaT-Thin |
| 300 | ProximaNova-Light |
| 400 | ProximaNova-Regular ✓ (výchozí) |
| 600 | ProximaNova-Semibold |
| 700 | ProximaNova-Bold |
| 800 | ProximaNova-Extrabld |
| 900 | ProximaNova-Black |

*Všechny váhy mají i italic variantu.*

**Použití:** `body`, `nav`, obecný UI text — font-size 16px, line-height 24px (1.5)

---

### Font 2: `Proxima Nova Extra Condensed` — headings, navigační linky, tlačítka
```css
font-family: "Proxima Nova Extra Condensed", -apple-system, ...
```

**Dostupné váhy:** 100, 300, 400, 600, 700, 800, 900 (+ italic varianty)

**Použití:** `h1`, `h2`, `h3`, `a` (navigace), tlačítka — kondenzovaný řez pro velké display texty

---

### Font 3: `Inter` — záložní / sekundární
```css
font-family: Inter, sans-serif;
```
Načtený přes self-hosting (woff2/woff), váhy 100–900 + italic. Slouží jako záložní systémový font.

---

### Typografická hierarchie

| Element | Font | Velikost | Váha | Line-height | Transform | Barva |
|---|---|---|---|---|---|---|
| `h1` | Proxima Nova Extra Condensed | `72px` | 700 | 72px (1.0) | UPPERCASE | `#ffffff` |
| `h2` | Proxima Nova Extra Condensed | `36px` | 400 | 40px (1.11) | UPPERCASE | `#ffffff` |
| `h3` | Proxima Nova Extra Condensed | `30px` | 400 | 36px (1.2) | UPPERCASE | `#ffffff` |
| `p` (hero) | Proxima Nova Extra Condensed | `30px` | 400 | 36px | none | `#ffffff` |
| `body` | Proxima Nova | `16px` | 400 | 24px (1.5) | none | `#ffffff` |
| `a` (nav) | Proxima Nova Extra Condensed | `24px` | 400 | 32px | UPPERCASE | `#ffffff` |
| Button | Proxima Nova Extra Condensed | `30px` | 400 | — | UPPERCASE | `#ffffff` |
| Button large | Proxima Nova Extra Condensed | `36px` | 400 | — | UPPERCASE | `#ffffff` |

**Klíčové pozorování:**
- Condensed řez se používá výhradně pro display/heading úrovně
- Vše nadpisové je UPPERCASE
- Žádný letter-spacing (na rozdíl od TwistCafe) — condensed font nepotřebuje tracking
- Váha heading fontů je **nižší** (400–700), kondenzovaný tvar dodává vizuální sílu sám o sobě

---

## 2. BAREVNÁ PALETA

### Pojmenované barvy (Tailwind config)

| Název | HEX | RGB | Použití |
|---|---|---|---|
| `hema-praha-blue-charcoal` | `#050a20` | rgb(5, 10, 32) | Hlavní pozadí stránky (body bg) |
| `hema-praha-blue` | `#274caa` | rgb(39, 76, 170) | Primární modrá, tlačítka (světlý střed) |
| — | `#142d70` | rgb(20, 45, 112) | Modrá (tmavý okraj gradientu tlačítek) |
| — | `#142756` | rgb(20, 39, 86) | Tmavě námořní (sekční pozadí) |
| — | `#0b112d` | rgb(11, 17, 45) | Přechodová tmavá (gallery gradient) |
| — | `#1d2747` | `theme-color` meta | Střední tmavá modrá |
| — | `#18357e` | `msapplication-TileColor` | Dlaždice modrá |

### Pomocné Tailwind barvy (použité v UI)
| Tailwind třída | Barva | HEX |
|---|---|---|
| `text-blue-400` / `bg-blue-400` | Světle modrá | `#60a5fa` / `#479aff` |
| `bg-red-400` | Červená (badge/alert) | `#f87171` |
| `text-red-600` | Tmavá červená | `#dc2626` |
| `text-gray-300` / `text-gray-400` | Šedé texty | `#d1d5db` / `#9ca3af` |
| `text-gray-200` | Světle šedá | `#e5e7eb` |
| `text-gray-500` | Středně šedá | `#6b7281` |
| `text-white` | Bílá | `#ffffff` |

### Gradienty (klíčové sekční pozadí)

#### Tlačítka — radial gradient (modrý)
```css
background: radial-gradient(
  87.77% 96.22% at 22.79% 4.91%,
  rgb(39, 76, 170) 0px,      /* světlá modrá — světelný bod vlevo nahoře */
  rgb(20, 45, 112) 100%      /* tmavá námořní modrá — okraj */
);
```

#### Sekce — About / HEMA Fencer / Gallery
```css
/* About section */
background: radial-gradient(47.2% 47.2% at 31.17% 50%,
  rgb(20, 39, 86) 0px,
  rgb(5, 10, 32) 100%
);

/* Trainers section */
background: radial-gradient(45.26% 43.71% at 50% 43.71%,
  rgb(20, 39, 86) 0px,
  rgb(5, 10, 32) 100%
);

/* Weapons section */
background: radial-gradient(54.74% 54.74% at 50% 45.26%,
  rgb(20, 39, 86) 0px,
  rgb(5, 10, 32) 100%
);

/* Gallery section */
background: linear-gradient(
  rgb(5, 10, 32),     /* charcoal */
  rgb(11, 17, 45)     /* slightly lighter navy */
);
```

#### Icon pozadí
```css
background: radial-gradient(
  87.77% 96.22% at 22.79% 4.91%,
  rgb(39, 76, 170) 0px,
  rgb(20, 45, 112) 100%
);
```

### Barvy – souhrn

```
Velmi tmavá (body bg):      #050a20  ←── dominantní pozadí
Tmavá námořní:              #0b112d
Střední námořní:            #142756
Tmavá modrá:                #142d70
Primární modrá:             #274caa  ←── CTA, accenty
Světlá modrá (UI):          #60a5fa / #479aff

Bílá (text):                #ffffff
Světle šedá:                #e5e7eb
Šedá (muted text):          #9ca3af / #d1d5db

Červená (alert/badge):      #f87171 / #dc2626
```

---

## 3. TLAČÍTKA

### Primární tlačítko (CTA)
```css
.btn-primary {
  background: radial-gradient(87.77% 96.22% at 22.79% 4.91%,
    rgb(39, 76, 170) 0px,
    rgb(20, 45, 112) 100%
  );
  color: #ffffff;
  border-radius: 9999px;           /* pill tvar */
  padding: 24px 20px;              /* large */
  font-family: "Proxima Nova Extra Condensed", sans-serif;
  font-size: 30px;
  font-weight: 400;
  text-transform: uppercase;
  border: none;
  cursor: pointer;
}

/* Střední varianta */
.btn-primary-md {
  padding: 16px 24px;
  font-size: 30px;
}

/* Malá varianta */
.btn-primary-sm {
  padding: 12px 20px;
  font-size: 20px;
}

/* XL varianta (hero/pricing) */
.btn-primary-xl {
  padding: 24px 32px;
  font-size: 36px;
}
```

**Tvar:** Vždy `border-radius: 9999px` (plný pill/capsule)

---

## 4. VIZUÁLNÍ STYL

### Celkový charakter
- **Tmavý, intenzivní** — téměř celá stránka na `#050a20` (téměř černomodrá)
- **Militantně sportovní** — dramatické typografické pózy, condensed font, shadowy imagery
- **Bez ostrých hran** — tlačítka jsou pill, karty mají mírný border-radius (4px u event cells)
- **Vrstvení pozadí** — sekce přecházejí přes radial gradienty, ne plochými barvami

### Efekty
```css
/* Text shadow pro nadpisy na obrázcích */
text-shadow:
  rgb(0, 0, 0) 0px 2px,
  rgb(0, 0, 0) 0px 2px 4px,
  rgb(0, 0, 0) 0px 4px 8px,
  rgb(0, 0, 0) 0px 8px 12px,
  rgb(0, 0, 0) 0px 12px 24px;

/* Víceúrovňový box-shadow pro prvky */
box-shadow:
  rgba(0,0,0,0.2) 0px 2px 2px,
  rgba(0,0,0,0.2) 0px 4px 4px,
  rgba(0,0,0,0.2) 0px 8px 8px,
  rgba(0,0,0,0.2) 0px 16px 16px,
  rgba(0,0,0,0.2) 0px 24px 24px,
  rgba(0,0,0,0.2) 0px 48px 48px;

/* Hover na schedule event buňkách */
.event-cell { transition: transform 0.2s ease-in-out; }
.event-cell:hover { transform: scale(1.02); z-index: 20; }

/* Border oddělovač */
border-bottom: 1px solid rgba(255, 255, 255, 0.2);  /* solid */
border-bottom: 1px dashed rgba(255, 255, 255, 0.2); /* dashed */
border-right: 1px solid rgba(255, 255, 255, 0.2);
```

### Stránka je postavena v Next.js + Tailwind CSS
- Vlastní Tailwind konfigurace s `hema-praha-blue` a `hema-praha-blue-charcoal`
- Self-hosted fonty přes `@font-face` v CSS bundlu
- Mapbox pro mapu (custom dark/navy styl)

---

## 5. INSTRUKTOŘI

### Přehled
| Jméno | Soubor |
|---|---|
| MUDr. Matvey Sakharov | `sakharov-2.0.png` |
| Alexander Stankevich | `stankevich-3.0.png` |
| Adam Prochaska | `adam.png` |
| Pavel Grussmann | `pavel.png` |
| Vladislav Tovt | `vlad.png` |

Obrázky jsou uloženy ve složce `hema-instructors/` v tomto projektu.
Rozměr: 2600 × 2539 px, formát PNG (průhledné pozadí), `object-contain`.
