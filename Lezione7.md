#### Audio
vi sono due tipi di Audio che studieremo :

- Audio Analogico :
    > è un segnale a tempo continuo e valori continui, ogni istante di tempo è campionato entro un certo range di valori. Le variazioni della curva del nostro segnale seguono l'andamento della curva dell'ampiezza dopo che viene convertita in segnale elettrico.

- Audio Digitale : 
    > è un segnale a tempo discreto e valori discreti, la sua rappresentazione non cerca di imitare la curva di un segnale analogico, ma la costruisce da zero assegnando di volta in volta il valore dell'ampiezza in istanti di tempo successivi.

**come possiamo ottenere l'audio analogico?**
tramite un trasduttore le onde di pressione vengono trasformate in onde elettriche per poi essere registrate su un supporto.

**come possiamo riprodurre un audio analogico?**
bisogna interpretare le variazioni delle grandezze fisiche presenti sul supporto, per esempio in un audio cassetta si interpretano le variazioni dell'intensità dei campi magnetici.

**Cosa avviene durante la catena di produzione-riproduzione di un audio analogico**

inizialmente descriveremo la catena di registrazione di un audio analogico dove il trasduttore registra la variazione di pressione e la trasforma in segnale elettrico, una volta finita la trasformazione si applica una pre-amplificazione utile a migliorare il suono o aumentare il volume di segnali troppo bassi, successivamente viene applicata la fase di amplificazione vera e propria, queste 2 fasi vengono applicate per regolare il livello del segnale in maniera da prevenire altre distorsioni, infine avviene la registrazione su supporto.
Successivamente vi è una lettura delle variazioni delle grandezze fisiche del supporto, questa porta del segnale sonoro che viene prima pre-amplificato e poi amplificato per migliorarne la qualità per poi essere infine riprodotto dai diffusori.

nel momento che abbiamo un audio analogico potremmo avere delle distorsioni, ovvero del rumore che nella versione originale non vi è, il rapporto **segnale-rumore** viene definito come :
$$SNR = \frac {S}{N}$$
dove :
S = ampiezza massima del segnale originale.
N = ampiezza massima della distorsione introdotta.

possiamo descrivere l'SNR, **Signal to Noise Ratio**, tramite il dB e possiamo rappresentarlo come segue:

$$SNR = 10 \log_{10}\frac {S^2}{N^2} = 20  \log_{10}\frac{S}{N}$$

maggiore sarà questo indice, meglio è.

##### Pro e Contro del Segnale Analogico
Pro : possiamo rappresentare più facilmente le frequenze, ci vuole poco per costruire un apparecchiatura per riprodurre l'audio ed ha un campionamento migliore.

Contro : introduzioni di distorsioni fisiche, vi è un degradamento del supporto che può quindi rovinare il segnale ancora di più e la rappresentazione dipende dal tipo di supporto che usiamo.

#### Audio Digitale
l'audio digitale non cerca di imitare la forma d'onda analogica, ma assegna dei valori discretizzati che rappresentano l'andamento della forma d'onda.

**come possiamo ottenere un audio digitale?**
le onde di pressioei vengono catturate e convertite in onde elettriche da un trasduttore, successivamente vengono mandate ad un ADC ed infine si sceglie il formato e la memoria di massa archiviandolo.

**come posso riprodurre un audio digitale?**
il file memorizzato viene interpretato partendo dalla sua estensione, successivamente mandiamo il segnale di output ad un DAC, che produce un segnale elettrico, questo segnale fa vibrare la cassa e quindi noi ascolteremo l'output.

un dispositivo che utilizza sia ADC che DAC viene chiamato **Data AcQuisition** ovvero DAQ ed è utilizzato sia per acquisire che riprodurre audio digitali.

**Catena di Registrazione-Riproduzione Audio digitali**

tramite un trasduttore andremo a catturare le onde di pressione e le trasformeremo in segnale elettrico, successivamente queste passando da un filtro passa-basso vengono inviate ad un ADC che le tratterà con campionamento, quantizzazione e codifica, una volta finito avremo il nostro audio digitale che dovrà essere conservato su un qualsiasi supporto digitale, per la riproduzione tramite il nostro file viene decodificato da un DAC che tramite un filtro passa-basso manda il segnale elettrico al diffusore che inizierà a vibrare facendo sentire l'audio.

#### Conversione Analogico-Digitale
visto che ormai i device esistenti trattano segnali digitali, è necessario convertire il segnale analogico per tanto dovremmo trasformare un segnale a tempo continuo e valori continui in uno a tempo discreto e valori discreti questo avviene tramite due processi :
- Campionamento;
- Quantizzazione;

