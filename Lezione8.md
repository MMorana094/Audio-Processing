### Argomenti trattati
- MPEG-1 ed i suoi layer
- accenni di MPEG-2-3-4-7-21-D
- altri formati audio
#### MPEG
è un gruppo che ha prodotto varie strategie per l'elaborazione audio/video, ha prodotto vari standard quali : 
- MPEG-1
- MPEG-2
- MPEG-3
- MPEG-4
- MPEG-7
- MPEG-21
- MPEG-D

##### MPEG-1
questo standard definisce tre livelli di compressione, ognuno col proprio decoder :
1) **Layer I**

Specifiche Tecniche Layer 1:
- Risoluzione FFT : 512
- Tassi di campionamento : 33/44.1/48 kHz
- Blocco di campionamento : 384 campioni
- Bitrate Massimo : 224 kbps.
- Bitrate Minimo : 32 kbps.
- 32 bande di frequenze uguali.
- 12 campioni per banda.


Specifiche Tecniche Compassion:
- quanto di tempo utilizzato 2dB;
- fattore di scala : 6 bit (ogni campione viene normalizzato rispetto al picco della propria banda);
- bit per rappresentare la classe di quantizzazione : 4 bit;
- lunghezza della codifica : [0-15] bit dipende dalla classe;


si usa un campionamento a 384 campioni, a questo andremo ad applicare tramite DCT un banco di filtri per rimuovere le ridondanze producendo così 32 bande uniformi, troppo grandi se comparate con le bande critiche a bassa frequenza e troppo piccole comparate con le bande critiche bassa frequenza, di frequenze formate da 12 campioni per banda, la grandezza e la durata della banda dipende dal tasso di campionamento usato e può essere : 
    
> - con un tasso di campionamento 33Khz avremo una grandezza di banda di 515,65Hz per banda ed una durata di essa di 11ms
> - con un tasso di campionamento 44.1Khz avremo una grandezza di banda di 689,0625Hz per banda ed una durata di essa di 8,7ms
> - con un tasso di campionamento 48Khz avremo una grandezza di banda di 750Hz per banda ed una durata di essa di 8ms

per ogni banda si applica la compressione compassion, usando quanti di tempo di 2dB, visto che si usano quanti da 2 dB avremo un range dinamico per l'aumento dei valori dei 12 blocchi considerando il massimo, e classi di quantizzazione(serve ad indicare la grandezza di ogni quanto, vi sono quindi 15 configurazioni dove cambia il numero di bit per banda, la classe 0 che indica il silenzio, mentre la classe 1111 non è usata) che vanno da 0 a 15 rappresentate in 4 bit, inoltre il fattore di scala viene riquantizzato a 6 bit in questa maniera regoliamo la quantizzazione in maniera tale da garantire una normalizzazione in base al picco della banda, per tanto ogni banda conterà un costo di 10 bit + la lunghezza dei campioni che è variabile.

2) **Layer II**

il layer II apporta qualche miglioramento rispetto alle specifiche tecniche del Layer I e sono :

- Risoluzione FFT : 512 $\rightarrow$ 1024
- Blocco di Campionamento : 384 $\rightarrow$ 1152
- Tassi di Campionamento : aggiunti 16/22.05/24 kHz
- Frequenze divise in 3 ragione :
    - frequenza bassa : 15 classi (4bit);
    - frequenza media : 7 classi (3bit);
    - frequenza bassa : 3 classi (2bit);

3) **Layer III**

viene utilizzata una trasformata del seno modificata che ci permette di partizionare le bande in maniera da assomigliare alle bande critiche, si utilizza una quantizzazione non uniforme, vengono raggruppate bande con lo stesso fattore di scala e si utilizza una codifica di huffman con sincronizzazione per gestire la codifica a lunghezza variabile, tra blocchi differenti il bitrate è variabile.

#### MPEG-2
in questo formato si ha un bitrate di 6 Mbps e può gestire l'audio 5.1 quindi gestisce più di due canali.

#### MPEG-3
è stato integrato in MPEG-2 perchè non introduce innovazioni significative, ma migliorie tecniche per le tv HD.

#### MPEG-4
è un formato molto in uso ed usa oggetti separati.

#### MPEG-7
introduce l'innovazione di correlare i file di metadati per la gestione dei dati in rete, viene quindi associato un file XML ai file multimediali, dalla fusione di MPEG-7 e MPEG-4 prende vita MPEG-47 che unisce la codifica di MPEG4 alle regole di descrizione di MPEG-7

#### MPEG-21
non viene modificata la codifica, ma vengono aggiunte regole per i DRM.

#### MPEG-D
aggiunge codifiche specifiche per il parlato, codifiche per il surround e l'audio spaziale.

tutte le versione di MPEG hanno retrocompatibilità tra loro.

#### Altri formati Audio

- MPEG-AAC è un codec incluso in MPEG4 utilizza un BitRate comparabile a 192 kbps in MP3 e supporta fino a 48 canali.
- Dolby AC-3, introduce una compressione percettiva su MPEG-AAC.
- Flac è una compressione lossless (circa 50%)
- WMA è un formato audio proprietario di Windows ed ha una resa migliore sulla musica ma peggiore sulle voci