#### Trattamento dell'Audio Digitale
trattare un campione audio digitale è più semplice rispetto ad uno analogico, questo perchè non dobbiamo preoccuparci di distorsioni non volute, inoltre in questo trattamente stiamo andando ad modificare l'energia di partenza associata al campione, in questi trattamenti le operazioni possono essere sia locali che puntuali, per semplicità viene normalizzata la traccia in un range [-1, 1] in questa maniera avremo i valori massimi e minimi in 1 e -1 e il silenzio in 0.
un'altra fase del trattamento di una traccia audio è quella di dividere la traccia in frame, solitamente la quantità di questi frame è presa scegliendo un numero potenza di 2, 512,1024 sono degli esempi, una volta scelta la quantità di frame N, conoscendo la frequenza di campionamento $f_c$ possiamo ricavarne la loro durata T:

$$T = \frac{N}{F_c}$$

$N = \text{quantità di frame}$
$F_c = \text{Frequenza di Campionamento}$

una volta definita la dimensione del frame, possiamo definire la **Risoluzione in frequenza** R, ovvero la frequenza più piccola rappresentabile nello spettro, quest'ultimo ovvero lo spettro può essere ricavato applicando la Trasformata Discreta di Fourier al frame.

$$R = \frac{f_c}{N}$$

#### Ricampionamento
andiamo a modificare la frequenza di campionamento, in sovracampionamento o sottocampionamento, questo funzionamento è uguale allo scaling nelle immagini.

Sovracampionamento : 
> vado ad aumentare la frequenza di campionamento introducendo per interpolazione dei nuovi campioni.

Sottocampionamento :
> vado a diminuire la frequenza di campionamento con un filtro passa basso/alto/banda, andrò a perdere delle informazioni e se sottocampiono troppo possiamo introdurre dell'aliasing.

#### Riquantizzazione
Riquantizzare un segnale digitale vuol dire andare a normalizzare in maniera uniforme o non-uniforme in un determinato range, più piccolo dell'originale i valori per rappresentare l'audio.

#### Modifica del Numero di Canali
modificare il numero di canali, può migliorare l'esperienza spaziale dell'audio e vi sono 2 modi per modificare i canali : 

Aggiunta :
> andremo per esempio ad aggiungere un'altro strumento, il lavoro da fare dietro non è per niente semplice ma migliora l'esperienza audio, solitamente per aggiungere un canale si stima il suo comportamento in base alla posizione che dovrebbe avere rispetto agli altri canali.

Rimozione :
> andremo ad eliminare un canale, perdendo delle informazioni oppure potremmo sommare questo canale negli altri e poi eliminarlo in maniera da non perderlo, come si fa quando si trasforma un Audio Stereo in Mono

#### Modifica di Ampiezza
andando a modificare l'ampiezza andremo ad aumentare o diminuire il volume di ogni frame, per fare ciò basterà moltiplicare il vettore dei campioni per il Guadagno K ovvero la quantità di aumento o diminuizione del volume.

$$Y_i = K * X_i$$

$Y_i = \text{frame con ampiezza modificata}$
$K = Guadagno$
$X_i = \text{i-esimo frame del segnale digitale}$

se dopo questa modifica i valori vanno oltre il range di rappresentazione, vengono riportati al massimo o minimo valore rappresentabile, questo fenomeno è detto **clipping**.

#### Clipping
Questo fenomeno avviene se aumentando troppo i dorsi o i ventri del nostro segnale, questi superano la soglia di rappresentazione oppure potrebbe verificarsi anche se aumentiamo troppo il volume rispetto al valore massimo riportato sul diffusore in uso, per evitare ciò si massimizza il volume andando a trovare il guadagno più grande che non introduca clipping.

#### Maximize
Con questa operazione andremo ad aumentare il volume di ogni frame al massimo valore rappresentabile in modo da non introdurre il clipping.

$K_i = max(|X_i|)$
$Y_i = \frac{M}{K_i} * X_i$

$K_i = \text{Massimo valore che posso usare nella modifica del frame per non introdurre il clipping}$
$Y_i = \text{Frame con volume massimizzato}$
$M = \text{Massimo valore di ampiezza rappresentabile}$
$X_i = \text{Frame preso in considerazione del segnale audio}$

#### Minimize
Con questa operazione andremo a diminuire il volume di ogni frame al minimo valore rappresentabile in modo da non introdurre il clipping, con questa operazione portiamo alla soglia del silenzio quello che era il valore minimo di ampiezza di ogni frame.

$$K_i = min(|X_i|)$$
$$Y_i = sign(X_i)*(|X_i|-K_i)$$

$X_i = \text{i-esimo frame preso in considerazione}$
$K_i = \text{minimo valore utilizzabile per la modifica del frame}$
$Y_I = \text{frame con valore minimizzato}$


#### Fade In (Dissolvenza in ingresso)
è una funzione che fa variare l'inviluppo in un crescendo di ampiezza da un frame a ad un frame b di un valore da 0 a 1.

questa funzione ha delle proprietà ben precise : 
1) è monotona crescente;
2) f[0, N] $\rightarrow$ f[0, 1]
3) f(0) = 0; f(N) = 1;

è possibile scegliere tra diverse funzioni, alcune sono :

a. Lineare;
$$f(n) = \frac{n}{N}$$
b. Logaritmica;
$$f(n) = 10\log_{1+N}(1+n)$$
c. Esponenziale;
$$f(n) = \begin{cases} 0 \text{ } \text{n = 0}\\ \beta^{n-N} \text{ } \text{con $\beta$ > 1}\end{cases}$$

