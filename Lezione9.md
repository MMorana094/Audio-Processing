#### MIDI
è un protocollo standard per far comunicare diversi device, permette di registrare performance musicali ed è caratterizzato da tre aspetti : 
- Protocollo, il linguaggio e le regole;
- Interfaccia, ovvero le componenti che servono a far comunicare i device;
- Estensioni dei file, che grazie a ciò contiene informazioni e strutture;

la qualità non dipende dall'estensione del file, ma dal modulo di sintesi ovvero il programma con cui si apre il file MIDI.

in un file MIDI abbiamo da 1 a 16 Canali che servono ad implementare il concetto di strumento, inoltre vi sono da 1 a n Tracce che implementano concetti di partiture e mixing permettendo una distinzione logica di contenuto, poi abbiamo da 1 a 128 patch che implementano il concetto di timbro, poi possiamo avere da 1 a n Banchi che permettono di incrementare il numero di patch, le correlazioni possono andare solo in una direzione, da dove vi è la possibilità di infinito a finito, esempio:

Tracce $\rightarrow$ Canali
Canali $\rightarrow$ Patch

ogni dispositivo MIDI è dotato di un clock per l'ordine dei messaggi, l'unità di base è il tick che possono essere anche chiamati Parti Per Quarto(il Quarto è un'unità relativa alla definizione di Quarto)(PPQ), questo è variabile e va da 24 a 4096 si utilizza un multiplo di 2 o un numero potenza di 2, il numero di Quarti in un minuto è variabile da 40 a 240 per minuto ed è indicato dai BPM.

Esempio:
Quanto dura 1 tick se abbiamo 120 BPM e 24 PPQ?
prima calcoliamo la durata di un beat.
$60/120 = 0,5s$
successivamente calcoliamo la durata di un tick.
$0,5 / 24 = 0.02 s$

la grandezza del PPQ è detta Division, più grande sarà maggiore sarà la risoluzione temporale possibile.

#### Messaggi
questo protocollo va avanti per messaggi, sono sequenze di 10 bit dove il primo e l'ultimo bit contengono informazioni sull'inizio e la fine del messaggio quindi in sostanza sono 8 bit di contenuto, il primo bit indica che tipo di messaggio mandare con valori (0, 1) :

1) se il bit contiene valore 1 sarà uno **Status Byte**, il messaggio di Stato può essere di due tipi per riconoscerli vengono usati 3 bit distinguendo quindi i messaggi in base al numero di bit in :
    - da [000 a 110] Messaggi di Canale ed indicano la produzione di una nota con un determinato strumento o cambio di timbro, ogni combinazione dei bit1, bit2, bit3 del nibble1 esclusa la combinazione 111 darà dei messaggi differenti con delle conseguenze differenti;
    - [111] Sono messaggi di Sistema e indicano operazioni come :
        - timing;
        - sincronizzazione;
        - Selezionare una traccia;
        - indicizzazione all'interno di una traccia;
        - Reset del device;
        - Connettere due device;
        - vengono usati dai costruttori per specificare informazioni sui prodotti;
2) se il bit contiene il valore 0 sarà un **Data Byte** ed utilizzerà i restanti 7 bit per la trasmissione dati.