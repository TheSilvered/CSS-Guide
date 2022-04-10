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

### Selettori

Esistono vari tipi di selettori ma verranno approfonditi solo i selettori semplici e i selettori di attributi.

I selettori semplici permettono di selezionare un elemento basandosi su nome, classe o id. Per selezionare un elemento per nome basta scrivere il nome del tag, esempio con un paragrafo:

```css
p {
    color: white;
}
```

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

[^2]: tutto quello tra `<!--` e `-->` è un commento di HTML ed è ignorato