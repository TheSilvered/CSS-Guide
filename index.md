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
- [Tipi di valori](#tipi-di-valori)
- [Foglio a cascata](#foglio-a-cascata)
- [Il Box Model di CSS](#il-box-model-di-css)
- [Lista delle proprietà](#lista-delle-proprietà)
  - [background](#background)
    - [background-color](#background-color)
    - [background-image](#background-image)
    - [background-size](#background-size)
    - [background-repeat](#background-repeat)
    - [background-attachment](#background-attachment)
  - [text](#text)
    - [text-align](#text-align)
    - [text-decoration-line](#text-decoration-line)
    - [text-decoration-style](#text-decoration-style)
    - [text-decoration-color](#text-decoration-color)
    - [text-decoration-thickness](#text-decoration-thickness)
  - [font](#font)
    - [font-family](#font-family)
    - [font-weight](#font-weight)
    - [font-size](#font-size)
    - [font-style](#font-style)
  - [border](#border)
    - [border-color](#border-color)
    - [border-width](#border-width)
    - [border-style](#border-style)
    - [border-radius](#border-radius)
  - [list-style](#list-style)
    - [list-style-type](#list-style-type)
    - [list-style-position](#list-style-position)
  - [padding](#padding)
    - [padding-top](#padding-top)
    - [padding-bottom](#padding-bottom)
    - [padding-left](#padding-left)
    - [padding-right](#padding-right)
  - [margin](#margin)
    - [margin-top](#margin-top)
    - [margin-bottom](#margin-bottom)
    - [margin-left](#margin-left)
    - [margin-right](#margin-right)
  - [Altre proprietà](#altre-proprietà)
    - [color](#color)
    - [width](#width)
    - [height](#height)
    - [display](#display)
    - [visibility](#visibility)
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
Per dare un valore a queste proprietà si utilizzano i due punti `:`; Il valore in sé può essere di vari [tipi](#tipi-di-valori).

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

Una proprietà, in CSS, può prendere più di un valore. In questo caso, i vari valori vanno separati da uno spazio.

```css
.highlight {
    border: 2px solid white;
}
```

Qui la proprietà `border` prende tre valori: `2px` per lo spessore, `solid` per lo stile e `white` per il colore.

[^4]: Non sono elencati tutti i tipi di valori

## Foglio a cascata

CSS è un foglio di stile a cascata, questo significa che qualsiasi proprietà di un elemento è determinata dall'ultimo valore dato. Un file CSS è letto dall'alto verso il basso, quindi se all'interno c'è questo codice:

```css
body {
    background-color: red;
}

body {
    background-color: blue;
}
```

il colore di sfondo di `body` sarà blù, visto che `background-color: red` è *sovrascritto* da `background-color: blue`.

## Il Box Model di CSS

![css box model](https://extelos.com/assets/images/blog/boxmodel.gif)

Il Box Model indica lo spazio che è occupato da un elemento:

- *Content* indica il contenuto dell'elemento
- *Padding* indica lo spazio tra il contenuto e il bordo
- *Border* indica lo spessore del bordo
- *Margin* indica dello spazio aggiuntivo occupato dall'elemento

## Lista delle proprietà

### background

Tutte le proprietà che iniziano con `background-` hanno a che fare con lo sfondo

#### background-color

Imposta il colore di sfondo di un elemento.

Valori accettati:
- nomi di colori
- colori rgb e rgba
- colori hsl e hsla
- colori esadecimali

#### background-image

Imposta l'immagine di sfondo.

Valori accettati:
- link tramite la funzione `url`

#### background-size

Imposta la dimensione dell'immagine di sfondo.

Valori accettati:
- la larghezza dell'immagine, mantiene le proporzioni
- un secondo valore opzionale che indica l'altezza e non rispetta le proporzioni

```css
body {
    background-image: url("image.jpg");
    background-size: 20em;
}

div {
    background-image: url("image.jpg");
    /* l'immagine è lunga il doppio dell'altezza */
    background-size: 20em 10em;
}
```

#### background-repeat

Imposta il criterio di ripetizione dell'immagine.

Valori accettati:
- `repeat`, valore di default, ripete l'immagine in entrambi gli assi
- `repeat-x` ripete l'immagine sull'asse orizzontale
- `repeat-y` ripete l'immagine sull'asse verticale
- `no-repeat` non ripete l'immagine

#### background-attachment

Imposta il criterio di scorrimento dell'immagine.

Valori accettati:
- `scroll`, valore di default, l'immagine scorre con gli elementi della pagina
- `fixed` l'immagine non scorre

### text

Varie proprietà per modificare il testo.

#### text-align
Imposta l'allineamento del testo.

Valori accettati:
- `left`, valore di default, allinea il testo a sinistra
- `right` allinea il testo a destra
- `center` allinea il testo al centro
- `justify` allinea il testo a sinistra, adattando la riga alla larghezza dell'elemento

#### text-decoration-line
Imposta la posizione della linea di decorazione.

Valori accettati:
- `underline` sottolineatura
- `overline` linea sopra
- `line-through` linea in mezzo (come il tag `<s>`)

Può accettare uno o due di questi valori.

#### text-decoration-style
Imposta lo stile della decorazione del testo.

Valori accettati:
- `solid`, valore di default, linea solida
- `wavy` linea ondulata
- `dottet` linea a puntini
- `dashed` linea tratteggiata
- `double` linea doppia

#### text-decoration-color
Imposta il colore della decorazione del testo.

Valori accettati:
- nomi di colori
- colori rgb e rgba
- colori hsl e hsla
- colori esadecimali

#### text-decoration-thickness
Imposta lo spessore della decorazione del testo.

Valori accettati:
- un numero che indica lo spessore

### font

Varie proprietà per modificare il font del testo.

#### font-family
Imposta la famiglia del font.

Valori accettati:
- `serif` font con le grazie
- `sans-serif` font senza grazie
- `monspace` font con caratteri della stessa larghezza
- il nome della famiglia tra virgolette

```css
#p1 {
    font-family: sans-serif;
}

#p2 {
    font-family: "Comic Sans MS";
}
```

#### font-weight
Imposta il peso del font ("nerezza").

Valori accettati:
- `bold` grassetto/neretto
- un numero senza unità di misura da 100 a 900

#### font-size
Imposta la grandezza del font.

Valori accettati:
- `small` piccolo
- `smaller` più piccolo
- `large` grande
- `larger` più grande
- un numero con unità di misura che indica l'esatta altezza di ogni carattere

#### font-style
Imposta lo stile del font.

Valori accettati:
- `normal`, valore di default, testo normale
- `italic` testo corsivo

### border

Proprietà per personalizzare il bordo di un elemento.

#### border-color
Imposta il colore del bordo.

Valori accettati:
- nomi di colori
- colori rgb e rgba
- colori hsl e hsla
- colori esadecimali

#### border-width
Imposta lo spessore della decorazione del testo.

Valori accettati:
- un numero che indica lo spessore

#### border-style
Imposta lo stile della decorazione del testo.

Valori accettati:
- `solid` linea solida
- `dottet` linea a puntini
- `dashed` linea tratteggiata
- `double` linea doppia
- `inset` bordo in 3D verso l'interno
- `outset` bordo in 3D verso l'esterno

Questa proprietà accetta uno o quattro valori. Se si mette un singolo valore lo stesso stile è applicato a tutti i lati, se si mettono quattro valori lo stile è applicato in ordine al lato sopra, a destra, sotto, a destra.

#### border-radius
Imposta la smussatura degli angoli di un elemento.

Valori accettati:
- un numero con un'unità che indica il raggio

Questa proprietà accetta uno o quattro valori. Se si mette un singolo valore lo stesso stile è applicato a tutti gli angloi, se si mettono quattro valori lo stile è applicato in ordine all'angolo in alto a sinistra, in alto a destra, in basso a destra, in basso a sinistra.

### list-style

Proprietà che modificano lo stile di una lista.

#### list-style-type
Imposta il tipo di simbolo usato nella lista.

Valori accettati per \<ul\>:
- `disc` pallino pieno, default
- `circle` pallino vuoto
- `square` quadratino
- `none` nessuno

Valori accettati per \<ol\>:
- `decimal` numeri decimali
- `decimal-leading-zero` numeri decimali con uno zero davanti
- `lower-alpha` lettere minuscole
- `upper-alpha` lettere maiuscole
- `lower-greek` lettere greche minuscole
- `upper-greek` lettere greche maiuscole
- `lower-roman` numeri romani minuscoli
- `upper-roman` numeri romani maiuscoli

#### list-style-position
Imposta la posizione del simbolo della lista.

Valori accettati:
- `outside`, valore di default, il simbolo è al difuori dell'area della lista
- `inside` il simbolo è all'interno dell'area della lista

### padding
Imposta il padding di ogni lato.

Valori accettati:
- numero con unità di misura

#### padding-top
Imposta il padding del lato sopra.

Valori accettati:
- numero con unità di misura

#### padding-bottom
Imposta il padding del lato sotto.

Valori accettati:
- numero con unità di misura

#### padding-left
Imposta il padding del lato a sinistra.

Valori accettati:
- numero con unità di misura

#### padding-right
Imposta il padding del lato a destra.

Valori accettati:
- numero con unità di misura

### margin
Imposta il margin di ogni lato.

Valori accettati:
- numero con unità di misura

#### margin-top
Imposta il margin del lato sopra.

Valori accettati:
- numero con unità di misura

#### margin-bottom
Imposta il margin del lato sotto.

Valori accettati:
- numero con unità di misura

#### margin-left
Imposta il margin del lato a sinistra.

Valori accettati:
- numero con unità di misura

#### margin-right
Imposta il margin del lato a destra.

Valori accettati:
- numero con unità di misura

### Altre proprietà

#### color
Imposta il colore del contenuto di un elemento.

Valori accettati:
- nomi di colori
- colori rgb e rgba
- colori hsl e hsla
- colori esadecimali

#### width
Imposta la larghezza del contenuto di un elemento.

Valori accettati:
- numero con unità di misura

#### height
Imposta la larghezza del contenuto di un elemento.

Valori accettati:
- numero con unità di misura

#### display
Imposta il metodo di visualizzazione dell'elemento.

Valori accettati:
- `block` l'elemento occupa l'intera larghezza dello shermo
- `inline` l'elemento occula la larghezza minore possibile
- `none` l'elemento esiste all'interno della pagina ma non occupa spazio e non è visibile

#### visibility
Imposta la visibilità di un elemento.

Valori accettati:
- `visible` visiblie
- `hidden` nascosto

Un elemento nascoso è semplicemente non visibile, occupa comunque l'area che occupava quando era visibile
