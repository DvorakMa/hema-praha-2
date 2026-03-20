# Design Guidelines — TwistCafe Franchise (franchise.twistcafe.com/en/)

> Extrahovány přímou analýzou HTML/CSS kódu stránky postavené ve Frameru.

---

## 1. BAREVNÁ PALETA

### Primární barvy
| Název | HEX | RGB | Použití |
|---|---|---|---|
| Brand Black | `#120700` | rgb(18, 7, 0) | Pozadí celé stránky, nav, footer |
| Brand Yellow | `#ffe654` | rgb(255, 230, 84) | Hlavní žlutá značky |
| CTA Yellow | `#ffdb09` | rgb(255, 219, 9) | Barva tlačítek Primary |
| White | `#ffffff` | rgb(255, 255, 255) | Primární text na tmavém pozadí |
| Off-White | `#fafafa` | rgb(250, 250, 250) | Text sekundárních tlačítek |

### Škála žluté (10 stupňů od tmavší po světlejší)
```
#f5c400 → #ffdb09 → #ffdf22 → #ffe23a → #ffe654 → #ffe96b → #ffed84 → #fff19c → #fff4b5 → #fff8cd → #fffbe5
```

### Škála hnědošedé (neutrály)
```
#0a0908 → #120700 → #383330 → #4f4844 → #665d58 → #7c726c → #928881 → #a69e98 → #bab3af → #cec9c6 → #e2dfdd → #f6f5f4
```

### Doplňkové barvy (akcenty)
| Název | HEX | Použití |
|---|---|---|
| Cream | `#faf5e1` | Světlé pozadí alternativních sekcí |
| Pink | `#fadceb` | Dekorativní akcent |
| Blue | `#d3dff5` | Dekorativní akcent |
| Brown | `#aa6e50` | Dekorativní akcent |

### CSS Custom Properties (tokeny)
Stránka používá pojmenované tokeny v CSS. Klíčové:
```css
--token-f7c03d34: #120700;   /* Brand Black */
--token-bfbe3ecb: #ffffff;   /* White */
--token-7e84a827: #ffe654;   /* Brand Yellow */
--token-472a0ea5: #ffdb09;   /* CTA Yellow */
--token-7a42bdcd: #f5c400;   /* Deep Yellow */
--token-c68d3188: #fadceb;   /* Pink */
--token-9c7abb8c: #d3dff5;   /* Blue */
--token-e0e97ab9: #aa6e50;   /* Brown */
```

---

## 2. TYPOGRAFIE

### Font
- **Primární font:** `Inter` (Google Fonts / self-hosted)
- **Variabilní verze:** `Inter Variable` — používána pro display headings (H1)
- **Fallback:** `sans-serif`
- **Font smoothing:** `-webkit-font-smoothing: antialiased`
- **OpenType features aktivní:** `"blwf" on, "cv09" on, "cv03" on, "cv04" on, "cv11" on`

### Typografická hierarchie

| Element | Velikost | Váha | Line-height | Letter-spacing | Transform | Barva |
|---|---|---|---|---|---|---|
| **H1 (Display)** | `96px` | 400 (Regular) | 1.05 (100.8px) | +1% (0.96px) | UPPERCASE | `#ffffff` |
| **H2 (Section)** | `56px` | 800 (ExtraBold) | 1.3 (72.8px) | +1% (0.56px) | UPPERCASE | `#120700` |
| **H3 (Sub-heading)** | `32px` | 700 (Bold) | 1.0 (32px) | normal | none | `#ffffff` |
| **H6 / Eyebrow** | `14px` | 800 (ExtraBold) | 1.1 (15.4px) | +18% (2.52px) | UPPERCASE | `#ffffff` |
| **Body / p** | `14px` | 600 (SemiBold) | 1.6 (22.4px) | +6% (0.84px) | UPPERCASE | `#120700` |
| **Button text** | `14px` | 600 (SemiBold) | — | +6% (0.84px) | UPPERCASE | `#120700` |
| **Small label** | `12px` | 800 (ExtraBold) | 1.1 | +18% (2.52px) | UPPERCASE | `#ffffff` |

### Klíčové typografické vzory
- **Vše uppercase** — celá stránka používá výhradně velká písmena (headings, body, tlačítka, labels)
- **Agresivní letter-spacing** na malých textech (labels, body) — 0.84–2.52px
- **H1 display** je tenký (weight 400), zatímco H2 je extra-bold (800) — vytváří dramatický kontrast
- **H1 čísla** (statistiky) — stejný styl jako display heading, 96px, uppercase

---

## 3. LAYOUT A GRID

### Container
```css
max-width: 1600px;
content-width: ~1393px;   /* při viewport 1520px */
```

