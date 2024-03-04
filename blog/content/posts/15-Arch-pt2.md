+++
title = 'I use Arch (btw) - parte 2'
date = 2024-03-03T22:02:05+01:00
draft = false
+++

## L'inizio della fine

Come detto [precedentemente](https://www.lolloandr.com/blog/posts/14-arch-pt1/) ho deciso di installare [Arch Linux](https://archlinux.org/). I motivi che mi hanno spinto ad effettuare questa decisione sono:
- estrema possibilità di **personalizzazione**
- voglia di provare una distro che non avevo mai usato
- difficoltà del processo di installazione

Capisco che potreste essere confusi: che vantaggio c'è in una distribuzione difficile da installare? Semplice, che sei costretto a **capire cosa stai facendo**. Come detto nel precedente articolo questo viaggio è iniziato dalla mia voglia di imparare linux, quindi ho pensato che mettermi subito alla prova fosse la cosa più corretta!                     

Quindi, mi sono recato sul sito di arch linux, ho formattato una chiavetta usb e ci ho scritto sopra il file `.iso` usando il tool [dd](https://www.cyberciti.biz/faq/how-to-create-disk-image-on-mac-os-x-with-dd-command/)


Dopo di che ho accesso il ThinkPad e mi sono immediatamente diretto nelle impostazione del bios UEFI.

In questa schermata ho effettuato due operazioni:
- Disabilitare il **secure boot** (step necessario per permettere l'avvio da chiavetta USB)
- Cambiare l'ordine di boot inserendo per prima la pennetta USB preparata in precedenza

### L'installazione

Dopo un veloce riavvio mi sono trovato davanti ad uno schermo completamente nero con una shell. Arch linux può essere installato in due modi:
- Usando [archinstall](https://wiki.archlinux.org/title/archinstall) un simpatico script che dovrebbe **semplificare** il processo di installazione
- Facendo **tutto a mano**

Nello spirito di questo viaggio ovviamente ho scelto la seconda opzione. La prima cosa che ho fatto è stata guardami un [video su youtube](https://www.youtube.com/watch?v=68z11VAYMS8&t=1118s) per capire sommariamente a cosa andavo incontro. Dopo di che ho aperto la [guida di installazione](https://wiki.archlinux.org/title/installation_guide) sul sito ufficiale di arch linux e mi sono messo all'opera. La guida è veramente ben fatta, tuttavia sorvola alcuni passi importati che il video sottolineava.

Per installare arch ho impiegato circa 30 minuti. Ed il processo si può riassumere in questi punti:
- **connessione ad internet** collegando un cavo di rete o usando `iwctl`
- **partizionamento del disco e formattazione delle partizioni** usando tool come `cfdisk`, `mkfs` e `mkswap`. In questo step è importante pensare bene alle dimensioni delle varie partizioni
- **montaggio delle partizioni appena create** usando `mount`
- **installazione dei primi pacchetti** questo probabilmente è un punto critico, il comando `pacstrap -K /mnt` ci permette di installare pacchetti sulle partizioni appena montate. La guida ci indica come essenziali i pacchetti `base linux linux-firmware` delegando poi la scelta di altri pacchetti (a mio avviso essenziali) ad una serie di bullet point. I pacchetti aggiuntivi che ho installato sono stati `sof-firmware base-devel networkmanager vim man-db man-pages texinfo grub efibootmgr`
- creazione del file **fsab**
- **context swtich** tramite `arch-chroot /mnt`
- **altre impostazioni** come timezone, locale ed hostname.
- **installazione e configurazione di grub:** il boot loader installato in precedenza
- **creazione dell'utente:** è buona norma utilizzare il computer con un utente diverso da `root`

Dopo di che ho riavviato il pc e finalmente sono entrato nel nuovo sistema operativo

### Desktop environment

Una volta riavviato il computer mi sono ritrovato di nuovo di fronte ad una CLI. Fino ad ora non abbiamo installato nulla di grafico, è il momento di farlo.

Ho aperto la [pagina della wiki](https://wiki.archlinux.org/title/sway) di arch dedicata a [sway](https://swaywm.org/). Sway non è propriamente un Desktop environment, ma è (cito testualmente) _tiling Wayland compositor_

Nella pratica è molto più limitato rispetto ad un desktop environment, ma ha il vantaggio di essere estremamente **leggero** e senza distrazioni.

Quindi ho digitato nel terminale il comando `sudo pacman -S sway xorg-wayland kitty firefox wofi waybar nautilus`. Per installare, in ordine:
- sway
- xorg-wayland, layer di compatibilità per applicazioni che girano solo su [x11](https://it.wikipedia.org/wiki/X_Window_System)
- [kitty](https://sw.kovidgoyal.net/kitty/), emulatore di terminale
- firefox
- [wofi](https://man.archlinux.org/man/wofi.1.en), launcher di applicazione
- [waybar](https://github.com/Alexays/Waybar), status bar
- [nautilus](https://apps.gnome.org/Nautilus/), file manager

Dopo di che ho creato copiato il file di configurazione sample dalla directory `/etc/sway/config` alla `~/.config/sway/config` e dopo aver cambiato qualche parametro ho avviato sway.

Andremo più nei dettagli di come ho configurato sway ed altre funzioni come audio, led tastiera, networking e vpn in un altro articolo. Alla prossima!