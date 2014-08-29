fx2048
======


*Pr2 Project 2014*

*Francesca Trudu* -
*Fulgheri Nadia Jolanda*

Modifica dell'implementazione del gioco 2048 in modo da permettere, opzionalmente, di giocare autonomamente con un giocatore automatico. 



Strumenti utilizzati:

git - distributed version control system


*Game2048.java*
classe contenente il main e il metodo start.
Implementa le funzioni e le variabili che si occupano di inizializzare e gestire l interfaccia grafica,
da qui viene inizializzato anche un oggetto di tipo GameManager che si occupa di tutte le funzioni di gestione del gioco: 
-i meccanismi di somma e spostamento delle caselle, 
-aggiornamento della griglia (a livello grafico), 
-aggiornamento dello score, 
-conclusione del gioco in caso di game over e vittoria del gioco.


Modifiche effettuate:
-aggiunta del package giocatoreAutomatico (e giocatoreAutomatico.player);
-aggiunta delle classi implementate dalle interfacce.

aggiunta di 3 variabili in GameManager -> boolean: gameOver e gameWon pubbliche e Griglia: myGriglia che viene aggiornata in base alla situazione del gioco


aggiunta di variabili , ascoltatore e Thread in Game2048 -> 
giocatoreAutomatico: viene creato un oggetto giocatoreAutomatico tramite il suo metodo; 
button per attivare il giocatore automatico e conseguente azione che crea un Thread permettendo di simulare la pressione del tasto H tramite un oggetto di tipo Robot, evento che viene catturato da un ascoltatore apposito addBtnClicked che implementa l'azione da eseguire: 
chiamata al metodo del giocatoreAutomatico prossimaMossa che restituisce un int random da 0 a 3, switch nel valore int con conseguente creazione di un valore Direction che viene passato al metodo move() del GameManager.
Game manager  si occupa di gestire tutto il procedimento del movimento di una casella, delle sue conseguenze, di inizializzare  myGriglia e di aggiornarla contemporaneamente a GameGrid.
Finchè non si ha il gameOver (e anche il gameWon) il Robot continua a premere H e ogni volta l'ascoltatore intercetta l evento permettendo l esecuzione del gioco in autonomia.

il processo principale è l'intefaccia grafica.
L'ascoltatore richiama il metodo prossima mossa.
L'oggetto giocatore automatico viene creato tramite il suo metodo button (per attivare il giocatore automatico), la pressione del tasto shift è creato tramite un oggetto di tipo robot, che va in un thread che viene mandato in esecuzione affianco all'interfaccia grafica.
Il meccanismo di simulazione di premere il tasto shift viene fatto in un altro processo (thread) rispetto al processo principale perchè cosi può lavorare in maniera simultanea rispetto all'interfaccia grafica<, infatti questo permette il suo funzionamento. Non sarebbe stata corretto in sostituzione l'utilizzo  di una for o una while perchè l'aggiornamento del processo secondario non sarebbe stato simultaneo a quello dell'interfaccia grafica e quindi il tutto non sarebbe stato corretto.

Il thread secondario serve per far gestire l'evento per premere il tasto shift riconoscerlo e richiamare alcuni metodi in un altro thread che è separato da quello principale.
I due processi lavorano in maniera affiancata o meglio parallela; il secondo thread lavora in autonomia ma non blocca il processo principale come succede nelle chiamate dei metodi classici.Questo permette di gestire il giocatore automatico parallelo senza bloccare il giocatore automatico, abbiamo avuto il bisogno di gestire la chiamata al metodo move in modo automatico e parallelo al processo principale senza bloccarlo e da li è nata la nostra l'idea di un thread di un altro processo.la chiamata al metodo move avviene in questo metodo 
adbtclick è l'ascoltatore che lavora nel processo principale perchè viene catturata l'evento del tasto premuto 


READ ME SECONDO NADIA

*Pr2 Project 2014*

*Francesca Trudu* -
*Fulgheri Nadia Jolanda*

Modifica dell'implementazione del gioco 2048 in modo da permettere, opzionalmente, di giocare autonomamente con un giocatore automatico. 



Strumenti utilizzati:

-github
-netbeans

*Game2048.java*
La classe Game2048 contiene il main e il metodo start, implementa le funzioni e le variabili che si occupano di inizializzare e gestire l interfaccia grafica.
Dalla classe in questione viene inizializzato anche un oggetto di tipo GameManager che si occupa di tutte le funzioni di gestione del gioco: 
-meccanismi di somma e spostamento delle caselle, 
-aggiornamento della griglia (a livello grafico), 
-aggiornamento dello score, 
-conclusione del gioco in caso di game over e game won della partita.


Modifiche effettuate:
-aggiunta del package giocatoreAutomatico (e giocatoreAutomatico.player);
-aggiunta delle classi implementate dalle interfacce.

-aggiunta di 3 variabili in GameManager -> boolean: gameOver e gameWon pubbliche e Griglia: myGriglia viene aggiornata in base alla situazione del gioco


-aggiunta di variabili, di un ascoltatore e di un Thread in Game2048 -> giocatoreAutomatico: viene creato un oggetto giocatoreAutomatico tramite il suo metodo; 
-aggiunta di button per attivare il giocatore automatico e della conseguente azione che crea un Thread permettendo di simulare la pressione del tasto shift tramite un oggetto di tipo Robot, evento che viene catturato da un ascoltatore apposito addBtnClicked che implementa l'azione da eseguire: 
-chiamata al metodo del giocatoreAutomatico prossimaMossa che restituisce un int random da 0 a 3, che verrà utilizzato dallo switch case per restituire la Direction ed essere successivamente passato al metodo move() del GameManager.

GameManager  si occupa di gestire tutto il procedimento del movimento di una casella, delle sue conseguenze, di inizializzare  myGriglia e di aggiornarla contemporaneamente a GameGrid.
Finchè non si ha il gameOver (e anche il gameWon) il Robot continua a premere shift e ogni volta l'ascoltatore intercetta l evento permettendo l esecuzione del gioco in autonomia.

Il processo principale rimane comunque l'intefaccia grafica.
L'oggetto giocatore automatico viene creato tramite il suo metodo button (per attivare il giocatore automatico), la pressione del tasto shift è creato tramite un oggetto di tipo robot, che va in un thread che viene mandato in esecuzione affianco all'interfaccia grafica.
Il meccanismo di simulazione di premere il tasto shift viene fatto in un altro processo (thread) rispetto al processo principale perchè cosi può lavorare in maniera simultanea rispetto all'interfaccia grafica<, infatti questo permette il suo funzionamento. Non sarebbe stata corretto in sostituzione l'utilizzo  di una for o una while perchè l'aggiornamento del processo secondario non sarebbe stato simultaneo a quello dell'interfaccia grafica e quindi il tutto non sarebbe stato corretto.

Il thread secondario serve per far gestire l'evento per premere il tasto shift riconoscerlo e richiamare alcuni metodi in un altro thread che è separato da quello principale.
I due processi lavorano in maniera affiancata o meglio parallela; il secondo thread lavora in autonomia ma non blocca il processo principale come succede nelle chiamate dei metodi classici.Questo permette di gestire il giocatore automatico parallelo senza bloccare il giocatore automatico, abbiamo avuto il bisogno di gestire la chiamata al metodo move in modo automatico e parallelo al processo principale senza bloccarlo e da li è nata la nostra l'idea di un thread di un altro processo.la chiamata al metodo move avviene in questo metodo 
addBtnclick è l'ascoltatore che lavora nel processo principale perchè viene catturata l'evento del tasto premuto.
