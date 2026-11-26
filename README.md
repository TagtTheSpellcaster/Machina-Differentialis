# Machina Differentialis

![Versione](https://img.shields.io/badge/brevetto%20meccanico-1.6.3-b08a45)
![Licenza](https://img.shields.io/badge/licenza-AGPL--3.0-blue)
![Formato](https://img.shields.io/badge/formato-HTML%20singolo-lightgrey)

Machina N° 010 della serie **OFFICINA DEGLI ENIGMI**. Gioco didattico in un unico file HTML, ispirato alla Macchina Differenziale di Charles Babbage: una macchina che calcola e stampa tavole di polinomi usando soltanto addizioni.

[Puoi usarlo qui](https://tagtthespellcaster.github.io/Machina-Differentialis/)

## Contenuto

- **Esercizi**: 14 esercizi numerati più il «Calcolo libero». Dodici (1–11 e 14) chiedono di scrivere i numeri iniziali nei registri perché la macchina stampi una tavola data (il testo precisa che le righe del nastro sono i risultati per x = 0, 1, …, e che x è il numero a sinistra di ogni riga); il 12 e il 13 («Errata corrige») chiedono di trovare e correggere un errore in una tavola stampata guardando le differenze. Il «Calcolo libero» non ha scopo (da 2 a 6 registri, menu di esempi).
- **Soluzione**: il pulsante SOLUZIONE (limita l'esercizio a 1 stella) apre una spiegazione a passi nello stesso formato del tutorial: tabella delle differenze, scelta dei numeri da scrivere, prova sulla macchina; per l'errata corrige, individuazione della riga e calcolo del valore giusto.
- **Tutorial**: nove schede con terminologia fissa (cifra = un anello, numero = 9 cifre, registro = una fila). Durante ogni somma il registro che riceve è evidenziato in oro e quello che dà in azzurro, con gli anelli coinvolti, e una riga di testo descrive l'operazione.
- **Manovella**: un clic avvia il giro; con il passo passo spento, un clic durante il moto ferma la macchina (come STOP: i registri tornano ai valori di inizio giro); con il passo passo acceso, un clic fa avanzare di un passo. STOP resta disponibile. Animata con 30 fotogrammi (uno ogni 12°, in senso orario, a partire dalla posizione in alto) estratti da `manovella.gif` fornita dall'autore; lo sfondo nero è reso trasparente all'elaborazione. I fotogrammi sono incorporati nel file come WebP.
- **Passo passo**: con l'interruttore PASSO PASSO attivo (accanto a STOP e AZZERA; nel tutorial lo è di default, tranne nei passi che usano GIRA ×10) la macchina si ferma dopo ogni passo e attende un clic, un tocco o la barra spaziatrice. L'attesa è segnalata sulla riga di testo (che non taglia più il testo: ha altezza minima 106 px su PC e 170 px su schermi stretti, con una riga riservata alla scritta «CLICCA PER CONTINUARE»), con un anello luminoso intorno alla manovella e con la scritta «▶ CLICCA». Vale per GIRA ×1, GIRA ×10, ESEGUI e per la manovella. L'interruttore ha effetto anche a macchina già in moto: acceso, la macchina si ferma al passo successivo; spento mentre è in attesa, riprende da sola. Su schermi larghi (almeno 1100 px) il tutorial e le soluzioni si dispongono su due colonne.
- **Stampante a nastro**: la carta esce da una fessura in un alloggiamento in ottone, in basso, e sale a ogni riga stampata (nessuna scritta «Nastro di stampa»). Altezza minima 300 px; con più registri il nastro si allunga fino all'altezza della pila dei cilindri. Il bordo inferiore della pila dei registri coincide sempre con quello del nastro (con 2–3 registri la pila scende). Se le righe non stanno tutte, si scorre il nastro con la rotella o trascinando con il mouse, senza barre di scorrimento; a ogni nuova riga il nastro torna in fondo.
- **AZZERA** riporta a 0 tutte le cifre di tutti i registri e svuota il nastro.
- **Anelli stile cryptex**: 9 cifre per registro, inizialmente tutte a 0. Si ruotano trascinando in alto o in basso, toccando la cifra piccola sopra (−1) o sotto (+1), o con la rotella del mouse. In alternativa, campi numerici (accettano i negativi).
- **Suoni meccanici** sintetizzati con Web Audio, senza colonna sonora e senza rumore continuo: scatto (un anello avanza; anche quando l'utente ruota un anello), ding acuto da campanello di macchina da scrivere (riporto, al massimo uno ogni 70 ms), colpo sordo grave con tonfo (valore stampato sul nastro), campana (esercizio risolto), ronzio (risultato errato). Il collegamento fra due registri (evidenziatori oro e azzurro) non produce alcun suono. Legenda sotto i comandi audio. Interruttore SUONO ON/OFF e volume logaritmico (da −50 a 0 dB).
- **Velocità**: un giro dura sempre lo stesso tempo, qualunque sia il numero di registri, quindi la manovella ha velocità angolare costante (misurata: 3,6 rad/s negli esercizi 1 e 9 alla stessa impostazione). Con più registri le singole operazioni sono quindi più rapide. Il quadrante non ha scritte né indicazioni numeriche: la velocità si legge solo dalla lancetta. La velocità è scelta dall'utente con il volano e il manometro posti sotto i registri (trascinare il volano o la lancetta, oppure frecce da tastiera). Il volano non gira in continuo: la sua posizione dipende solo dalla velocità scelta. La scelta è salvata in `localStorage`. Il pannello, con il titolo «REGOLATORE VELOCITÀ MANOVELLA» (sopra il volano, a sinistra), ha il lato destro allineato con quello del telaio dei cilindri, è allineato in basso con la manovella e alto quanto la sua escursione (la manopola resta sempre dentro il pannello; la scritta «MANOVELLA» è stata tolta); con 4–6 registri l'area di disegno si allunga per lasciare spazio.
- Stelle per ogni esercizio (3 meno i suggerimenti usati, minimo 1) salvate in `localStorage`.

## Come funziona

Registro 0 = valore della tavola; registri 1..n = differenze in avanti; l'ultimo è costante. A ogni giro ogni registro somma quello sotto di sé (valori vecchi, dall'alto in basso) e il valore del registro 0 viene stampato. Gli anelli sono 9 per registro; i numeri negativi sono in complemento a 10^9 (−3 = 999999997). I riporti sono trasmessi dopo l'addizione, anello per anello.

## Uso

Aprire `macchina-differentialis.html` in un browser moderno. Nessuna dipendenza, nessuna rete.

## Verifiche

Verificato con test automatici:
- Riga di descrizione delle operazioni a 360 e 390 px di larghezza (emulazione Chromium) e a 1400 px: nessun testo tagliato né sovrapposto alla scritta «CLICCA PER CONTINUARE» durante un'esecuzione guidata dell'esercizio 1 e un calcolo libero con riporti; altezza costante (170 px su stretto, 106 px su largo).
- Velocità angolare della manovella misurata durante un giro negli esercizi 1 (2 registri) e 9 (5 registri): 3,60 e 3,65 rad/s (prima della 1.6.3: 7,9 e 1,3).
- Le evidenziazioni oro/azzurro sono disegnate dopo tutte le file, quindi il bordo inferiore non è più coperto dalla fila sotto (controllato con uno screenshot dell'esercizio 9).
- 20000 addizioni casuali e casi limite del modello ruota per ruota coincidono con l'aritmetica modulare.
- Per ogni esercizio con macchina, la soluzione calcolata dalle differenze produce l'intera tavola richiesta (inclusi i valori oltre quelli mostrati); per le due errata l'errore è visibile nell'ordine di differenza previsto.
- In Chromium (Playwright): clic sulla manovella ferma il moto; passo passo acceso a metà giro produce l'attesa; spento in attesa riprende; il volano compare sotto i registri con 3, 4 e 6 registri senza errori di script.
- In Chromium (Playwright) i 14 esercizi risultano risolti, e per ciascuno la soluzione guidata porta alla tavola corretta (con 1 stella al massimo), digitando i valori nei campi numerici; trascinamento, tocco e rotella sugli anelli, tutorial, esercizio libero e persistenza funzionano; nessun errore di script.

Non verificato:
- Ascolto effettivo dei suoni (compreso il nuovo campanellino) e loro equilibrio.
- Durata reale di un giro alle varie velocità del volano (non misurata) e comodità della scala.
- Sovrapposizione fra scritta VELOCITÀ e lancetta del manometro a fondo scala sinistro (visibile in uno screenshot, lieve).
- Il trascinamento degli anelli con il dito (il canvas blocca lo scorrimento della pagina) e l'aspetto della manovella su schermi reali.
- Il movimento della manovella è a scatti, a 30 posizioni per giro, senza interpolazione.
- Il layout a due colonne su schermi diversi da 1400×900 (provato solo a quella dimensione e a 1000 px di larghezza).
- La comprensibilità delle nuove spiegazioni: non provata da nessun lettore esterno.
- Tocco su dispositivi reali, Safari e Firefox.
- Equilibrio della difficoltà dei livelli.
- Dettagli storici sull'ordine delle operazioni e sui riporti della macchina originale: la simulazione è una semplificazione e non li riproduce. Fatti confermati: progetto iniziato nel 1821, progetto del 1830 con 16 cifre e 6 ordini, modulo dimostrativo del 1832 (circa un settimo, circa 2000 parti), costruttore Clement.
- Il nome è provvisorio.

## Licenza

GNU Affero General Public License v3.0 (AGPL-3.0). Licenza assunta, da confermare.

---
OFFICINA DEGLI ENIGMI · Machina N° 010 — BREVETTO MECCANICO 1.6.3 – 1894
