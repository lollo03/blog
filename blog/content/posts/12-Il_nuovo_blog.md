+++
title = 'Il nuovo blog, hugo e static site generation'
date = 2024-02-23T14:40:06+01:00
draft = false
+++

Come potete vedere qua ci sono stati dei cambiamenti, la parte di blog sul mio [portfolio](https://www.lolloandr.com/) è stata sostituita da questo nuovo sito. Ma come è stato fatto?

Quando si pensa a creare un sito web nella nostra mente iniziano a comparire parole come **database, wordpress, server, hosting**. Sono tutte cose di cui bisogna preoccuparsi prima di poter pensare di creare un nuovo sito. Ma tutto questo è realmente necessario?

## Semplificare è meglio

Prendiamo l'esempio di un blog o di un portfolio. É veramente necessario avere un database? É veramente necessario avere una complessa installazione di wordpress con mille plugin per avere delle funzionalità base? É veramente necessario avere una vps o un container che esegue del codice php o node.js ogni volta che qualcuno vuole vedere una pagina web?

_In my opinion_ no, nel 90% dei casi in cui vogliamo mostrare del contenuto **statico** (o che cambia poco di frequente) tutto questo è superfluo.

La forma più essenziale di sito web è quella rappresentata da una serie di file che vivono su un web server, se modifichiamo questi file, si modifica il sito.

Ovviamente modificare file html e css "a mano" può risultare tedioso, ma per fortuna ci sono tool chiamati **static site generator** che ci possono aiutare.

## Vantaggi di un sito web statico

I vantaggi di un sito web statico si possono riassumere in alcuni importanti punti:

- **facilità:** come presto vedremo sono necessari non più di 15 minuti per configurare il sito, hosting e scrivere il nostro primo articolo!
- **SEO:** ai motori di ricerca piacciono i contenuti statici, non è una novità
- **velocità:** il rendering di un sito generato (che alla fine della fiera si tratta di una serie di file html e CSS) è molto più veloce di un sito dinamico

Tuttavia è arrivato il momento di affrontare il grande difetto di questa tecnologia: **la mancanza di interattività con l'utente**

Su un sito web statico possiamo dimenticarci di funzionalità come commenti e **pagine generate ad hoc** per ogni singolo utente. Tuttavia, è bene considerare l'utilità di questi strumenti per progetti come portfolio o piccoli blog. Come spesso avviene non esiste una soluzione che è necessariamente migliore di un'altra, ma ci sono vantaggi e svantaggi e la decisione deve essere ponderata e pensata.

Fatta questa doverosa premessa, entriamo nel dettaglio

## Hugo

![Logo Hugo](https://gohugo.io/images/hugo-logo-wide.svg)

Un esempio di ssg FOSS (free and open source) è [HUGO](https://gohugo.io/), un tool velocissimo scritto in GO che ci permette di creare un blog o un sito in pochi minuti.

Una volta creato il nostro sito tramite la cli di hugo troveremo una serie di cartelle organizzate con all'interno vari file. Tuttavia a noi interessa solo il file di configurazione, la cartella `content` e la cartella `assets`

### Temi e configurazione

Hugo è accompagnato da una moltitudine di [**temi**](https://themes.gohugo.io/) che si installano in qualsiasi progetto con due comandi dal terminale. (se siete curiosi il tema che ho usato per questo sito è [PaperMode](https://github.com/adityatelange/hugo-PaperMod))

Molti temi possono essere **personalizzati** a piacimento modificando il file di configurazione `hugo.yaml`. In questo file possiamo sia definire parametri propri del tema, sia configurare il nostro sito in generale. Per esempio possiamo aggiungere degli elementi al menù o cambiare la lingua:

```yaml
baseURL: "https://lolloandr.com/blog"
languageCode: "it-IT"
title: "Lorenzo Andreasi"
theme: "PaperMod"
sectionPagesMenu: main
menus:
  main:
    - name: Portfolio
      params:
        rel: external
      url: https://www.lolloandr.com/
      weight: 30
    - name: Yathzee
      params:
        rel: external
      url: https://www.lolloandr.com/Yathzee-board/
      weight: 30
```

### Articoli

Creare un articolo è un gioco da ragazzi, basta aprire il terminale nella cartella di hugo e scrivere `hugo new content posts/nomearticolo.md`

Ogni articolo è un file **markdown** preceduto da un piccolo blocco di configurazione dove possiamo specificare alcune. Gli articoli possono essere arricchiti con foto, blocchi di codice, matematica e virtualmente qualsiasi cosa che possa essere scritta in html. Compresi gli **iframe** e **javascript**

<iframe width="560" height="315" src="https://www.youtube.com/embed/jNQXAC9IVRw?si=sr996lEuBh054Iuw" title="YouTube video player" frameborder="0" allow="accelerometer; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

Ora attuale ricavata tramite javascript: <span id="demo"></span>

<script>
setInterval(function(){
  let date = new Date();
  document.getElementById("demo").innerHTML = `${date.getHours()}:${date.getMinutes()}:${date.getSeconds()}`;
}, 1000);
</script>

<h4 class=wow>WOW!</h4>
<style>
    .wow{
        animation: changeColor 1s infinite alternate;
    }
    @keyframes changeColor {
    from {
        color: red;
    }
    to {
        color: #00B1D7;
    }
}
</style>

### Live reloading

Un'altra fantastica caratteristica di hugo è quella di avviare un web server da linea di comando e vedere come appariranno i nostri articoli sul nostro blog. Basta effettuare il comando `hugo server -D` per avere una versione interattiva del sito e vedere i nostri cambiamenti in tempo reale.

### Generare il sito

Quando avremo finito di personalizzare il sito web e scrivere gli articoli basterà eseguire il comando `hugo` e come per magia nella cartella `public` troveremo una serie di file pronti per essere messi su un web server ed essere visibili ai nostri visitatori.

Quando il sito viene generato, hugo si preoccupa anche di creare una **sitemap** e un **feed RSS** che può essere usato (ad esempio) anche nel [README](https://github.com/lollo03/lollo03) di un profilo github!

## Hosting di siti web statici

Per hostare il nostro sito abbiamo diverse opzioni. Possiamo utilizzare un hosting tradizione caricando i file tramite **ftp**

Ma un'opzione con dei significativi vantaggi e **gratuita** è quella di usare le github pages.

Sul sito web di hugo è disponibile una [guida](https://gohugo.io/hosting-and-deployment/hosting-on-github/) su come configurare la github action e le github pages per generare il sito web ed hostarlo. Ogni volta che pusheremo il nostro sito su github automaticamente verrà pubblicato.

Questo sito è hostato in questo modo, [qua](https://github.com/lollo03/blog) potete vedere il repository.

Grazie per aver letto questo articolo, ti ricordo di seguirmi su [github](https://github.com/lollo03), [instagram](https://www.instagram.com/lolloandr/) e sul mio canale [telegram](https://t.me/lorenzoandreasi). Alla prossima!
