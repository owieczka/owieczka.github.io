---
date: 2023-08-25
share: true
title: Seven Digit Display Step 01
parent: Seven Digit Display
---
## Krok 1 - Przygotowanie jednego segmentu wyświetlacza 7 segementowego

Pojedyczńca cyfra

![Single Digit](digit.jpg)

### Segment

Zaczynamy od pojedyńczego elementu `div`
```html
<div class="segment">
</div>
```
który można ustawić koło siebie w lini czyli  `display: inline-block`. Zdefiniujmy sobie klase css `segment` określającą pojedyńczy segment naszego wyświetlacza 7-segmentowego. Ustalmy sobie jego wielkość na `--s-width` i `--s-height` określone jako zmienne css które bedzie można sobie potem swobodnie zmieniać. Ponieważ inne elementy naszego wyświetlacza będziemy obliczac na podstawie zmiennych `--s-width` i `--s-heigth` ustawmy je jako liczby bez jednostek, ułatwi to obliczenia arytmetyczne na tych zmiennych. Ustawmy też sobie kolor tła na szary `#626262`. 

```css
.segment {
  --s-width: 60;
  --s-height: 100;
  --s-color: #626262;
  position: relative;
  left: 0;
  top:0;
  display: inline-block;
  width: calc(var(--s-width)*1px);
  height: calc(var(--s-height)*1px);
  background-color: var(--s-color);
}
```

![Segment](step01-01.jpg)

### Element aktywny

Kolejnym potrzebnym elementem jest pojedyńcze pole aktywne które można zapalać i gasić.
```html
<div class="segment">
  <div class="bar-h"></div>
</div>
```
Zdefiniujmy sobie kolejną klase css `bar-h` które bedzie reprezentowała pojedyńczy element aktywny naszego segmentu - linie poziomą. Element bedzie się składał z 3 cześci: cześci środkowej i dwóch zakończeń zrealizowanych jako elementy `before` i `after`. 

Nasz element aktywny bedzie miał szerokość segmentu oraz wysokość `--bar-thickness`. Przypiszemy mu też kolor tła `--bar-color`, który przypiszeny do nowej zmiennej `--local-bar-color` aby móc zmienić go na inny w przyszłości oraz wykorzystać w elementach `before` i `after` które w hierarchi sa podelementami elementu `bar-h`
```css
 .bar-h {
  --local-bar-color: var(--bar-color);
  position: absolute;
  box-sizing: border-box;
  width: calc((var(--s-width)) * 1px);
  height: calc(var(--bar-thickness) * 1px);
  background-color: var(--local-bar-color);
}
```
Jako początek i zakończenie elementu wykorzystami obrócony o 45 stopni kwadrat. Do obrócenia elementu wykorzystamy własność `transform`. Pierw przesuwamy element o 50% tak aby rotacja zachodziła względem środka elementu a potem odstawiamy go na pozycje będąco połową rozmiaru elementu. Wielkość elementów `before` i `after` wyliczamy tak aby przekątna tych elementów była równa wysokości pojedyńczego elementu aktywnego. 

```css
.bar-h::before, .bar-h::after{
  content: "";
  position: absolute;
  box-sizing: border-box;
  width: calc(var(--bar-thickness) / 2 * 1.4142px);
  height: calc(var(--bar-thickness) / 2 * 1.4142px);
  left: 0;
  top: 0;
  transform: translate(-50%, -50%) rotate(45deg) translate(50%,50%);
  background-color: var(--local-bar-color);
}
.bar-h::before {
  left: 0;
}
.bar-h::after {
  left: 100%;
}
```
I dodanie nowych zmiennych css do klasy `segment`
```css
.segment {
  --bar-thickness: 20;
  --bar-color: #ff0000;
}
```

![Element Aktywny](step01-02.jpg)
### Dopasowanie rozmiary elementu aktywnego

Element aktywny jest troszkę za duży i wystaje w naszego segmentu. Cały element należy skrócić o wielkość końcówek - dwukrotność `--bar-thickness` i przesunąć o `--bar-thickness`. Element przesuniemy przez dodanie lewego i prawego marginesu