##### Campionamento
per trasformare un segnale a tempo continuo in uno a tempo discreto si fa uso del teorema di Nyquist-Shannon per il campionamento che afferma per ricostruire fedelmente un segnale è necessario che la frequenza di campionamento sia maggiore al doppio della frequenza presente nello spettro. La frequenza di campionamento consigliata è di 44.100 perchè tramite la soglia di udibilità fissiamo che la frequenza massima sarà di 20.000 Hz che tanto oltre non sentiamo, si prendono 44.100 campioni perchè qualsiasi cosa introduce distorsioni e quindi per evitare problemi prendiamo circa il 20% in più del nyquist-rate.

##### Quantizzazione
Abbiamo diversi tipi di quantizzazione e sono :

- Quantizzazione Uniforme o Lineare:
> ad intervalli uguali di ampiezza corrisponde un numero uguale di livelli di quantizzazione. in questo tipo di quantizzazione possiamo apprezzare un errore massimo $E_{max}$ pari a :

$$E_{max} = \frac{VFS}{2Q}$$

> dove Q è il numero di livelli di ampiezza e VFS il Valore a Fondo Scala

per calcolare il rumore introdotto dalla quantizzazione si utilizza l'SQNR(Signal to Quantization Noise Ratio), sapendo che N sono i livelli di bit di quantizzazione viene raffigurato così:

$$SQNR = 2^N* \sqrt{\frac{3}{2}}$$
in dB avremo :
$$SQNR = 10 \log_{10}(SQNR)$$

- Quantizzazione NON Uniforme o non lineare:
> ad intervalli uguali di ampiezza corrispondono diversi livelli di quantizzazione.

- Quantizzazione a Fondo Scala
> è la dimensione massima del range che si vuole rappresentare, si calcola con :

$$VFS = V_{max} - V_{min}$$

ora che conosciamo tutte le grandezze che caratterizzano un segnale possiamo andare a capire quanti bit servono per rappresentare un segnale audio? questa quantità viene calcolata come segue : 
$$Size = F_c * N * D * C$$
dove :
$F_c = Sampling Rate$
N = Profondità in Bit
D = Durata del Flusso Dati
C = Numero di Canali
il numero di bit nel tempo, misurato in bps è dato dalla formula :
$$bitrate = F_c * N * C$$ 

#### Codifica PCM (Pulse Code Modulation)

> Bisogna considerare ogni campione come un impulso, a questo impulso andiamo ad associare una codeword binaria che rappresenta l'ampiezza del suono, la lunghezza di questa codeword dipende dai bit di quantizzazione usati.

#### Compressione

Cosa è la compressione?

> è la rappresentazione di una informazione con un numero minore di bit, calcolato tramite opportune strategie.

questo viene fatto per ridurre la memoria occupata, ridurre il tempo di esecuzione, di avvio.

Come comprimere?
> Riduciamo la ridondanza nella codifica;
Riduciamo la ridondanza Spaziale/Temporale;
Riduciamo le informazioni irrilevanti(Es. tagliamo le alte e basse frequenze sotto o sopra la soglia di udibilità);

#### Metodo Naivè (Compressione del silenzio)
è una compressione Lossy basata sulla riduzione di informazioni irrilevanti.

#### Codifica DPCM e ADPCM

> DPCM (Differential Pulse Code Modulation): è un algoritmo di compressione Lossless, codifica i valori in PCM, si va a codificare la differenza tra il valore attuale e quello successivo
> ADPCM (Adaptive Differential Pulse Code Modulation): è un algoritmo di compressione Lossy che migliora la codifica DPCM adattando dinamicamente la dimensione del passo di quantizzazione. Si va a predire il valore del campione attuale tramite il valore predetto precedente, trasmettendo però solo gli errori di predizione, in caso di ambiguità si utilizza scegliere quello più alto, utilizza un approccio di quantizzazione per adattarsi alle differenze.

#### Codifica A-Law $\mu$-Law
Sono due algoritmi di ccodifica definiti dallo standard G.711, servono a codificare la voce al telefono quindi utilizza frequenze comprese tra 0 4Khz

##### $\mu$-Law
viene usata in Nord-America e Giappone, grazie ad una quantizzazione non lineare a 8 bit possiamo ottenere una qualità equivalente ad una quantizzazione lineare a 14bit.

