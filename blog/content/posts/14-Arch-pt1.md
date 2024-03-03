+++
title = 'I use Arch (btw) - parte 1'
date = 2024-03-01T23:46:48+01:00
draft = false
+++


### Prologo

Autoconvincersi di avere la necessità di qualcosa è una mia specialità. Devo ammettere che non è da tutti trovare "scuse" per sentirsi bene con se stessi.

E' così che nascono la maggior parte dei _weekend project_ che mi tengono impegnato per mesi.

Questa storia comincia nell'attimo in cui mi sono detto "voglio imparare ad usare __linux__". Ma per davvero!

Come ho già scritto in altri [post](https://www.lolloandr.com/blog/posts/11---homelab-struggle-parte-2/) uso già una distribuzione di linux (in particolare Ubuntu server) nel mio homelab. Nonostante mi sappia muovere nella shell e fare operazioni elementari riconosco di non saper come __funziona__ veramente linux. Voglio poter sperimentare per davvero, capire le differenze tra i vari window manager, desktop enviroment, sperimentare con diverse distro, modificare il kernel...

Tutte cose che non mi sognerei mai di fare sul server che uso per  file, foto e applicazioni importati per me

### I need hardware

Il mio primo pensiero è stato: ok, ho già un computer, basta prendere una chiavetta, fleshare la iso eh... __no__

Il mio _daily driver_ è un __MackBook Pro M1__ che come molti di voi sapranno si basa su architettura ARM. ARM è super valida per il mio utilizzo di tutti i giorni ma sentivo che non sarebbe stata la migliore scelta in questo contesto.

Si presenta anche un secondo problema: è impossibile installare linux su mac. O almeno, __circa__. Negli ultimi tempi si è sentito molto parlare di [asahi linux](https://asahilinux.org/) un progetto fighissimo che porta linux su mac. Tuttavia non è tutto oro quello che luccica:
- asahi linux ha ancora un __supporto abbastanza limitato__ per le features del mac
- __non volevo effettuare un dual boot__ (unico modo per utilizzare asahi linux)
- ho pensato che sarebbe stato meglio "allenarsi" su una macchina che non sia la mia principale (in caso qualcosa andasse __storto__)

Quindi, la mia risposta impulsiva a questo problema è stata __aprire ebay__

Non è un segreto che gli utenti di linux amano i __thinkpad__. Ci sono una serie di motivi:
- il __supporto della comunità__ (a dir poco essenziale!) dei thinkpad è eccezionale
- sono computer solidi e __ben costruiti__
- __costano poco__ sul mercato dell'usato


Mi sono messo quindi ad osservare una serie di aste che avvenivano su ebay per dei thinkpad t460, t460s, t470 e t470s spediti dalla germania.

Ho adocchiato subito un thinkpad __t470s__ con __8GB__ di __ram__, __512GB__ di __SSD__ NVMe ed una CPU Intel __i5-7300U__ che era arrivato al prezzo 100€ . Dopo qualche puntata e qualche giorno sono riuscito ad aggiudicarmelo al costo di __115,99€__ spedizione inclusa... direi un buon affare

Qualche giorno dopo un pacco si presenta alla mia porta:

![Foto di circuito fatto a mano con sensore e D1 mini](/blog/thinkpad.png)

Il computer si presenta con windows 10 già installto (in tedesco) e qualche segno di usura, ma niente di eccessivo. 

Ovviamente ho subito fleshato una chiavetta usb con la ISO di __arch linux__ usando balena etcher (primo errore). Ed ho iniziato il processo di installazione... ma questo ve lo racconto nel prossimo post

Alla prossima!
