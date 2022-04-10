---
title: Guida CSS
sidebar:
  nav: "docs"
---

CSS è un acronimo che sta per **C**ascading **S**tyle **S**heet, foglio di stile a cascata. È utilizzato per formattare il codice HTML mantenendo leggibile la struttura della pagina.

## Storia

Nel 1993 alcuni browser web iniziarono a presentare tag proprietari, come `<font>`, che funzionavano solo al loro interno. Questo portò i programmatori a farne molto uso per poter cambiare lo stile della pagina web ma portò anche a molti problemi:

- I tag dei file HTML sono molto più lunghi a causa dei molti attributi, questo li rendeva più pesanti in termini di memoria e rallentava (oggi non sarebbe più un problema) il loro trasferimento e la loro lettura
- Il codice diventava spesso molto difficile da leggere ed era molto confuso perché non aveva degli standard.
- Molti browser non supportavano tutti i tag o tutti gli attributi che erano presenti in altri browser (oggi il problema esiste ancora ma è più limitato)

Per questi e altri problemi, il W3C (**W**orld **W**ide **W**eb **C**onsortium) presentò nel 1996 le specifiche del CSS 1. Queste separavano la formattazione dalla struttura e davano uno standard che i browser potessero seguire.