#### Fade Out (Dissolvenza in uscita)
è una funzione che fa variare l'inviluppo in un decrescendo di ampiezza da un frame a ad un frame b di un valore da 1 a 0, valgono le stesse funzioni e osservazioni del Fade In

#### Eco
per simulare l'eco prendiamo dei frame precedenti e li andiamo a sommare al frame interessato diminuendo l'ampiezza e quindi il volume.

sia **$\theta$** il frame risultante, **$\omega$** l'i-esimo frame di un segnale, **r** il numero di ripetizioni dell'eco, d un intero positivo che indica il ritardo in frame, **D** è un fattore di decadimento $0 < D \leq 1$ per pesare meno i frame più lontani andremo a calcolare l'eco in questa maniera : 
$$\theta = \omega + \sum_{j = 1}^{r}(D^j*\omega-(j*d))$$

solitamente il decadimento D è di ordine esponenziale.
per trovare l'eco dovremo sommare l'onda calcolata decaduta con l'onda originale.

#### Tremolo
è il variare dell'ampiezza in maniera sinusoidale attorno al valore originale, produce una sensazione di vibrazione.

sia **$\theta$** il frame risultante, **$\omega$** l'i-esimo frame di dimensione **K**, **$\alpha$**, **$\beta$** che sono dei fattori costanti, **$f_c$** è la frequenza di campionamento del segnale andremo a calcolare il tremolo in questa maniera :
$$\theta = \omega$$

#### Elaborazione del Range Dinamico
Sono elaborazioni che non lavorano per frame, ma sono puntuali quindi possiamo rappresentarle come LUT, ovvero una struttura che serve ad associare un valore di input ad un valore di output, solitamente il valore viene espresso in dBFS(deciBel Relative to Full Scale) che permettono di rappresentare i valori di ampiezza di un segnale audio in funzione del massimo valore disponibile in codifica PCM senza tenere conto dei segni.
$$E_{dbfs} = 20\log_{10}\frac{|V_{PCM}|}{2^{n-1}}$$

IN    |   OUT    |
------|----------|
$x_1$ | $f(x_1)$ |
$x_2$ | $f(x_2)$ |

per il valore 0, per convenzione si usa il valore **0,5** perchè il logaritmo di 0 non si può fare, inoltre se vogliamo ritornare da dBMS a PCM dobbiamo tenere conto dei segni e quindi memorizzarli prima.


#### Operazione Limitatore

questa operazione pone un Clipping ovvero un tetto massimo all'energia e quindi alla sua rappresentazione, data una soglia T tutto quello che supera T viene riportato a T.

$$f(x) = \begin{cases} x \text{ }\text{ se il valore non supera la soglia rimane inalterato} \\ T \text{ } \text{se x supera la soglia viene riportato alla soglia T}\end{cases}$$

#### Operazione Noise Gate
questa operazione pone un tetto minimo all'energia e quindi alla sua rappresentazione, data una soglia T tutto quello sotto tale soglia viene posto al valore di non udibilità.

$$f(x) = \begin{cases} x \text{ }\text{ se il valore supera la soglia rimane inalterato} \\ min \text{ } \text{se x supera la soglia viene portato a 0}\end{cases}$$

#### Operazione Compressore
questa operazione ha due funzionamenti :
funzionamento upward :
> scelta una soglia le ampiezze sotto la soglia vengono amplificate
$$f(x) = \begin{cases} x \text{ } \text{ se x < T} \\ \frac{(x-T)}{R}+ T \text{ } \text{ se x $\leq$ T}\end{cases} $$

funzione downward :
> scelta una soglia le ampiezza sopra la soglia vengono ridotte.
$$f(x) = \begin{cases} \frac{(x-T)}{R}+ T \text{ } \text{se x < T} \\ x\end{cases}$$

#### Operazione Espansione
questa operazione ha due funzionamenti :
funzionamento upward :
> scelta una soglia le ampiezze sopra la soglia vengono amplificate
$$f(x) = \begin{cases} x \text{ } \text{ se x < T} \\ (x-T)*R + T \text{ } \text{ se x $\leq$ T}\end{cases} $$

funzione downward :
> scelta una soglia le ampiezza sotto la soglia vengono ridotte, se R tende a infinito si comporta come un Noise Gate.
$$f(x) = \begin{cases} (x-T)*R + T  \text{ } \text{se x < T} \\ x \text { } \text{se x $\geq$ T}\end{cases}$$

### Trasformata Discreta di Fourier
per trovare il vettore $X_j$ dei coefficienti associato ad $x_i$, 
$$X_j(u) = \frac{1}{\sqrt N} \sum_{j = 0}^{N-1}x_i(a)e^{-j2\pi\frac{ua}{N}}$$

se invece volessimo tornare ad $x_i$ conoscendo $X_j$ 
$$x_i(u) = \frac{1}{\sqrt N} \sum_{j = 0}^{N-1}X_J(a)e^{j2\pi\frac{ua}{N}}$$ 

### Filtraggio Temporale
possiamo applicare filtri di media, mediano, convoluzione ed altri filtri usati nell'elaborazione delle immagini.

### Filtraggio Frequenziale
tramite trasformata di fourier si passa al dominio delle frequenze e si applicano i filtri ideali, butterworth, gaussiano, etc visti in interazione.

per applicare un filtraggio nelle frequenze si seguono i seguenti passaggi.
**DFT $\rightarrow$ Filtraggio $\rightarrow$ IDFT**