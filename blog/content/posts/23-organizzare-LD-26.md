+++
title = 'Come (cercare) di organizzare un Linux Day'
date = 2026-10-25T16:44:38+01:00
draft = false
+++

Da due edizioni faccio parte del comitato che organizza il [Linux Day di Milano](https://linuxdaymilano.org/).

Tutto è iniziato nel 2025, quando, da vicepresidente del [POuL](https://poul.org/) (Politecnico Open unix Labs), uno degli esponenti di spicco di [ILS](https://www.ils.org/) (Italian Linux Society) ci ha lanciato una mezza provocazione dopo la conferenza di [Richard Stallman](https://poul.org/2025/05/richard-stallman-2025/): "Ma quand'è che portate il Linux Day al Politecnico?"

Da allora io, Dario e _Jep_ (che insieme formavamo il direttivo del POuL) ci siamo avviati su un terreno per noi inesplorato: organizzare, almeno per la parte logistica, un evento di quel calibro, con relatori, sponsor e banchetti di varie associazioni.

Il Linux Day (d'ora in poi **LD**) del 2025 è andato bene, ma ha evidenziato degli **errori** e delle **criticità** che sono poi state corrette nell'edizione del 2026. In questo articolo, vorrei mettere in evidenza questi errori e descrivere i **processi** che abbiamo implementato per evitarli, in modo che possano essere utili a chiunque voglia organizzare un evento del genere nella propria città.

## Il contesto

Il LD di Milano è organizzato da **POuL** e [**unixMiB**](https://www.unixmib.org/), il Linux User Group (LUG) dell'Università di Milano-Bicocca, con il patrocinio di **ILS**. Prima del 2025 si svolgeva in Bicocca, dove il POuL aveva un ruolo marginale, in quanto la logistica dell'evento veniva gestita principalmente da unixMiB.

Organizzare il LD al Politecnico significava, per il POuL, farsi carico di questa responsabilità logistica e burocratica (almeno per i rapporti con l'Università). Ci tengo ad evidenziare il ruolo **fondamentale** di unixMiB anche in questi ultimi due anni, in quanto LUG universitario di Milano-Bicocca e connessione diretta con ILS. Soprattutto, poter lavorare fianco a fianco con chi possiede il _know how_ permette di facilitare **notevolmente** il processo.

### Gli errori del 2025

L'edizione del 2025 è stata organizzata in pochi mesi. Questo ha portato a una scelta della location non ottimale. Nel 2025 il LD si è svolto nell'[edificio 3](https://www.polimi.it/il-politecnico/architetture-al-politecnico-di-milano/campus-leonardo). L'edificio rispettava tutti i requisiti: aule numerose e ampie, posizione facilmente accessibile, dimensioni adeguate. Tuttavia presentava anche un'enorme criticità: l'assenza di uno spazio al **chiuso** e **riscaldato** per posizionare i "banchetti" di associazioni e sponsor.

La critica più frequente che ci è stata rivolta nel 2025 è stata: "**fuori fa freddo**", specialmente a fine ottobre.

Inoltre, uno sfruttamento non ottimale delle risorse del Politecnico ci ha messo nella sgradevole situazione di dover gestire anche il trasporto di tavoli e attrezzature.

Abbiamo immediatamente compreso che per l'anno successivo era necessario un cambio di location. La scelta ovvia è ricaduta sul fiore all'occhiello del Politecnico: il [Trifoglio](https://www.polimi.it/il-politecnico/architetture-al-politecnico-di-milano/campus-bonardi/trifoglio).

### Organizzazione LD 2026

L'organizzazione per il 2026 è partita a inizio novembre 2025, quando abbiamo presentato al Politecnico un **bando** che prevedeva il finanziamento dell'apertura **straordinaria** del Trifoglio per il sabato dell'evento, un servizio di **sicurezza** (richiesto dal Politecnico) e un servizio di **facchinaggio**, così da avere i tavoli per i banchetti già pronti e risparmiare tempo prezioso.

Poiché l'evento era particolarmente grande rispetto al solito per il POuL, il processo è stato più complicato del previsto; tuttavia, anche grazie all'aiuto di alcune figure interne al Politecnico, siamo riusciti a presentare il bando.

Una volta **approvato** il bando, nel primo trimestre 2026, abbiamo avuto **conferma** che il LD si sarebbe svolto al Trifoglio.

Dopodiché è iniziata la parte relazionale e amministrativa (**sponsor**, **ILS** e **relatori**), gestita in **gran parte** da unixMiB, il tutto a partire da inizio settembre 2026.

Una volta ottenuta la lista di sponsor, talks e banchetti, abbiamo iniziato a pensare alla parte **logistica**:
- Pianificazione posizionamento banchetti
- Ottenere il materiale necessario (prolunghe, ciabatte)
- Coordinare i "turni dello staff" (ricordate! siamo tutti volontari, non si può "costringere" nessuno ad aiutare se non vuole)

Sembrava tutto pronto, finché il mercoledì prima dell'evento non abbiamo ricevuto una **bruttissima** notizia. Viste le mobilitazioni avvenute a Milano la settimana precedente, il Politecnico ci ha chiesto maggiori garanzie sulla **sicurezza** dell'evento. Al termine di un colloquio con l'Università siamo stati costretti a introdurre una misura mai vista prima a un Linux Day: l'obbligo di **registrarsi** per poter accedere all'evento.

Questa notizia ci ha messo nelle condizioni di doverci muovere velocemente: abbiamo scelto di utilizzare il software Open Source [pretix](https://pretix.eu/) installato sui server del POuL. Il software ha permesso a più di **390** persone di registrarsi all'evento in modo semplice, veloce e sicuro.

Un altro effetto di questa soluzione è che per la prima volta abbiamo potuto stimare con più precisione le presenze: a fronte di 390 iscrizioni, i partecipanti sono stati più di **300**. Non male per un evento che si è svolto in una giornata nella quale Milano era blindata per la paura di manifestazioni che avrebbero potuto degenerare.

Il LD, nonostante questa limitazione, si è svolto regolarmente e senza ulteriori complicazioni. In particolare, hanno funzionato bene il Trifoglio, il facchinaggio e pretix, mentre i walkie-talkie e tutti i volontari sono stati fondamentali.

## A cosa _non pensi_ quando organizzi il Linux Day?

La [legge di Murphy](https://it.wikipedia.org/wiki/Legge_di_Murphy) ci dice: _Se qualcosa può andare storto, lo farà_. Questo deve essere il mantra di chi organizza qualcosa del genere. È bene pensare ad **ogni possibile** complicazione e cercare di avere un piano per mitigarla.

La sera prima dell'evento, nella sede POuL, ci siamo chiesti: **cosa stiamo dimenticando?** Ed effettivamente dopo qualche minuto di brainstorming abbiamo pensato ad una serie di elementi utili e importanti:
- Moduli di **consenso** alla registrazione e alla pubblicazione dei talk, da far leggere e firmare ai relatori
- Cartelli, banalmente per **indicare** il WC o l'ingresso principale
- Un modo per **comunicare** tra noi in modo facile (la scelta è ricaduta su dei banali walkie-talkie: una soluzione **semplice** ma molto **efficace**)
- Organizzazione step-by-step dell'ora prima dell'apertura: **chi fa cosa e cosa deve fare**

Questi elementi, che possono sembrare banali, rischiano di essere **persi di vista** quando si pensa ad altre 100 cose insieme.

## Cosa migliorare nella prossima edizione?

Nonostante l'edizione del 2026 sia andata bene, credo ci siano ancora modi per rendere il processo più **snello e sicuro**.

Alcune delle cose a cui abbiamo pensato sono:
- **SCRIVERE, SCRIVERE, SCRIVERE**: trovare un modo per documentare ogni decisione, con il perché e il come, in modo che sia facilmente accessibile a chiunque sia coinvolto. Solitamente al POuL utilizziamo dei _pad_ [HedgeDoc](https://hedgedoc.org/) per tenere traccia delle decisioni, ma personalmente non ritengo questa modalità particolarmente efficiente.
- **Checklist**: credo che per minimizzare la possibilità di fare errori possa essere utile costruire delle vere e proprie checklist per **pianificare** ogni momento della giornata. È facile dimenticarsi cose scontate nella **frenesia** dell'evento.
- **Ridondanza**: cosa succede se un relatore non si presenta? che succede se c'è un incidente ed i volontari tardano ad arrivare? Penso sia bene pensare a dei **piani** di emergenza per queste eventualità.

Non sono idee nuove: sono ciò che si applica già nella gestione delle infrastrutture, concetti collaudati che possono essere adattati anche all'organizzazione di eventi.

## Ok, voglio organizzare anche io un Linux Day!

**Perfetto**, sono felice che tu sia entusiasta di questa idea. Il primo step è sicuramente leggere **accuratamente** la pagina "organizza" sul [sito dedicato](https://www.linuxday.it/) al LD.

Dopo di che, siediti e pensa a cosa vorresti ottenere. Prendi nota di tutte le tue idee e pensa a come realizzarle. Mi permetto di inserire una lista di alcune cose che potrebbero sembrare scontate ma potrebbero non esserlo.

- **Foto**: se vuoi fotografare l'evento, assicurati di ottenere il consenso **esplicito** di tutte le persone ritratte. **Attenzione**! Non sempre basta oscurare il volto: se la persona resta riconoscibile, serve comunque il consenso.
- **Registrazioni talk**: se vuoi registrare i talk, assicurati di trovare un sistema **facile** da usare ed **affidabile**. Spesso le università mettono a disposizione sistemi pensati apposta per le aule: **usali**.
- **Lascia dei tempi morti nella schedule**: una gran parte del LD è la possibilità di **conoscere** persone che condividono i tuoi interessi. Assicurati di lasciare del **tempo** che permetta ai tuoi ospiti di poter fare comunità.
- **Tratta bene i volontari**: una scorta di **bevande energetiche** o **snack** aiuta molto coloro che dedicano il proprio tempo gratuitamente al tuo evento.

E soprattutto, ricordati i **valori** che tutti noi teniamo a cuore: **condivisione e libertà**.

Se hai qualche domanda, o semplicemente vuoi farti una **chiacchierata**, sentiti **libero** di contattarmi col metodo che preferisci!

## Conclusione

Ci tengo a terminare questo mio pensiero **ringraziando** di cuore tutti coloro che partecipano al Linux Day! Che siano organizzatori, relatori, sponsor o visitatori. Siete voi che tenete viva la **community**.
