---
title: Guida CSS
layout: single
---

CSS è un acronimo che sta per **C**ascading **S**tyle **S**heet, foglio di stile a cascata. È utilizzato per formattare il codice HTML mantenendo leggibile la struttura della pagina.

Indice:
- [Storia](#storia)
- [Collegamento con HTML](#collegamento-con-html)
- [Sintassi](#sintassi)

## Storia

Nel 1993 alcuni browser web iniziarono a presentare tag proprietari, come `<font>`, che funzionavano solo al loro interno. Questo portò i programmatori a farne molto uso per poter cambiare lo stile della pagina web ma portò anche a molti problemi:

- I tag dei file HTML sono molto più lunghi a causa dei molti attributi, questo li rendeva più pesanti in termini di memoria e rallentava (oggi non sarebbe più un problema) il loro trasferimento e la loro lettura
- Il codice diventava spesso molto difficile da leggere ed era molto confuso perché non aveva degli standard.
- Molti browser non supportavano tutti i tag o tutti gli attributi che erano presenti in altri browser (oggi il problema esiste ancora ma è più limitato)

Per questi e altri problemi, il W3C (**W**orld **W**ide **W**eb **C**onsortium) presentò nel 1996 le specifiche del CSS 1. Queste separavano la formattazione dalla struttura e davano uno standard che i browser potessero seguire.

## Collegamento con HTML

Il CSS è scritto principalmente in file secondari con l'estensione `.css`. Per collegare un file esterno in HTML si usa il tag `<link>` e CSS non fa differenza.
Basta inserire il tag all'interno di `<head>`, con `rel="stylesheet"` e `href="nome-del-file.css"`[^1] quindi il tag completo diventerebbe:

```html
<head>
    <title>Titolo della pagina</title>
    <link rel="stylesheet" href="nome-del-file.css" />
</head>
```

Questo però non è l'unico metodo per mettere CSS all'interno di HTML. Infatti, esso può essere scritto direttamente all'interno del file HTML, come contenuto del tag `<style>` all'interno di `<head>` o come valore dell'attributo `style`, presente in qualsiasi elemento. Nell'ultimo caso non si può specificare un [selettore](#selettori) diverso dall'elemento stesso.

[^1]: `nome-del-file` è sostituito con il nome effettivo del file.

## Sintassi

Il codice CSS ha una sintassi completamente diversa da quella di HTML. Esso è composto da selettori, che specificano l'elemento a cui applicare lo stile e da dichiarazioni che contengono le proprietà, l'equivalente degli attributi in HTML, e i loro valori.

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

I commenti in CSS si aprono con `/*` e si chiudono con `*/` e servono per rendere più chiare le intenzioni di quello che si sta facendo, essi possono occupare più righe e vengono completamente ignorati.[^2]

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
Si possono selezionare classi appartenenti ad un solo tipo di elemento mettendo il nome della classe davanti all'elemento *senza spazi*.

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
