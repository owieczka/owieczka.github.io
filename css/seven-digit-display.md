---
date: 2023-08-25
share: true
title: Seven Digit Display
parent: CSS
---
# Wyświetlacz 7-segmentowy w CSS i Javascript

Prosty tutorial jak przygotować wyświetlacze siedmio segmentowy w JavaScript i CSS

GitHub - [7-Segment Digital Clock Tutorial (github.com)](https://github.com/owieczka/Tutorial-DigitalClock-JS)
## Krok 1 - Przygotowanie jednego segmentu wyświetlacza 7 segementowego

Pojedyńcza cyfra

```html
<body>
  <div class="segment digit-0">
    <div class="bar-h bar-a"></div>
    <div class="bar-h bar-b"></div>
    <div class="bar-h bar-c"></div>
    <div class="bar-v bar-v-t bar-d"></div>
    <div class="bar-v bar-v-t bar-e"></div>
    <div class="bar-v bar-v-b bar-f"></div>
    <div class="bar-v bar-v-b bar-g"></div>
  </div>
</body>
```

![Single Digit](../WebPage/css/css-assets/sevendigit/digit.jpg)

Więcej - [Pojedyńcza Cyfra - krok po kroku](seven-digit-display-step01.md)
## Krok 2 - WebComponent - komponent html'a

Reużywalny komponent cyfry
```html
<body>
  <segment-box class="digit-0"></segment-box>
  <segment-box class="digit-1"></segment-box>
  <segment-box class="digit-2"></segment-box>
  <segment-box class="digit-3"></segment-box>
  <segment-box class="digit-4"></segment-box>
  <segment-box class="digit-5"></segment-box>
  <segment-box class="digit-6"></segment-box>
  <segment-box class="digit-7"></segment-box>
  <segment-box class="digit-8"></segment-box>
  <segment-box class="digit-9"></segment-box>
</body>
```
![Single Digit](../WebPage/css/css-assets/sevendigit/digit.jpg)

Więcej - [Własny WebKomponent](WebPage/css/seven-digit-display-step02.md) 