$$Y = sign(X)\frac{\ln(1+\mu|X|)}{\ln(1 + \mu)}$$

X = valore originale di ampiezza normalizzato tra [-1, 1]
$\mu$ = 255 = ($2^8$ - 1)

per valore di x tendenti a 0 ci saranno più bit dedicati, invece per valori che si avvicinano agli estremi ci saranno meno bit.
Es.
X = 0.75
$$Y = +\frac{\ln(1+(0.75*255))}{\ln(1 + 255)} = 0.948 = 0.95$$

da questo esempio possiamo notare che da 0.75 a 1 ci sono 0.25 valori che vengono compressi in realtà a 0.05 valori.

per ottenere valori di Y a 8 bit con segno compreso tra [-128, 127] partendo da x compreso [-32768, 32767] si usano le seguenti formule di normalizzazione : 
$$X = \frac{x + 32768}{32767}-1$$ $$y = round(Y *127.5)$$
Es.
x = 10.000
$$X = \frac{10.000 + 32768}{32767}-1 = 0.305$$
$$Y = + \frac{\ln(1+(0.305*255))}{\ln(1 + 255)} = 0.787$$
$$y = round(0.787 *127.5) = 100 $$

##### Decodifica $\mu$-Law
per decodificare il segnale in codifica $\mu$-Law si utilizza la seguente formula :
$$X = sign(Y) \frac{e^{\ln(1+\mu)|Y|-1}}{\mu}$$

#### Codifica A-Law

è una codifica che viene usata in europa, usa una quantizzazione non lineare a 8 bit per avere la stessa qualità di una quantizzazione lineare a 13 bit.

$$Y = sign(X)\begin{cases} \frac{A|X|}{1+\ln A} \text{ per valori di |X|} \leq \frac{1}{A}\\
                            \frac{1+\ln A|X|}{1 + \ln A} \text{ |X| è compreso tra } \frac{1}{A} \text{ e } 1\end{cases}$$

la normalizzazione avviene come nel caso di $\mu$-Law.

#### Decodifica $\mu$-Law

$$Y = sign(X)\begin{cases} \frac{|Y|(1+\ln A)}{A} \text{ per valori di |X|} \leq \frac{1}{1+\ln A}\\
                            \frac{e^{|Y|(1+\ln A)-1}}{A} \text{ |X| è compreso tra } \frac{1}{1 + \ln A} \text{ e } 1\end{cases}$$

#### Quantizzazione a Virgola Mobile
fa uso della quantizzazione lineare vengono aggiunti dei bit extra che servono a shiftare il valore per codificarlo in virgola mobile, questa quantizzazione non è lineare.

Es.
se il bit extra è 0 codifico la parola a 8 bit con uno 0 a sinistra.
se il bit extra è 1 codifico la parola a 8 bit con uno 0 a destra.

considero ora 2 range differenti :
- range A [-V/2, +V/2];
- range B [-V, -V/2] U [V/2, V];

se il valore si trova nel range A quantizzo uniformemente aggiungendo il bit extra a 0;
se il valore si trova nel range B divido il valore per 2 aggiungendo il bit extra a 1;

Es.
V = 256;
2V = 512;
range dei valori da codificare = [-256, 255]

range A = [-128, 127]
range B = [-256, -128] U [128, 255]

codifico il valore 64 = ricade nel range A quindi codifico in binario = 01000000 e poi aggiungo il bit extra 0 a sinistra = 001000000

#### Fattori di Compressione per codifiche basate su PCM

dipendono da come è implementata la PCM : 

- su Windows abbiamo IMA ADPCM: con fattore 4 a 1;
- su MAC abbiamo ACE/MACE ADPCM: con fattore 2 a 1;

oltre a questo è l'utente che stabilisce cosa usare in base alle necessità scegliendo la fedeltà o la compressione.

#### Compressione Percettiva
Johnston ha fissato un limite teorico alla comprimibilità di un segnale audio se si vuole tenere una codifica trasparente, il limite è 2.1 bit per campione.
Abbiamo diversi tipi di compressioni percettive e sono :

- Compassion;
- Quantizzazione $\mu$-law e A-Law;
- Codifica Differenziale ADPCM;
- Codifica a Blocchi;
- Codifica per Sotto-Banda;
- Codifica per Trasformata;
- Codifica di HUFFMAN;

