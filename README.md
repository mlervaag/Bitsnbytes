# Bits & Bytes — 4-bit Ripple-Carry Adder Visualizer

En interaktiv webapp som visuelt demonstrerer hvordan to 4-bits tall adderes gjennom logiske gater. Strøm animeres sakte gjennom kretsen fra input til resultat, med lysende ledninger og synlige AND, OR, XOR-gater.

Inspirert av museumseksponater som viser digital logikk på en håndgripelig måte.

## Skjermbilde

Appen har et mørkt neon-tema med fargekodede signaler:
- **Cyan** — A-bits (første tall)
- **Magenta** — B-bits (andre tall)
- **Oransje** — Mente/carry (overføring mellom kolonner)
- **Grønn** — Sum (resultat-bits)

## Funksjoner

### Interaktiv krets
- Velg to tall (0–15) med +/- knapper
- Se signalene flyte gjennom alle 20 logiske gater i sanntid
- Animasjonshastighet justerbar (1x–10x)
- «Spill av»-knapp for å kjøre animasjonen på nytt

### Binær addisjon på papir
- Synkronisert papir-visning som viser kolonne-for-kolonne addisjon
- Kobler den kjente «addisjon på papir»-metoden med kretslogikken
- Viser mente (carry) som bæres mellom kolonner

### Trinnvis forklaring
- Tekstbeskrivelse oppdateres i sanntid under animasjonen
- Forklarer hva hver Full Adder beregner (Ai + Bi + Cin = Sum, Carry)

### 5-bit resultat
- LED-lignende indikatorer viser S4 S3 S2 S1 S0
- Desimaltall-visning av resultatet

### Pedagogisk innhold (5 faner)
1. **Binære tall** — Posisjonsverdier, konvertering desimal↔binær, 4-bit tabell
2. **Logiske gater** — AND, OR, XOR med sannhetstabeller og forklaringer
3. **Full Adder** — Hvordan 5 gater legger sammen 1 bit + carry
4. **Ripple-Carry** — Hvordan 4 Full Adders kobles i serie
5. **I virkeligheten** — Moderne CPUer, transistorer, carry-lookahead

## Teknologi

Hele appen er én enkelt HTML-fil uten avhengigheter:
- **HTML** — Struktur og innhold
- **CSS** — Dark theme med CSS custom properties, neon glow-effekter
- **JavaScript** — Kretslogikk, SVG-generering, animasjonssystem
- **SVG** — Programmatisk tegnet kretsdiagram med gater og ledninger

Ingen build-verktøy, ingen npm, ingen rammeverk. Bare åpne `index.html` i en nettleser.

## Kjøre appen

```
# Åpne direkte i nettleser
open index.html

# Eller bruk en enkel HTTP-server
python3 -m http.server 8000
# Gå til http://localhost:8000
```

## Kretsarkitektur

### Full Adder (1 bit)
Hver Full Adder har 3 innganger og 2 utganger:

```
Innganger: A, B, Cin (carry inn)
Gater:
  XOR1: P = A ⊕ B        (delvis sum / propagate)
  AND1: G = A · B         (direkte carry / generate)
  XOR2: S = P ⊕ Cin       (endelig sum)
  AND2: H = P · Cin        (propagert carry)
  OR:   Cout = G + H       (total carry ut)
Utganger: S (sum-bit), Cout (carry ut)
```

### 4-bit Ripple-Carry Adder

Fire Full Adders i kjede der carry «bølger» fra FA0 til FA3:

```
  A3,B3      A2,B2      A1,B1      A0,B0
    │          │          │          │
┌───┴───┐  ┌───┴───┐  ┌───┴───┐  ┌───┴───┐
│  FA3  │←─│  FA2  │←─│  FA1  │←─│  FA0  │←─ Cin=0
└───┬───┘  └───┬───┘  └───┬───┘  └───┬───┘
  S4,S3      S2          S1          S0
```

- **FA0** beregnes først (Cin = 0)
- Carry fra FA0 → FA1 → FA2 → FA3
- Resultat: 5 bits (S4 S3 S2 S1 S0), verdi 0–30

## Filstruktur

```
Bitsnbytes/
├── index.html    # Hele appen (HTML + CSS + JS + SVG)
└── README.md     # Denne filen
```

## Nettleserstøtte

Fungerer i alle moderne nettlesere med SVG-støtte:
- Chrome / Edge
- Firefox
- Safari

## Lisens

MIT