### Horizontální padding (sekce)
```
Desktop: 64px vlevo + 64px vpravo (standard)
Varianta: 32px vlevo + 32px vpravo (forma, testimonials)
Varianta: 24px vlevo + 24px vpravo (slider)
```

### Vertikální rytmus (padding sekcí)
| Typ sekce | Padding top | Padding bottom |
|---|---|---|
| Standard sekce | `80px` | `80px` |
| Menší sekce | `64px` | `64px` |
| Hero | `164px` | `80px` |
| CTA sekce | `140px` | `72px` |
| FAQ | `32px` | `64px` |
| Velká sekce | `120px` | `120px` |

### Grid gap
- Layout L: `40–77px` gap mezi sloupci
- Standardní grid: Flexbox nebo CSS Grid

---

## 4. KOMPONENTY

### 4.1 Navigace

**Struktura (2 vrstvy):**
1. **NavBanner** (top bar) — výška `44px`, bg `#120700`, padding `14px 64px`
   - Text: telefon + e-mail, bílá barva, H6 styl (14px, weight 800, letter-spacing 2.52px, uppercase)
   - Uprostřed: "WANT TO LEARN MORE? CONTACT US"
   - Vpravo: divider + telefon + e-mail jako linky

2. **Nav Content** — výška `88px` (celá nav = `132px`)
   - Logo (obrázek, vlevo)
   - Navigační linky (střed/vpravo)
   - CTA button — Primary L (vpravo)

**NavBg:** tmavý background `#120700`, opacity 0 → přechod na opacity 1 při scrollu (transition: opacity 0.4s ease)

```css
nav {
  position: relative; /* nebo sticky při scrollu */
  background-color: transparent;
  width: 100%;
}

[data-framer-name="NavBanner"] {
  background-color: #120700;
  height: 44px;
  padding: 14px 64px;
}

[data-framer-name="NavBg"] {
  background-color: #120700;
  opacity: 0;
  transition: opacity 0.4s ease;
}
```

---

### 4.2 Tlačítka

#### Primary L (hlavní CTA)
```css
.btn-primary-l {
  background-color: #ffdb09;
  color: #120700;
  border-radius: 20px;
  padding: 16px 32px;
  height: 64px;
  font-family: 'Inter', sans-serif;
  font-size: 14px;
  font-weight: 600;
  letter-spacing: 0.84px;
  text-transform: uppercase;
  border: none;
  cursor: pointer;
  display: inline-flex;
  align-items: center;
  justify-content: center;
}
```

#### Primary S (menší CTA)
```css
.btn-primary-s {
  /* stejné jako Primary L, ale: */
  border-radius: 12px;
  height: 54px; /* ~54.4px */
}
```

#### Secondary S (ghost/outline)
```css
.btn-secondary-s {
  background-color: transparent;
  color: #fafafa;
  border-radius: 12px;
  padding: 16px 32px;
  height: 54px;
  font-size: 14px;
  font-weight: 600;
  letter-spacing: 0.84px;
  text-transform: uppercase;
  border: 1px solid rgba(255,255,255,0.3); /* vizuálně, border v DOM je 0px */
}
```

**Pravidlo:** Primary vždy žlutá s tmavým textem, Secondary vždy průhledný s bílým textem.

---

### 4.3 Eyebrow label (štítek před nadpisem)
```css
.eyebrow-badge {
  background-color: rgba(0, 0, 0, 0.4);
  border-radius: 100px;
  padding: 6px 14px 6px 8px;
  display: inline-flex;
  align-items: center;
  gap: 8px;
  /* obsahuje ikonu + text v H6 stylu */
}

.eyebrow-badge h6 {
  font-size: 14px;
  font-weight: 800;
  letter-spacing: 2.52px;
  text-transform: uppercase;
  color: #ffffff;
}
```

---

### 4.4 Pricing / Feature Cards (tmavé)
```css
.card-dark {
  background-color: #120700;
  border-radius: 40px;
  padding: 32px;
  width: ~453px;  /* přizpůsobeno gridu */
}
```
- Interní layout: top (nadpis + badge) + divider + features list + button
- Features list: checkmark icon + text (H6 styl)
- Divider: 1px linka, barva z palety

---

### 4.5 Hero sekce
```css
.hero {
  padding-top: 164px;
  padding-bottom: 80px;
  padding-left: 64px;
  padding-right: 64px;
  position: relative;
}

.hero-overlay {
  background: linear-gradient(258deg, rgba(0,0,0,0.4) 0%, rgba(0,0,0,0.85) 100%);
  position: absolute;
  inset: 0;
}
```
- H1 display text: 96px, weight 400, uppercase, bílá
- Pod H1: USP badges (4× ikona + text, flex row)
- Pod USP: 2 tlačítka vedle sebe (Primary S + Secondary S)
- Pozadí: video nebo obrázek s overlay gradientem