#### Compassion
questa compressione è di tipo percettivo e prende il nome dalla contrattura delle parole Compression + Expansion, è pensata per risolvere i problemi SNR sui Nastri Magnetici, andiamo a comprimere in fase di registrazione diminuendo le ampiezze massime per poi aumentare le ampiezze in fase di riproduzione, in questa maniera durante la compressione prima di memorizzare comprimo anche il rumore che poi non verrà espanso in fase di espansione perchè il rumore è legato al supporto.

#### Codifica a Blocchi
Questo tipo di codifica può essere applicata insieme alla Floating Point quantizzation, nella Floating Point abbiamo che più campioni hanno lo stesso bit extra, quindi tutti i campioni con lo stesso bit extra verranno accorpati in un blocco, durante la decodifica vi è la possibilità di creare dei pre-echi, questo avviene quando due blocchi hanno il bit extra molto diverso tra loro e quindi vi è una transizione brusca da un blocco all'altro, la soluzione sarebbe quelle di dividere in blocchi più piccoli o blocchi dinamici.

#### Codifica per Trasformata
Questa codifica viene applicata con blocchi che hanno una bassa gamma dinamica, a questi blocchi viene applicata una Trasformata in base a quello che serve, inoltre per evitare i pre-echi calcoliamo la trasformata su intervalli sovrapposti al 50%

#### Codifica per Sotto-Banda
suddividiamo lo spettro in sottobande e codifichiamole separatamente, in questo modo ogni sotto banda ha le sue proprietà e possiamo trattarle in maniera separata, in questa maniera possiamo andare a comprimere una determinata banda per avere l'effetto desiderato, la scelta delle bande da usare è personale dipende da ciò che dobbiamo fare, ma ovviamente ci sono delle linee guide, una idea valida è quella di usare la suddivisione per bande critiche, però non è facilmente implementabile.

#### Codifica di HUFFMAN
Questa codifica assegna codici di lunghezza maggiore a frequenze più basse, viceversa codici con lunghezza minore a frequenze più alte, inoltre una codeword di codifica non può essere prefisso di altre codeword.
per applicare questa codifica selezioniamo le frequenze più basse, creiamo un nodo fittizzio con la somma delle due frequenze ed a questo leghiamo come figlio destro e figlio sinistro le frequenze prese in considerazione prima, continuiamo così fino a riempire l'albero di riferimento.
N.B. per frequenza si intende la frequenza di un carattere ovvero le ripetizioni del carattere in base al totale dei caratteri.

#### Codifica psicoacustica
queste tipo di codifiche vanno ad usare delle proprietà percettive dell'essere umano a vantaggio della compressione, in sostanza andremo a togliare tutte quelle cose irrilevanti o comunque che non verrebbe sentite dall'orecchio umano.

Es.
sappiamo che l'essere umano sente in un range ben specifico di frequenze? andremo ad annullare tutti i suoni maggiori o minori della soglia di udibilità.

nello specifico useremo la seguente formula per approssimare alla soglia di udibilità inferiore:
$$T_q(f) = 3,64 (\frac{f}{1000})^{0.8} - 6,5e^{-0,6(\frac{f}{1000}-3.3)^{2}} + 10^{-3}(\frac{f}{1000})^4$$

se una volta usata la formula avremo un contributo energetico $T_q(f)$ minore di una certa frequenza allora $T_q(f)$ è sopprimibile.

un'altro metodo per applicare delle codifiche psicoacustiche è quello di applicare del mascheramento, per fare ciò dobbiamo ricordare che quando si applica la quantizzazione andremo ad aggiungere del rumore e quindi ad aumentare l'SNR, se il nostro tono supera la soglia di mascheramento del rumore allora verrà mascherato e quindi non sarà udibile. Dobbiamo inoltre ricordare che l'SNR, ovvero la distanza tra l'ampiezza del tono mascheratore e la minima soglia di mascheramento può essere espresso in forma logaritmica come segue:
$$SMR = \log(segnale) - \log(rumore)$$
oltre l'SNR è cosa importante l'NMR ovvero il rapporto rumore maschera che è la distanza tra la distorsione introdotta quantizzando a m-bit e la soglia minima di mascheramento ed è espresso in questa maniera :
$$NMR = \log(gamma) - \log(rumore)$$ sapendo ciò possiamo ricavare l'SNR facendo la somma di SMR ed NMR :$$SNR = SMR + NMR$$

#### Codifiche per Modelli(LPC)
sono codifiche che si basano sulla costruzione di modelli matematici, alla fine si rappresenterà il comportamento della sorgente simulata, una codifica di questo tipo è la **codifica LPC** che memorizza la differenza tra il valore predetto dal modello e quello reale.