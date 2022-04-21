---
title: Guida CSS
layout: single
---

CSS è un acronimo che sta per **C**ascading **S**tyle **S**heet, foglio di stile a cascata. È utilizzato per formattare il codice HTML mantenendo leggibile la struttura della pagina.

Indice:
- [Storia](#storia)
- [Collegare CSS e HTML](#collegare-css-e-html)
  - [CSS esterno](#css-esterno)
  - [CSS interno](#css-interno)
  - [CSS in linea](#css-in-linea)
- [Sintassi](#sintassi)
  - [Commenti](#commenti)
  - [Selettori](#selettori)
  - [Proprietà](#proprietà)
  - [Funzioni](#funzioni)
- [Colori](#colori)
  - [RGB e RGBA](#rgb-e-rgba)
  - [HSL e HSLA](#hsl-e-hsla)
  - [Colori esadecimali](#colori-esadecimali)

## Storia

Nel 1993 alcuni browser web iniziarono a presentare tag proprietari, come `<font>`, che funzionavano solo al loro interno. Questo portò i programmatori a farne molto uso per poter cambiare lo stile della pagina web ma portò anche a molti problemi:

- I tag dei file HTML sono molto più lunghi a causa dei molti attributi, questo li rendeva più pesanti in termini di memoria e rallentava (oggi non sarebbe più un problema) il loro trasferimento e la loro lettura
- Il codice diventava spesso molto difficile da leggere ed era molto confuso perché non aveva degli standard.
- Molti browser non supportavano tutti i tag o tutti gli attributi che erano presenti in altri browser (oggi il problema esiste ancora ma è più limitato)

Per questi e altri problemi, il W3C (**W**orld **W**ide **W**eb **C**onsortium) presentò nel 1996 le specifiche del CSS 1. Queste separavano la formattazione dalla struttura e davano uno standard che i browser potessero seguire.

## Collegare CSS e HTML

Esistono tre modi per mettere CSS in HTML: esterno, interno e in linea.

### CSS esterno

Il CSS è scritto principalmente in file secondari con l'estensione `.css`. Per collegare un file esterno in HTML si usa il tag `<link>` e CSS non fa differenza.
Basta inserire il tag all'interno di `<head>`, con `rel="stylesheet"` e `href="nome-del-file.css"`[^1] quindi il tag completo diventerebbe:

```html
<head>
    <title>Titolo della pagina</title>
    <link rel="stylesheet" href="nome-del-file.css" />
</head>
```

### CSS interno

È possibile scrivere CSS direttamente all'interno del file HTML. Questo è fatto all'interno del tag `<style>`.

```html
<head>
    <style>
        p {
            font-family: monospace;
        }
    </style>
</head>
```

### CSS in linea

Per dare velocemente uno stile ad un singolo elemento è possibile scrivere il CSS come valore dell'attributo `style`.

```html
<body style="background-color: black;">

</body>
```

Nota che non è possibile utilizzare i [selettori](#selettori) quando si scrive CSS in linea.

[^1]: `nome-del-file` è sostituito con il nome effettivo del file.


## Sintassi

Il codice CSS ha una sintassi completamente diversa da quella di HTML. Esso è composto da [selettori](#selettori), che specificano l'elemento a cui applicare lo stile e da dichiarazioni che contengono le [proprietà](#proprietà), l'equivalente degli attributi in HTML, e i loro valori.

Questo è un esempio di codice CSS:
```css
p {
    text-align: center;
    color: rgb(255, 0, 90);
}
```

In questo caso `p` è il selettore, `text_align` e `color` sono proprietà, e `center` e `rgb(255, 0, 90)` sono valori. Da notare che tutte le proprietà sono racchiuse tra due parentesi graffe che si scrivono con `Alt Gr` + `è` per `{` e `Alt Gr` + `+` per `}`. Il valore di una proprietà è preceduto da `:`, come succedeva per l'uguale (`=`) in HTML e termina con un punto e virgola `;`. Questo perché CSS è fatto per poter essere scritto in una singola riga, quindi ogni nuova riga e le indentazioni servono solo a rendere il codice leggibile. Questo significa che il codice sopra potrebbe essere scritto così:

```css
p{text-align:center;color:rgb(255,0,90);}
```
ma è chiaramente meno leggibile di quello sopra.

### Commenti

I commenti in CSS si aprono con `/*` e si chiudono con `*/` e servono per rendere più chiare le intenzioni di quello che si sta facendo, essi possono occupare più righe e vengono completamente ignorati.

```css
/* Questo è un commento in una sola riga */
body {
    background-color: red;
}
/* Questo è un commento
che si espande
in più righe */
```

### Selettori

Esistono vari tipi di selettori ma verranno approfonditi solo i selettori semplici.

I selettori semplici permettono di selezionare un elemento basandosi su nome, classe o id. Per selezionare un elemento per nome basta scrivere il nome del tag, esempio con un paragrafo:

```css
p {
    color: white;
}
```

---

Per selezionare un elemento in base all'id, si scrive un cancelletto `#` seguito dal nome dell'id che si vuole selezionare. Da tenere a mente che non dovrebbero esistere più elementi con lo stesso id. Per dare un ad ad un elemento basta usare l'attributo `id`, qui il valore *non* deve essere preceduto da un cancelletto e non deve contenere spazi o iniziare con un numero.

Un esempio con CSS e HTML sempre di un paragrafo:[^2]

```html
<html>
<!-- Tralascio <head> -->

<body>
    <p id="p1">Paragrafo uno</p>
    <p id="p2">Paragrafo due</p>
</body>
</html>
```

```css
#p1 {
    font-family: monospace;
}

#p2 {
    font-size: 20px;
}
```

[^2]: tutto quello tra `<!--` e `-->` è un commento in HTML

---

Per selezionare un elemento in base alla classe, si scrive un punto `.` seguito dal nome della classe. Come per l'id, la classe viene impostata sull'elemento con l'attributo `class`, non deve contenere il punto presente in CSS e non può iniziare con un numero. A differenza dell'id, si possono avere più elementi con la stessa classe e un elemento può avere più classi. Per dare più classi ad un elemento basta separarle con uno spazio.
Si possono selezionare classi appartenenti ad un solo tipo di elemento mettendo il nome dell'elemento davanti alla classe separandoli con un punto.

Un esempio di come possono essere applicate le classi:

```css
.b {
    font-weight: bold;
}

p.i {
    font-style: italic;
}

.u {
    text-decoration: underline;
}
```

```html
<!-- Ometto <html> e <head> -->
<body>
    <!-- uso le classi 'b', 'i' e 'u' invece dei tag
         per dare lo stile a tutto il paragrafo -->
    <p class="b i u"></p>

    <!-- la classe 'i' non fa nulla perché modifica solo i tag <p> -->
    <h1 class="i">Titolo</h1>
</body>
```

---

Il selettore di gruppo permette di unire vari selettori che siano id, classe o nome dell'elemento. Ogni selettore da aggiungere è separato da una virgola:

```css
/* Un selettore che comprente tutti i titoli */
h1, h2, h3, h4, h5, h6 {
    font-family: monospace;
}
```

Un selettore di gruppo non deve avere tutti i selettori compresi dello stesso tipo:

```css
/* Comprende la classe 'bold', l'id 'important-p' e gli elementi 'div' */
.bold, #important-p, div {
    font-weight: bold;
}
```


### Proprietà

Le proprietà sono, in parte, l'equivalente degli attributi in HTML. Esse sono formate da una o più parole separate da trattini `-`.
Per dare un valore a queste proprietà si utilizzano i due punti `:`. Il valore in sé può essere di vari tipi spiegati in seguito.

### Funzioni

Le funzioni in CSS prendono degli argomenti e contengono del codice che svolge una funzione in base ad essi. Una funzione si dice che viene "chiamata" quando il codice contenuto all'interno viene eseguito. Per chiamare una funzione si scrive il nome di essa, seguito da un paio di parentesi tonde `()` che contengono gli argomenti separati da virgole:

```css
.rosso {
    background-color: rgb(255, 0, 0);
}
```

Qui `rgb` è la funzione e fiene chiamata con gli argomenti `255`, `0` e `0`. Attenzione a mettere il numero esatto di argomenti che una funzione accetta e di *non* mettere una virgola in più alla fine: `rgb(255, 0, 0,)` è sbagliato.

## Colori

In CSS esistono vari modi per selezionare un colore:

- [Colori predefiniti](https://www.w3schools.com/cssref/css_colors.asp)
- [Funzioni rgb e rgba](#rgb-e-rgba)
- [Funzioni hsl e hsla](#hsl-e-hsla)
- [Colori esadecimali](#colori-esadecimali)

### RGB e RGBA

La [funzione](#funzioni) `rgb()` prende tre argomenti: il valore del rosso, del verde e del blu necessari per rappresentare un colore. Ognuno di questi valori è un numero intero che va da 0 a 255 compreso.

La [funzione](#funzioni) `rgba()` prende un'argomento in più: la [percentuale](#tipi-di-valori) di trasparenza del colore.

```css
.rosso {
    background-color: rgb(255, 0, 0);
}

.verdino {
    background-color: rgba(0, 255, 0, 50%);
}

.bianco {
    background-color: rgb(255, 255, 255);
}
```

### HSL e HSLA

La [funzione](#funzioni) `hsl()` sfrutta un sistema diverso di rappresentazione di colori e prende tre valori: la tinta, la saturazione e la lucentezza (in inglese **h**ue, **s**aturation e **l**ightness).

La tinta è un numero intero che può avere un valore tra 0 e 360 compresi, la saturazione e la lucentezza sono entrambe [percentuali](#tipi-di-valori).

Come per `rgba()`, `hsla()` prende un quarto valore: la trasparenza, che è anch'esso una pencentuale.

```css
/* i colori sono gli stessi di rgb() e rgba() */
.rosso {
    background-color: hsl(0, 100%, 50%);
}

.verdino {
    background-color: hsla(120, 100%, 50%, 50%);
}

.bianco {
    background-color: hsl(0, 0%, 100%);
}
```

### Colori esadecimali

I colori esadecimali, in CSS, sono una rappresentazione esadecimale dei colori ottenuti con `rgb()` e `rgba()`[^3], sono preceduti da un cancelletto `#` e possono avere quattro diverse lunghezze:

```
#rrvvbb
#rrvvbbtt
#rvb
#rvbt
```

Qui `r` sta per rosso, `v` per verde, `b` per blu e `t` per trasparenza, quindi, nel primo tipo di colore, le prime due cifre del numero cambiano il livello del rosso del colore, le seconde due quello del verde e le ultime due quello del blu.

Le cifre singole sono utilizzate solo quando sia la prima che la seconda cifra di ogni colore (e della trasparenza) sono uguali, quindi scrivere `#ff0077` o `#f07` è indifferente.

```css
/* i colori sono gli stessi di rgb() e rgba() */
.rosso {
    background-color: #f00;
}

.verdino {
    background-color: #00ff0077;
}

.bianco {
    background-color: #ffffff;
}
```

[^3]: Contando in esadecimale `00` è uguale a `0` e `ff` è uguale a `255`, una diretta correlazione con le due funzioni

## Tipi di valori

In CSS le proprietà possono avere vari tipi di attributi[^4]:

- `%` percentuali
- `em` dimensione del font dell'elemento corrente
- `rem` dimensione del font dell'elemento principale (il tag `<html>`)
- `vw` 1% della larghezza della finestra del browser
- `vh` 1% dell'altezza della finestra del browser
- `cm` centimetri
- `mm` millimetri
- `px` pixel

Per specificare il tipo di un valore (numerico) bisogna mettere il valore in sé, seguito dall'unità di misura:

```css
p {
    font-size: 20px;
}
```

Ci possono essere anche delle proprietà che hanno dei valori in parola, in questo caso essi non hanno un'unità di misura:

```css
body {
    background-repeat: no-repeat;
}
```
In questo caso `background-repeat` accetta quattro valori: `repeat`, `no-repeat`, `repeat-x` e `repeat-y`. Qualsiasi altro valore non funziona.

[^4]: Non sono elencati tutti i tipi di valori