---

### 4.6 Accordion (FAQ)
```css
.accordion-item {
  /* wrapper */
}

.accordion-header {
  /* H4 styl, cursor pointer */
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.accordion-icon {
  /* 2 linky (Line × 2) tvořící + nebo × */
  /* animace rotate při open/closed */
}

.accordion-body {
  /* Closed: výška 0, overflow hidden */
  /* Open: výška auto */
  transition: height 0.3s ease;
}
```
- Stavy: `Open` (expanded) a `Closed` (collapsed)
- Icon: dvě linky (`framer-jwng3c` + `framer-i4g8c3`), animované jako +/×

---

### 4.7 Slider / Carousel
- **Navigace:** 2 šipky vlevo/vpravo (`Left` + `Right` jako `<a>` tagy)
- Šipky jsou kruhová tlačítka s ikonou šipky
- Aktuálně: slider pro "Krakow" case study + testimonials slider

---

### 4.8 Formulář
```css
.form-field-wrapper {
  height: 64px;
  background: transparent;
  /* obsahuje label + input */
}

.form-input {
  background: transparent;
  border: none;
  border-bottom: 1px solid #120700; /* spodní linka jako oddělovač */
  color: #120700;
  font-size: 14px;
  font-weight: 600;
  letter-spacing: 0.84px;
  text-transform: uppercase;
  width: 100%;
}

.form-submit-btn {
  /* stejný styl jako Primary L button */
}
```
- Formulář je na světlém cream (`#faf5e1`) pozadí sekce
- Skupiny polí: "BRANCH INFORMATION", "OTHER", "ANYTHING ELSE"

---

### 4.9 Statistiky / čísla
- Velká čísla: `96px`, weight 400, UPPERCASE, barva `#ffffff` nebo `#ffe654`
- Procento (%) ve stejném stylu jako číslo
- Popisek pod číslem: `h3` styl (32px, bold)
- Použití: "STABILITY OF THE PRODUCT MIX" sekce (Drinks 15%, Chimney Cakes 60%, Ice Cream 25%)

---

### 4.10 Footer
```html
<footer>
  <!-- Plná šířka, bg #120700 -->

  <!-- Horní část -->
  <div class="footer-top">
    <div class="logo-tagline">
      <!-- Logo -->
      <p>A FRANCHISE THAT MAKES SENSE.</p>
    </div>
    <a class="btn-back-to-top">BACK TO TOP ↑</a>
  </div>

  <div class="footer-divider"></div>

  <!-- Střední část — navigační linky -->
  <div class="footer-nav">
    <div>LEARN MORE ABOUT THE FRANCHISE</div>
    <!-- In numbers, Types of franchises, Success in practice, ... -->

    <div>B2C WEB</div>

    <div><!-- Address --></div>

    <div><!-- Contact --></div>
  </div>

  <div class="footer-divider"></div>

  <!-- Spodní část -->
  <div class="footer-bottom">
    <span>© 2026 Twistcafe. All rights reserved.</span>
    <div class="social-links"><!-- Instagram, Facebook, ... --></div>
  </div>
</footer>
```

---

## 5. STRUKTURA STRÁNKY (sekce v pořadí)

| # | Sekce | Framer name | Popis |
|---|---|---|---|
| 1 | NavBanner | `NavBanner` | Top bar: tel + email |
| 2 | Navigace | `Desktop` | Logo + links + CTA |
| 3 | Hero | `Hero` | H1 + USP ikony + 2 CTA tlačítka + BG video/foto |
| 4 | Video Reveal | `Video Reveal` | Full-bleed video sekvence |
| 5 | Numbers / Invest | `Section` | H1 velký text + investiční karty |
| 6 | Franchise Types | `Section` | H2 + 3 pricing cards (New/Existing/License) |
| 7 | Success (Krakow) | `Section` | H2 + slider s konkrétní pobočkou |
| 8 | Full Management | `Section` | H2 + 7× H3 list |
| 9 | Product Mix | `Section` | H2 + velká čísla (%) + kategorie produktů |
| 10 | Branch Overview | `Section` | H2 + 5 feature cards s ikonou |
| 11 | Application Form | `Section` | H2 + kontaktní formulář |
| 12 | Founder Story | `Section` | H2 + text + fotka |
| 13 | Reviews | `Section` | H2 + testimonial slider + hodnocení hvězdičkami |
| 14 | FAQ | `Section` | H1 "WHAT ARE YOU MOST INTERESTED IN?" + accordion |
| 15 | Footer | `Desktop` | Logo + navigace + adresa + copyright |

---

## 6. VIZUÁLNÍ STYL A PRAVIDLA