```css
 .bar-h {
  --local-bar-color: var(--bar-color);
  position: absolute;
  box-sizing: border-box;
  width: calc((var(--s-width) - var(--bar-thickness) * 2) * 1px);
  height: calc(var(--bar-thickness) * 1px);
  margin-left: calc(var(--bar-thickness) * 1px);
  margin-right: calc(var(--bar-thickness) * 1px);
  background-color: var(--local-bar-color);
}
.bar-h::before, .bar-h::after{
  content: "";
  position: absolute;
  box-sizing: border-box;
  width: calc(var(--bar-thickness) / 2 * 1.4142px);
  height: calc(var(--bar-thickness) / 2 * 1.4142px);
  left: 0;
  top: 0;
  transform: translate(-50%, -50%) rotate(45deg) translate(50%,50%);
  background-color: var(--local-bar-color);
}
.bar-h::before {
  left: 0;
}
.bar-h::after {
  left: 100%;
}
```

![Element aktywny](step01-03.jpg)

### Trzy poziome elementy aktywne

Dodajmy wiecej elementów `div` do naszego segment. Każdy element bedzie reprezentował jeden element naszego wyświetlacza 7-segmentowego.
```html
<div class="segment digit-8">
  <div class="bar-h bar-a"></div>
  <div class="bar-h bar-b"></div>
  <div class="bar-h bar-c"></div>
</div>
```
Trzy dodatkowe klasy css `bar-a`, `bar-b` i `bar-c` pozwalają na ustawienie położenia trzech elementów aktywnych na górze, na dole i po środku.
```css
.bar-a {
  top: 0%;
  left: 0%;
}
.bar-b {
  top: calc(50% - var(--bar-thickness) / 2 * 1px);
  left: 0%;
}
.bar-c {
  bottom: 0%;
  left: 0%;
}
```

![Trzy element aktywne](step01-04.jpg)

### Pionowy element aktywny

Teraz przygotujemy pionowy element aktywny i odpowiadająca mu klasę css `bar-v`.

```html
<div class="segment digit-8">
  <div class="bar-h bar-a"></div>
  <div class="bar-h bar-b"></div>
  <div class="bar-h bar-c"></div>  
  <div class="bar-v bar-v-t bar-d"></div>
</div>
```

Pionowy element aktywny jest podobny do poziomego elementu akrywnego, z tą różnicą iż jego wielkość określona jest na `--bar-thickness` na `--s-height / 2` z korekta na końcówkę 

```css
.bar-v {
  --local-bar-color: var(--bar-color);
  position: absolute;
  box-sizing: border-box;
  width: calc(var(--bar-thickness) * 1px);
  height: calc((var(--s-height) / 2 - var(--bar-thickness) * 1.5) * 1px);
  background-color: var(--local-bar-color);
}
.bar-v::before, .bar-v::after{
  content: "";
  position: absolute;
  box-sizing: border-box;
  width: calc(var(--bar-thickness) / 2 * 1.4142px);
  height: calc(var(--bar-thickness) / 2 * 1.4142px);
  left: 0;
  top: 0;
  transform: translate(-50%, -50%) rotate(45deg) translate(50%,-50%);
  background-color: var(--local-bar-color);
}
.bar-v::before {
  top: 0;
}
.bar-v::after {
  top: 100%;
}
.bar-v-t {
  margin-top: calc(var(--bar-thickness) * 1px);
  margin-bottom: calc(var(--bar-thickness) / 2 * 1px);
}
```

klasa `bar-d` pozwala na ustawienie elementu w odpowiedniej pozycji

```css
.bar-d {
  top: 0%;
  left: 0%;
}
```

![Trzy element aktywne](step01-05.jpg)

Elementy pionowe w górnej części segmentu powinny mieć inaczej istanione marginesy niż w dolnej cześci dlatego tworzymy dodatkową klase css `bar-v-b` aby ustawić marginesy symetrycznie dla dolnego elementu aktywnego

```css
.bar-v-b {
  margin-top: calc(var(--bar-thickness) / 2 * 1px);
  margin-bottom: calc(var(--bar-thickness) * 1px);
}
```

Wszystkie pionowe elementy aktywne

```html
<div class="segment digit-8">
  <div class="bar-h bar-a"></div>
  <div class="bar-h bar-b"></div>
  <div class="bar-h bar-c"></div>
  <div class="bar-v bar-v-t bar-d"></div>
  <div class="bar-v bar-v-t bar-e"></div>
  <div class="bar-v bar-v-b bar-f"></div>
  <div class="bar-v bar-v-b bar-g"></div>
</div>
```

I ich klasy pozycjonujące

```css
.bar-e {
  top: 0%;
  right: 0%;
}
.bar-f {
  top: 50%;
  left: 0%;
}
.bar-g {
  top: 50%;
  right: 0%;
}
```

![Trzy element aktywne](step01-06.jpg)

### Marginesy pomiedzy elementami aktywnymi

