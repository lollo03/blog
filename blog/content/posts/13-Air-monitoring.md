+++
title = "Monitoraggio qualità dell'aria on a budget"
date = 2024-02-23T16:16:31+01:00
draft = false
+++

L'aria è un qualcosa con cui interagiamo ogni giorno ma non ci facciamo caso. Nelle nostre case creiamo veri e propri microclimi e se passiamo tanto tempo in una stanza può essere utile misurare la qualità dell'aria per capire quando è necessario arieggiare.

Nell'articolo di oggi voglio proporvi due soluzioni economiche per controllare questi parametri ed imparare qualcosa di nuovo.

## IKEA VINDRIKTNING

![foto sensore](https://www.ikea.com/it/it/images/products/vindriktning-sensore-della-qualita-dellaria__1073150_ph177967_s5.jpg?f=l)

> Fonte foto: Sito IKEA

Sappiamo tutti quanto può essere divertente (ed a volte anche conveniente economicamente!) modificare un prodotto già pronto per aggiungere funzionalità. Un esempio è quello dell'[IKEA VINDRIKTNING](https://www.ikea.com/it/it/p/vindriktning-sensore-della-qualita-dellaria-80515910/) un sensore di **PM 2.5** che possiamo comprare a 9,95 €

I [PM 2.5](https://it.wikipedia.org/wiki/PM_2.5) sono una famiglia di polveri sottili di dimensione minori o uguali ai 2,5 micron

Solo molto piccole, ma a lungo andare possono danneggiare la nostra salute. Queste polveri sono monitorare in tutte le città e vengono prodotte anche dalle automobili. Nella casa si possono accumulare in seguito all'utilizzo di oggetti come **saldatori**, **detersivi** e fumo (camini, vaporizzatori, cucina...)

Vi presento un piccolo esempio pratico:

![Grafico che mostra un piccolo nelle polvere sottili](/blog/pm25.png)

Cosa stavo facendo per far alzare così tanto il livello di PM25? Semplice, stavo usando un saldatore, **e con la finestra aperta!** Poter monitorare questi parametri mi permette di adattare le mie abitudini ed avere uno stile di vita più salutare.

### Hacking time

Il sensore IKEA VINDRIKTNING ci mostra lo stato delle polveri sottili tramite 3 led posti sulla parte anteriore del prodotto:



![Sensore dopo la modifica](/blog/sensore_1.jpeg)

> Sensore dopo la modifica

Tuttavia il sensore non è capace di loggare o condividere le sue misurazioni. Come ho fatto a rendere questo prodotto utile per i miei scopi?

Sul sito hackster.io è presente [un articolo](https://www.hackster.io/news/ikea-vindriktning-air-quality-sensor-mod-adds-sensors-and-indicators-aac85d80c7c9) che ci mostra come è possibile connettere un ESP8266 o simili e poter ottenere i dati dal sensore. Quindi, ho ordinato degli [esp8266 D1 Mini](https://www.az-delivery.de/it/products/d1-mini) e mi sono messo all'opera. Dopo un'operazione di circa 30 minuti sono riuscito a connettere il D1 mini al sensore ed ottenere i dati che volevo.

### Coding time

Dopo di che mi sono messo all'opera per scrivere del codice che è disponibile su questo [repository](https://github.com/lollo03/IKEA-VINDRIKTNING-mod-by-Lollo) github

Ho scritto il **firmware** per l'esp8266 che effettua una serie di misurazioni ed ogni minuto manda una **richiesta web** ad una API scritta in **node.js** che carica i dati su un database. Dopo di che usando [grafana](https://grafana.com/) (installato sul mio server) ho creato una **dashboard** che mi permetta di **visualizzare** i dati, et voilà il gioco è fatto.

![Dashboard su grafana](https://raw.githubusercontent.com/lollo03/IKEA-VINDRIKTNING-mod-by-Lollo/main/docs/grafanaDashboard.png)

Il sensore funziona bene e per una spesa che non supera i 15 € direi che è un buon affare.

## Espandere gli orizzonti

Tuttavia mi sono reso conto di voler misurare un'altra serie di parametri come la **temperatura**, **umidità**, **[TVOC](https://www.aircare.it/inquinanti-indoor-tvoc/)** (Composti organici volatili totali) ed [**eCO2**](https://www.careforair.eu/en/eco2/) (valore della CO2 calcolata tramite la concentrazione di TVOC)

Per misurare questi parametri ho trovato il sensore che faceva a caso mio:
**ENS160 + AHT21** che si trova a pochi euro su [aliexpress](https://it.aliexpress.com/item/1005004685403045.html?gatewayAdapt=glo2ita) o siti simili. Una volta ordinato il sensore ho preso un altro D1 mini e mi sono messo al lavoro, ottenendo però un risultato meno raffinato rispetto alla modifica del sensore ikea

![Foto di circuito fatto a mano con sensore e D1 mini](/blog/sensore_2.jpeg)

Ho scritto un firmware anche per questo secondo sensore, modificato l'api e la dashboard ed ho ottenuto questo risultato:

![Dashboard grafana](/blog/dashboard_aria_finita.png)

Come si può notare sono presenti molti più parametri che mostrano un quadro molto più completo della situazione.

Da un sensore da 5 euro non ci possiamo aspettare precisione assoluta, ma per il costo e l'uso hobbistico direi che è _good enough_

## Soluzioni commerciali

Un sensore connesso con capacità simili è l'[amazon Smart Air Quality Monito](https://www.amazon.it/amazon-smart-air-quality-monitor-conosci-la-qualita-dell%E2%80%99aria/dp/B08X2V3T2B?) che al momento viene venduto al prezzo di 80 euro

Il sensore misura gli stessi parametri dei due sensori che vi ho mostrato ma ad un prezzo superiore.

Non posso dire con certezza se le informazioni sono più accurate rispetto alla soluzione DIY (sospetto utilizzino gli stessi sensori) ma sicuramente rappresenta un'alternativa per chi non vuole sporcarsi le mani.

## Passi futuri

In futuro proverò a combinare entrambi i sensori facendoli entrare nella scocca dell'ikea VINDRIKTNING per renderli più puliti.

Inoltre, aggiornerò l'api per inviarmi delle notifiche quando la qualità scende al di sotto di una certa qualità.

Se vuoi rimanere aggiornato ti invito a seguirmi su github e mettere un _watch_ al [repository](https://github.com/lollo03/IKEA-VINDRIKTNING-mod-by-Lollo) per non perderti aggiornamenti.


## Update 

Ho "fuso" insieme i due sensori ottenendo questo risultato:

![Sensore dopo la modifica](/blog/sensore_1.jpeg)

Non male, vero?
