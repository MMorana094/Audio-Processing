#### FFMPEG
è un progetto open-source costituito da librerie e programmi per la gestione dei file multimediali, l'acronimo significa **Fast Forward Moving Pictust Experts Group**

#### Formati Supportati
per scoprire i formati supportati da ffmpeg basterà scrivere da terminale, difronte ad ogni formato ci saranno due bit, che portano le seguenti informazioni : 
bit 1 = impostato come D = Demuxing supportato dal formato
bit 2 = impostato come E = Muxing supportato dal formato

> ffmpeg -formats

alcuni sono:

- 3gp
- MPEG
- MPEG4
- JPEG

#### Codec Usati
per scoprire che tipo di codec possono essere usati basterà scrivere da terminale 

> ffmpeg -codecs

i codec sono vengono accompagnati da una codeword di 6 bit, ogni bit equivale ad un tipo di codec.

......

bit 1 e 2 = servono a capire il primo se il deconding è supportato ed il secondo se l'encoding è supportato.
bit 3 = serve a capire che tipo di codec stiamo usando se Video(V), Audio(A), Sottotilo(S).
bit 4 = quando è impostato serve a sapere se il codec comprime le informazioni solo all'interno di ciascun frame.
bit 5 = serve a capire se il codec utilizza una compressione lossy.
bit 6 = serve a capire se il codec utilizza una compressione lossless.


Es.
il codec H263 è così raffigurato : 
DEV.L. H263

ciò vuol dire che in questo codec sono supportati l'encoding ed il decoding, è un codec video con una compressione lossy.

#### Metadati
pre scoprire i metadati di un file multimediale bisogna scrivere da terminale 

> ffmpeg -i "input"

#### Taglio
per tagliare un file multimediale e quindi dividerlo si utilizza la seguente stringa : 

> ffmpeg -ss "iniziodeltaglio" -t "finedeltaglio" -i "input" -c copy "output"

oppure

> ffmpeg -ss "iniziodeltaglio" -t "duratadeloutput" -i "input" "output"

#### Estrarre Audio
per estrarre la traccia audio di un file multimediale basterà usare il seguente comando : 

> ffmpeg -i "input" "output.mp3"

oppure se volessimo delle qualità differenti possiamo scrivere :

> ffmpeg -i "input" -vn -acodec libmp3lame -ar 44100 -b:a "qualità" "output.mp3"

dove in qualità andremo a mettere un valore tra **96, 48, 24**

#### Stream_loop
se volessimo scegliere di eseguire diverse volte uno stesso file multimediale dovremmo scrivere questo :

> ffmpeg -stream_loop "n" - i "input" -c copy "output"

con n che varia da -1(loop infinito) a n(numero arbitrario di volte che il file deve essere eseguito)

#### Concatenazione file Multimediali
se volessimo creare un file multimediale che è la concatenazione di più file multimediali basterà servirci di un file di testo da usare come lista per contenere i nomi dei file multimediale e del seguente comando da shell:

> ffmpeg -f concat -i "list.txt" output

#### Convertire due canali in uno
se per necessità volessimo convertire un multimedia stereo in mono dovremmo usare :

> ffmpeg -i "input" -ac 1 "output"

se invece volessimo isolare i due canali dovremmo usare : 

> ffmpeg -i "input" -af "pan=stereo|FL < c0" "output"
> ffmpeg -i "input" -af "pan=stereo|FR < c0" "output"

in questa maniera avremo un file **stereo** ma dove sentiremo un solo canale.

se volessimo passare da questi file stereo ma con un solo canale, ad un file direttamente mono dovremmo usare :

> ffmpeg -i "input" -filter_complex"[0:a]channelsplit=channel_layout=stereo[right] -map "[right] input.

> ffmpeg -i "input" -filter_complex"[0:a]channelsplit=channel_layout=stereo[left] -map "[left] input.

#### Spettrogramma
se volessimo avere uno spettrogramma di un file multimediale basterà usare :

> ffmpeg -i "input" -lavfi showspectrumpic=s=hd720 "output.jpg"

#### Velocizzare o Rallentare l'audio
se volessimo velocizzare o diminuire l'audio basterà usare :

> ffmpeg -i "input" -filter:a "atempo=valore" -vn output

con atempo con valore compreso [0.1. 2.0]