Obecnie elementy aktywne dotykają się. W wyświetlaczach 7-segmentowych elementy aktywne oddzielone są od siebie przerwą. W celu zrobienia przerw możemy wykorzystać właśnosć `padding` która nie zmieny rozmiarów elementów w modelu pudełkowym `box-model: border-box`

Na poziomych elementach dodajmy `padding` od góry i od dołu, a na elementach pionowych z lewej i prawej stronie. Aby miec możliwość sterowanie wielkością odstępów, wykorzystamy zmienną `--bar-padding` zdefiniowaną na poziomie segmentu

```css
 .segment {
  --s-width: 60;
  --s-height: 100;
  --s-color: #626262;
  --bar-thickness: 20;
  --bar-padding: 2;
  /*...*/
  background-color: var(--s-color);
}
```

Aby kolor tła wypełniony był tylko wewnątrz obszaru paddingu, niezbędne jest ustawienie wykadrowania tła `background-clip: content-box` do obszaru treści. 

```css
.bar-h {
  --local-bar-color: var(--bar-color);
  position: absolute;
  box-sizing: border-box;
  /*..*/
  padding-top: calc(var(--bar-padding) * 1px);
  padding-bottom: calc(var(--bar-padding) * 1px);
  background-clip: content-box;
}
/*...*/
.bar-v {
  --local-bar-color: var(--bar-color);
  position: absolute;
  box-sizing: border-box;
  /*...*/
  padding-left: calc(var(--bar-padding) * 1px);
  padding-right: calc(var(--bar-padding) * 1px);
  background-clip: content-box;
}
```
W przypadku końcówek elementów aktywnych czyli elementów `before` i `after` wielkość paddingu wymaga przeliczenia ze względu na zastosowaną transformacje (rotaceje)

```css
.bar-h::before, .bar-h::after{
  content: "";
  position: absolute;
  box-sizing: border-box;
  /*...*/
  padding: calc(var(--bar-padding) / 1.4142 * 1px);
  background-clip: content-box;
}
/*...*/
.bar-v::before, .bar-v::after{
  content: "";
  position: absolute;
  box-sizing: border-box;
  /*..*/
  padding: calc(var(--bar-padding) / 1.4142 * 1px);
  background-clip: content-box;
}
```
W efekcie otrzymujemy ładne równe przerwy pomiedzy elementami aktywnymi

![Przerwy pomiedzy elementami aktywnymi](step01-07.jpg)

### Definicja wyświetlanych cyfr

Ostatnim elementem jest możliwość przełącznania wyświetlanych cyfr na wyświetlaczu. W zależnosci od przypisanego koloru do poszczególnych elementów aktywnych wyświetlacza, możemy wyświetlić różne cyfry. Stwórzmy sobie klase css `digit-0` przypisywana do całego segmentu wyświetlacza reprezentującą konkretny układ elementów aktywnych reprezenutujący zero.

```css
/* 0 definition */
.digit-0 .bar-a { --bar-color: var(--bar-color-on) }
.digit-0 .bar-b { --bar-color: var(--bar-color-off) }
.digit-0 .bar-c { --bar-color: var(--bar-color-on) }
.digit-0 .bar-d { --bar-color: var(--bar-color-on) }
.digit-0 .bar-e { --bar-color: var(--bar-color-on) }
.digit-0 .bar-f { --bar-color: var(--bar-color-on) }
.digit-0 .bar-g { --bar-color: var(--bar-color-on) }
```
gdzie `--bar-color-on` i `--bar-color-off` są dwoma zmiennymi css zdefiniowanymi w klasie `segment` okreslojącymi okolor elementu aktywnego w stanie właczonym i wyłączonym
```css
.segment {
  --s-width: 60;
  --s-height: 100;
  --s-color: #626262;
  --bar-thickness: 20;
  --bar-padding: 2;
  --bar-color-on: red; /*#f6fa10;*/
  --bar-color-off: #828282;
  /*...*/
}
```
Przypisanie klasy `digit-0` do segmentu, wyświetli nam cyfrę 0 na naszym wyświetlaczu 7-segmentowym

```html
<div class="segment digit-0">
  <div class="bar-h bar-a"></div>
  <div class="bar-h bar-b"></div>
  <div class="bar-h bar-c"></div>
  <div class="bar-v bar-v-t bar-d"></div>
  <div class="bar-v bar-v-t bar-e"></div>
  <div class="bar-v bar-v-b bar-f"></div>
  <div class="bar-v bar-v-b bar-g"></div>
</div>
```

![Cyfra 8](step01-08.jpg)

podobnie definiujemy klasy dla pozostałych cyfr 1-9

[Index](../readme.md)