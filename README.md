# 📖 get_next_line

 Che si tratti di un file, di uno standard input o prossimamente di una connessione di rete, avremo sempre bisogno di un modo per leggere il contenuto di un file line by line.

#### È ora di iniziare a lavorare su questa funzione essenziale per i progetti futuri.

<!-- TOC -->
* [💡 Introduzione](#-introduzione)
* [🔍 Variabili statiche](#-variabili-statiche)
* [📝 Esecuzione](#-esecuzione)
* [🛠️ Testing](#-testing)
<!-- TOC -->

------------

## 💡 Introduzione

**get_next_line** ci consentirà di approfondire le funzioni *open*, *read* e *close*, le **variabili statiche** e i file-descriptor.

>get_next_line consiste nel codificare una funzione che restituisce una linea alla volta da un file di testo.

In questo progetto vedremo come i files vengono aperti letti e richiusi in un OS,
e come vengono interpretati da un linguaggio di programmazione per un ulteriore analisi.

Questo compito è fondamentale per un futuro programmatore poiché molto del tempo viene speso per la gestione dei dati e la loro [**persistenza**](https://en.wikipedia.org/wiki/Persistence_(computer_science).

la nostra funzione verrà prototipata come segue:

> int get_next_line(int fd, char **line);

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

 **get_next_line** inserirà in un puntatore ad una stringa la linea letta da un file descriptor. 
La funzione deve lavorare con qualsiasi lunghezza e con più descrittori di file contemporaneamente 
utilizzando solo su una variabile statica e nessuna variabile globali.

    La funzione utilizza una sola variabile statica per ricordare cosa è rimasto dall'ultima chiamata di read. 
    Questa memoria statica è un puntatore a un puntatore dove al primo livello sono presenti più slot di memoria. 
    Ciascuno di questi slot è unico per ogni descrittore di file, punterà a una stringa che leggerà il buff rimanente 
    dall'ultima chiamata (sempre se il descrittore di file è stato chiamato).
    La funzione controllerà se è rimasto un buffer passato ogni volta che viene chiamato e lo aggiungerà alla riga del risultato. 
    poi andrà a leggere il file vero e proprio concatenando quanto letto ad ogni ciclo alla riga del risultato.
    Quando incontra un buffer con una nuova riga, concatena alla riga del risultato solo il buffer fino alla nuova riga 
    e il nuovo buffer verrà aggiornato alla sotto-stringa dopo la nuova riga.

| Funzione             | Descrizione                                                                                                                                                                                                          |
|:---------------------|:---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **ft_get_line**      | Legge i dati dal file descriptor in blocchi di dimensione BUFFER_SIZE e concatena i dati letti con la linea precedente. Quando viene trovato il carattere newline, la funzione termina e restituisce la linea letta. |
| **ft_new_line**      | Crea una nuova stringa contenente i dati dopo il carattere newline. Questa funzione alloca dinamicamente la memoria per la nuova stringa e copia i dati dopo il carattere /n.                                        |
| **ft_get_next_line** | Questa funzione crea una nuova stringa contenente i dati fino al carattere /n. La funzione alloca dinamicamente la memoria per la nuova stringa e copia i dati dalla linea letta.                                    |
| **get_next_line**    | Coordina l'intero processo e restituisce la prima linea o quel che ne rimane                                                                                                                                         |

____________

## 🛠️ Testing

Una volta scritta una funzione main e datogli in pasto il nostro file .txt 
potremo andare a compilare il codice attraverso un makefile simile a questo:

    NAME = test_gnl

    SRCS = main.c get_next_line.c get_next_line_utilis.c  

    OBJS = $(SRCS:.c=.o)

    CC = gcc

    CFLAGS = -Wall -Wextra -Werror -D BUFFER_SIZE=42

    all: $(NAME)

    $(NAME): $(OBJS)
    $(CC) $(CFLAGS) $(OBJS) -o $(NAME)

    clean:
    rm -f $(OBJS)

    fclean: clean
    rm -f $(NAME)

    re: fclean all

    .PHONY: all clean fclean re


Testando diversi valori per BUFFER_SIZE e con diversi file di testo, potremo verificare che la funzione funzioni correttamente.

Potremmo anche utilizzare anche il tester di [Tripouille](https://github.com/Tripouille/gnlTester) che metterà a dura prova la nostra funzione.
