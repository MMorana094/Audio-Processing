#### Caratteristiche delle onde

Le onde sono formate da diverse grandezze fisiche e sono : 

1) Ampiezza
> è la differenza che c'è tra un picco di massimo e un picco di minimo, aumentando o diminuendo questa alzeremo o abbasseremo il volume.
2) Frequenza
> è il numero di oscillazione al secondo, si misura in Hz e modificandola renderemo la traccia più acuta o grave
3) Periodo
> è il reciproco della frequenza, si misura in $\frac{1}{f}$
4) Spettro
> è il timbro o armonia del suono e mostra l'insieme delle frequenze elementari con i relativi contributi che formano l'onda complessa, può essere rappresentato tramite un grafico frequenza-ampiezza o un semplice grafico delle frequenze.
5) pulsazione
> è il numero di oscillazione completo in un tempo 2$\pi$, si misura in radianti ed è definito come: $$\omega = \frac{2\pi}{T} = 2\pi f$$
6) velocità d'onda
> è la velocità di propagazione di un'onda in un mezzo qualsiasi, dipende dal mezzo.
7) lunghezza d'onda
> è la distanza percorsa dall'onda nel tempo di un periodo, necessaria a passare da un punto di massimo al corrispondente punto di minimo, viene misrata in metri ed è definita come $$\lambda = vT = \frac{v}{f}$$ dove v è la velocità d'onda, f la frequenza
8) fase
> da informazioni sulla posizione dell'onda nel suo ciclo, possiamo interpretarla come la spazializzazione del suono, per esempio se prendiamo due suoni con la stessa fase sentiremo un aumento di volume, se invece prendiamo due suoni in opposizione di fase sentiremo il silenzio.
9) fase iniziale
> è il periodo trascorso dall'inizio.

le onde periodiche possono essere descritte come :
$$f(t) = f (t+kT) \text{ per K $\exists $ R} $$
in particolare noi studieremo le onde sinusoidali che possono essere descritte come : 
$$y(t) = A \sin(2\pi ft + \phi_0)$$
con A che sarà uguale all'ampiezza dell'onda, f la frequenza e $\phi_0$ la fase iniziale, inoltre sappiamo che il contenuto della parentesi ($2\pi ft + \phi_0$) è uguale alla fase

---

Esempio:
Data la seguente onda sinusoidale : 
$$y(t) = 10 sin(4\pi t + 4)$$
1) quanto vale la sua ampiezza? 10
2) quanto vale la sua frequenza? 2
3) quanto vale la sua fase iniziale? 4

---

ora che abbiamo parlato delle grandezze fisiche delle onda, possiamo entrare nel dettaglio andando a parlare del **Principio di sovrapposizione delle onde** che afferma :
> se due o più onde della stessa natura vengono sovrapposte allora la loro perturbazione finale sarà pari alla somma algebrica delle loro oscillazioni

questo principio è basato sugli studi della fase delle onde e dobbiamo definire due onde :
**Onde in fase** = sono quelle onde che hanno la stessa frequenza e raggiungono l'ampiezza massima nello stesso istante di tempo.
**Onde in Opposizione di fase** = sono quelle onde che hanno la stessa frequenza e la stessa ampiezza, ma la loro fase ha una differenza di 180°

Parlando di Onde periodiche dobbiamo parlare anche dell'analisi armonica di Fourier che afferma :
> Qualunque funzione periodica, sotto opportune condizioni matematiche può essere rappresentata come somma di onde sinusoidali di opportuna ampiezza e di frequenza fondamentale multipla della fondamentale di riferimento.

Tramite la serie di Fourier possiamo scomporre una somma di onde periodiche sinusoidale nei suoi termini elementari seguendo questa formula :
$$y(t) = \frac{a_0}{2} + \sum_{n = 1}^{+ \inf} (a_n \cos(n\frac{2\pi}{T}t) + b_n \sin (n\frac{2\pi}{T}t))$$

sapendo che $\frac{2\pi}{t}$ è la nostra pulsazione andiamo a sostituire questo con $\omega$ 

$$y(t) = \frac{a_0}{2} + \sum_{n = 1}^{+ \inf} (a_n \cos(n\omega t) + b_n \sin (n\omega t))$$

la serie che abbiamo appena visto può essere anche espressa in versione esponenziale come segue :

$$y(t) = \sum_{n = -\inf}^{\inf} (C_{n}e^{i\omega nt})$$

il coefficiente $C_n$ è così definito :

$$ C_n = \frac{1}{T} \int_{-\frac{T}{2}}^{\frac{T}{2}}(y(t) e^{-i\omega n T})dt$$

$a_n \cos(n\omega t) + b_n \sin (n\omega t)$ = n-esima armonica
$a_n, b_n$ = coefficienti dell'ennesima armonica ottenuti in questa maniera :

$$a_n = 2T\int_{-\frac{T}{2}}^{\frac{T}{2}}y(t)\cos(n\omega t) dt$$

$$b_n = 2T\int_{-\frac{T}{2}}^{\frac{T}{2}}y(t)\sin(n\omega t) dt$$

$$a_0 = \frac{2}{T} \int_{-\frac{T}{2}}^{\frac{T}{2}} y(t) dt$$

da notare che in questa maniera l'armonica ottenuta per n = 1 sarà l'armonica fondamentale ed ha frequenza pari a quella dell'onda.

Dimostrazione:

$$y(t) = A \sin (\omega t + \phi_0) \rightarrow a \cos(\omega t) + b \sin(\omega t) \rightarrow $$
$$ A \sin(\omega t + \phi_0) \rightarrow $$

applichiamo la formula di addizione del seno
$$ A \sin \omega t \cos \phi_0 + A \cos \omega t \sin \phi_0$$

ora poniamo :
$A \cos \phi_0$ = b 
$A \sin \phi_0$ = a

ed avremo $$a \cos(\omega t) + b \sin(\omega t)$$
possiamo dunque affermare:
$$A_n \sin(n\omega t + \phi_n) = A_n \cos n \omega t + b_n \sin n \omega t$$

dove 

$$A_n = \sqrt{(a_{n}^{2} + b_{n}^{2})}$$

$$\phi_n = \tan^{-1}(\frac{a_n}{b_n})$$

per le onde non periodiche, andremo a utilizzare la trasformata di Fourier nella seguente maniera :

$$y(t) = \int_{-\inf}^{+\inf}c(f)e^{i\omega t} dt$$
con
$$c(f) = \int_{-\inf}^{+\inf}y(t)e^{-i\omega t} dt$$

come esempi di spettro possiamo dire che per un onda sinusoidale avremo un grafico composto dalla sola frequenza dell'unica sinusoide che costituisce l'onda.

N.B. per onde triangolari, a dente di sega, quadra o raddrizzata serviranno infiniti termini per essere sintetizzata, quindi a livello digitale si utilizzano i primi termini per approssimare il resto.