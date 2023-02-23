# 📖 get_next_line
 Che si tratti di un file, di uno standard input o prossimamente di una connessione di rete, avremo sempre bisogno di un modo per leggere il contenuto di un file riga per riga.

#### È ora di iniziare a lavorare su questa funzione essenziale per i progetti futuri.

<!-- TOC -->
* [💡 Introduzione](#-introduzione)
* [🔍 Variabili statiche](#-variabili-statiche)
* [📝 Esecuzione](#-esecuzione)
* [🛠️ Testing](#-testing)
<!-- TOC -->

------------

## 💡 Introduzione

**get_next_line** ci consentirà di approfondire le funzioni *open*, *read* e *close*, le variabili statiche e i file-descriptor.

>get_next_line ritorna una linea letta da un file descriptor.


Verrà prototipata come segue:

    int get_next_line(int fd, char **line);


## 🔍 Variabili statiche

> Una variabile statica viene dichiarata all'interno di una funzione ed è visibile solo a tale funzione.

Le **[variabili statiche](https://en.wikipedia.org/wiki/Static_variable)** sono utili quando si desidera tenere traccia del numero di volte in cui una funzione viene eseguita,
chiamata o quando si desidera tenere traccia di una variabile tra una chiamata e l'altra.

____________

## 📝 Esecuzione

Per eseguire il programma andremo ad utilizzare delle funzione già note come 
**strlen**, **strchr** e **strjoin**, che serviranno rispettivamente per misurare,
distinguere e concatenare le nostre linee di testo.

| Funzione    | Descrizione                                                  |
|:------------|:-------------------------------------------------------------|
| **strlen**  | data una stringa di n caratteri ritorna n                    |
| **strchr**  | individuerà il nostro carattere "\n" tra una linea e l'altra |
| **strjoin** | concatenerà le nostre linee di testo in un unica matrice     |


## ⏭️ ft_get_next_line

    Ogni volta che la funzione viene eseguita, controlla se c'è una nuova riga nella variabile statica. 
    In caso contrario, viene eseguita una nuova lettura, aumentando la dimensione della variabile statica. 
    Quando viene trovata una linea di testo, viene restituita e la variabile statica rimuove quella riga restringendosi. 
    Se non viene trovata alcuna nuova riga, il programma si riavvia, in maniera ricorsiva, consentendoci quindi 
    di leggere il testo disponibile nel file descriptor, una riga alla volta, fino alla fine del file.


| Funzione             | Descrizione |
|:---------------------|:------------|
| **ft_get_line**      |             |
| **ft_new_line**      |             |
| **ft_get_next_line** |             |
| **get_next_line**    |             |


____________


## 🛠️ Testing


Compileremo il codice come segue:

    gcc -Wall -Wextra -Werror -D 
    BUFFER_SIZE=42 
    get_next_line.c 
    get_next_line_utils.c 
    get_next_line.h main.c 
    -o test_gnl



Testando diversi valori per BUFFER_SIZE.
