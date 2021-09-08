# Track my pantry (Android app)

## Indice

- [Registrare l'utente](#Registrare-l'utente)
- [Autenticare l'utente](#Autenticare-l'utente)
- [Aggiornare il db remoto](#Aggiornare-il-db-remoto)
- [Aggiornare il db locale](#Aggiornare-il-db-locale)

#### Registrare l'utente

- Siccome serve l'autentcazione per accedere all'app, l'utente deve poter registrarsi
- **OP0 (REGISTER)**: l'utente deve registrarsi inserendo mail e password

#### Autenticare l'utente

- Un utente deve autenticarsi prima di poter usufruire usufruire delle funzionalità dell'applicazione
- **OP1 (AUTH)**: l'utente deve autenticarsi inserendo username, mail e password

#### Aggiornare il db remoto

- I prodotti devono essere registrati attraverso il loro barcode in un db remoto
- Ogni volta che un utente compra un prodotto puo eseguire le seguenti operazioni
  - **OP2 (GET PRODUCTS BY BARCODE)**: chiedere al web service di restituire la lista di prodotti che corrsipondono al barcode passato come parametro (si parla di lista perchè per lo steso prodotto, piu utenti potrebbero inserire informazioni diverse del db remoto).
    <br />
    Biosgna mandare almeno un voto positivo, si possono mandare piu voti tra i quali anche negativi.
    <br />
    Il voto puo essere: -1, 0, 1
  - **OP3 (POST VOTES)**: se il prodotto è presente nella lista, allora l'utente seleziona quel prodotto inserendo un voto(in questo modo notifica il web server della sua scelta).
  - **OP4 (POST PRODUCT DETAILS)**: se la lista restituita è vuota o non contiene le infromazioni desiderate, l'utente compila i relativi campi e inserisce il nuovo prodotto

#### Aggiornare il db locale

- **OP5 (INSERT PRODUCT)**: l'utende puo inserire un nuovo prodotto nella dispensa
- **OP6 (DELETE PRODUCT)**: l'utende puo imuovere un prodotto nella dispensa
- **OP7 (VIEW ALL PRODUCTS)**: l'utende puo vedere tutti i prodotti nella dispensa

#### Features aggiuntive

- Usare la fotocamera per lo scanner del barcode
- Aggiunta di informazioni al momento nel momento dell'inserimento di un prodotto nella dispensa (sia infomativi che quantitativi)
- Aggiunta di un immagine del prodotto
- Ricerca di prodotti
- Filtri per la ricerca all'interno della dispensa
- Aumento e decremento di quantità di un prodotto
- Sistema di avviso quando un prodotto è scaduto
- Lista dei desideri
- Mandare in formato pdf le liste via whatsapp