### Design jazyk
- **Tmavý, prémiový styl** — téměř celá stránka na `#120700` pozadí
- **Bold typografie** — velká bezpatkový font s agresivním letter-spacingem
- **Minimální barevnost** — pouze žlutá jako akcent, vše ostatní je bílé na tmavém
- **Uppercase all the way** — žádný lowercase text viditelný v UI
- **Velkorysé whitespace** — sekce dýchají, padding minimálně 80px vertikálně

### Efekty a animace
- **Nav opacity transition:** `opacity 0 → 1` při scrollu (0.4s ease)
- **NavBg** se zobrazí při scrollu přes hero
- **Accordion:** height transition pro open/close
- **Hover na footer linkách:** barva přechází na `#ffdb09` (CTA yellow)

### Ikonografické prvky
- Kruhové ikony v kartách (Icon - Round)
- Checkmark ikony v feature lists
- Šipkové navigační prvky ve sliderech
- Sociální sítě ikony ve footeru

### Responzivita
- Breakpoints nejsou explicitní z kódu (Framer), ale struktura naznačuje:
  - Desktop: `Layout L` s `max-width: 1600px`
  - Skryté elementy: `hidden-72rtr7`, `hidden-1jp9pa2`, `hidden-1qvnpt1` (utility classy pro různé viewporty)
  - Spacer elementy se zobrazují/skrývají dle breakpointu

---

## 7. HTML VZORY (šablony)

### Section wrapper
```html
<section style="padding: 80px 64px; background: transparent;">
  <div class="layout-l" style="max-width: 1600px; margin: 0 auto;">
    <!-- content -->
  </div>
</section>
```

### Section title blok (eyebrow + H2)
```html
<div class="section-title">
  <div class="eyebrow-badge">
    <span class="icon"><!-- SVG --></span>
    <h6>EYEBROW LABEL</h6>
  </div>
  <h2>SECTION<br>HEADING</h2>
</div>
```

### USP list item
```html
<div class="usp-item">
  <div class="usp-icon"><!-- SVG ikona --></div>
  <p>USP TEXT</p>
</div>
```

### Feature/check item
```html
<div class="feature-block">
  <div class="check-icon"><!-- SVG checkmark --></div>
  <p>Feature description text</p>
</div>
```

### Pricing card
```html
<div class="card-dark" style="background:#120700; border-radius:40px; padding:32px;">
  <div class="card-top">
    <h3>Card Title</h3>
    <div class="badge">...</div>
  </div>
  <div class="divider"></div>
  <div class="features">
    <h6>ADVANTAGES</h6>
    <!-- feature items -->
    <h6>TWIST GUARANTEES</h6>
    <!-- feature items -->
  </div>
  <a class="btn-primary-l">CTA BUTTON</a>
</div>
```

### Statistic number
```html
<div class="stat-block">
  <h3>CATEGORY NAME</h3>
  <div class="numbers">
    <h1>60</h1>
    <h1>%</h1>
  </div>
  <p>description</p>
</div>
```

---

## 8. CSS RESET A GLOBÁLNÍ PRAVIDLA

```css
html, body, #main {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

:root {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

* {
  box-sizing: border-box;
  -webkit-font-smoothing: inherit;
}

h1, h2, h3, h4, h5, h6, p, figure {
  margin: 0;
}

body {
  background-color: #120700;
  font-family: 'Inter', sans-serif;
  font-size: 12px;
}

/* Skrytí scrollbaru */
div::-webkit-scrollbar {
  display: none;
}
```

---

## 9. KLÍČOVÁ POZOROVÁNÍ

1. **Stránka je postavena ve Frameru** — veškeré třídy jsou `framer-*`, struktura je generovaná nástrojem
2. **Pozadí stránky je tmavé `#120700`**, přičemž sekce samy nemají vlastní pozadí (transparent) — globální barva "prosvítá"
3. **Dvě varianty H2** — bílá (na tmavém) a tmavá `#120700` (na světlém cream pozadí)
4. **Žlutá je výhradně pro CTA** — tlačítka a drobné akcenty, nikdy jako pozadí celé sekce
5. **Letter-spacing je zásadní** — malé texty (body, labels, buttons) mají výrazný tracking (+6–18%)
6. **Border-radius eskaluje s velikostí** — malé tlačítko: 12px, velké tlačítko: 20px, velká karta: 40px, badge: 100px (pill)
7. **Formulář je na světlém pozadí** — vizuální kontrast oproti většině tmavých sekcí
8. **Navigační struktura je dvouúrovňová** — top banner + main nav
9. **Font Inter Variable** pro display (H1), standard Inter pro ostatní
10. **Multijazyčnost** — stránka má česky/anglicky varianty obsahu v HTML (data-framer-name obsahuje "CZ", "EN")
