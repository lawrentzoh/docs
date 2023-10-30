[Aggiornata al 30 Ottobre 2023]

[lorenzo@starktech.it](mailto:lorenzo@starktech.it)
## Iscrizione e Configurazione Account

Per poter pubblicare un applicazione sull'App Store è necessario iscriversi all'Apple Develper Program **e posserere un Mac**. Prima di poter proseguire è necessario essere in possesso di un Apple ID, oppure [crearne uno nuovo](https://appleid.apple.com/). Per iscriversi all'Apple Developer Program, accedere alla [pagina dedicata ](https://developer.apple.com/programs/enroll/)e completare il processo di enrollment. Alla fine di tutto verrà chiesto di abbonarsi al servizio per 100$ all'anno. L'abbonamento è obbligatorio per pubblicare le app sull'App Store, sia per mantenere pubblicate quelle già presenti.

Nota: si consiglia di inserire una carta di credito nell'account ed attivare il rinnovo automatico per evitare che, allo scadere dell'abbonamento, le app vengano nascoste o rimosse dallo store.

### Apple Developer

Accedere al pannello di controllo [Apple Developer](https://developer.apple.com/) con l'account appena creato. Questo pannello di controllo è principalmente utilizzato per: 

- Rinnovare la Membership
- Creare certificati, id, profili ecc.  

Prendere nota del Team ID presente nella pagina Membership. Il Team ID viene molto spesso richiesto per la configurazione di certi plugin (ad esempio firebase ).
### App Store Connect

Accedere all'[App Store Connect](https://developer.apple.com/) con l'Apple ID appena creato. Questo pannello di controllo è utilizzato principalmente per:

- Pubblicare e aggiornare le applicazioni  
- Vedere reports e analytics sulle app pubblicate 
- Gestire utenti e permessi

È utile iniziare ad aggiungere gli utenti che dovranno gestire l'account. Questo può essere fatto nella pagina Utenti e Accessi. Cliccare sul (+) per inviare un nuovo utente al team. Selezionare il ruolo e le app a cui l'utente avrà accesso. A questo punto, l'utente dovrà accettare l'invito ricevuto via email e potrà accedere all'App Store Connect **tramite il suo Apple ID** e gestire l'applicazione (limitatamente alle funzionalità autorizzate). 

È molto importante aggiungere al team gli sviluppatori che dovranno pubblicare l'applicazione, cosi che possano compilare e caricare l'app bundle senza dover accedere con l'Apple ID dell'amministratore.

Nota: l'email fornita deve essere di un Apple ID.

## Creazione dei Certificati

Per la pubblicazione dell'app è necessario generare vari certificati e identificativi. Tutti i certificati vengono creati nel pannelloApple Developer, nella pagina Certificates, Identifiers & Profiles.

### Certificates

In questa sezione vengono creati vari certificati utilizzati per firmare le applicazioni sia in sviluppo che in produzione. È necessario creare almeno due tipi di certificati: Apple Development e Apple Distribution (che sia il certificato generico o quello specifico per iOS o macOS). Inoltre potrebbero essere richiesti altri certificati per abilitare alcuni servizi come le Notifiche Push.

1. Cliccare su + per creare un nuovo certificato.   
2. Selezionare il tipo e cliccare su Continue.
3. 1. Verrà richiesto di caricare un CertificateSigningRequest. È necessario generare questo file da un Mac tramite l'app di sistema Keychain Access. Seguire la [guida ufficiale di Apple](https://developer.apple.com/help/account/create-certificates/create-a-certificate-signing-request/) per generare la CSR e caricarla sul portale.
4. Cliccare su Continue e generare il certificato. Scaricare il certificato e farne il backup, ma non caricarlo in repository, sopratutto se pubbliche.

È necessario creare almeno un certificato Apple Development per lo sviluppo dell'applicazione, e sarà necessario creare un certificato Apple Distribution per pubblicare l'app quando lo sviluppo è completo.

### Profiles

In questa sezione vengono creati i Provisioning Profiles per permettere di installare le applicazioni su iOS e macOS e per distribuirle. Senza un profilo, non è possibile caricare l'applicazione sullo store e non è possibile installare in modalità debug l'applicazione sui dispositivi. Per generare un profilo è necessario aver già generato un certificato dello stesso tipo del profilo che si vuole creare (Development o Distribution).

1. Cliccare su (+) per creare un nuovo profilo.  
2. Selezionare il tipo e cliccare su Continue.  
3. Selezionare l'applicazione al quale il profilo è associato.  
4. Selezionare il certificato precedentemente creato che sarà utilizzato per firmare il profilo. 
5. Inserire un nome per identificare il profilo.  
6. Generare il certificato.

Un profilo raccoglie tutte le informazioni e certificati dell'applicazione. Per questo motivo, se viene modificato qualche certificato o aggiunta/rimossa qualche Capability nell'applicazione, potrebbe essere necessario rigenerare il profilo.

### Identifiers

In questa sezione in genere sarà necessario creare solo un Identifier, cioè l'App ID (Bundle ID). L'App ID è assolutamente necessario per pubblicare l'applicazione, ma

anche per configurare correttamente alcune librerie e/o servizi cloud. Si consiglia quindi di crearlo il prima possibile.

Accedere ad Apple Developer nella pagina Certificates, Identifiers & Profiles per registrare un Identifiers. Selezionare App ID e poi App. Nella schermata successiva vi saranno alcuni dati da inserire:

**Bundle ID**: è l'ID dell' applicazione sull'AppStore. Dovrebbe essere uguale a quello utilizzato nel Play Store, in un formato tipo com.mycompany.myapp. 

**Description**: Una descrizione breve dell'identifier.

**Capabilities**: Sono i servizi della Apple che l'app utilizza. Selezionare i servizi che si prevede di utilizzare (es: Push Notifications, Sign in with Apple). Potranno comunque essere modificati in futuro.

Cliccare su Continue e su Register. Verrà creato il Bundle ID. Questo Bundle ID dovrà essere anche inserito nell' Info.plist . 

### Devices

In questa sezione devono essere registrati i dispositivi che verranno utilizzati per lo sviluppo e debugging dell'applicazione (cioè i dispositivi in cui verrà installata l'applicazione in modalità debug, collegati via cavo al Mac e a Xcode). Registrare i dispositivi inserendo il Device UDID e assegnandogli un nome.

Nota: il Device ID si può recuperare collegando il dispositivo al Mac, aprendo il Finder e cliccando sul nome del dispositivo collegato. Verranno visualizzate, in alto, vari identificativi del dispositivo, tra cui il Device ID.

### Keys

In questa sezione vengono generate alcune chiavi necessarie per usufruire di alcuni servizi Apple. In genere sarà necessario creare una chiave per utilizzare le Notifiche Push, ed una per il Login con Apple ID. Per creare la chiave, selezionare il servizio per cui si sta creando la chiave, assegnargli un nome e cliccare su Continue e poi su Register.

## Generazione Icone e Splash Screen Icone App

Per creare l'icona dell'app è consigliato utilizzare qualche generatore online, in particolare EasyAppIcon.

1. Caricare l'icona  
2. Scegliere il colore dello sfondo  
3. Cliccare su Download e selezionare iOS+AdaptiveIcon

Il file scaricato conterrà tutte le icone necessarie sia per Android che per iOS. Il file è strutturato esattamente come la cartella ios del progetto, per cui copiare i file nella cartella e sovrascrivere quando richiesto.

Icona Notifiche

Non esiste un icona notifica su iOS. L'icona mostrata corrisponde all'icona dell'app.

Splash Screen

Per la generazione dello Splash Screen utilizzare il plugin flutter_native_splash . Installarlo tra le dev_dependencies : dart pub add --dev flutter_native_splash

Nel pubspec.yaml , configurare il plugin:

```
dev_dependencies:

flutter_test:

sdk: flutter

flutter_native_splash:

CONFIGURAZIONE flutter_native_splash

flutter_native_splash:

color: "#ffffff" # Colore sfondo splash screen

image: "assets/images/splash.png" # Immagine dello splash screen
```


Dopodichè eseguire il plugin con:

```flutter pub run flutter_native_splash:create```

Lo Splash Screen dovrebbe essere configurato per Android e per iOS.

Nota: L'immagine utilizzata dovrebbe essere un immagine molto grande (più dello schermo) con il logo dell'app al centro. Lasciare molto bordo in modo che si adatti a tutte le dimensioni dello schermo e che il logo non sia troppo grande.

In alternativa a flutter_native_splash è possibile utilizzare un sito di generatori di immagini come Ape Tools.

## Verifica della Configurazione

Prima del rilascio è consigliato verificare che la configurazione dell'app sia corretta e pronta per funzionare in modalità release.

**Importante**: Molti plugin e librerie richiedono modifiche alla configurazione (es: facebook_auth, image_cropper, molti plugin di firebase ecc.). Per ogni singola libreria ci sarà una configurazione ben particolare che dovrebbe essere stata implementata correttamente seguendo le istruzioni della libreria trovate su pub.dev

durante lo sviluppo. In questo paragrafo verranno mostrate le configurazioni di base da verificare prima della pubblicazione, senza tener conto di alcun plugin aggiuntivo.

In Android Studio, posizionarsi sopra la cartella ios e aprire il menu cliccando col tasto destro. Cliccare su Flutter > Open iOS Module in Xcode. 

Altrimenti, aprire Xcode, selezionare "File" nella barra degli strumenti del Mac, selezionare "Apri", recarsi nella seguente directory: `` MyProject -> ios `` ed aprire il file con estensione ".xcworkspace"
### Accesso con Apple ID

È necessario accedere ad un'Apple ID su Xcode per poter pubblicare l'applicazione. L'Apple ID può essere quello dell'account amministratore che ha creato l'applicazione, oppure quello personale (dello sviluppatore) che però deve essere stato inserito nel team dall'amministratore. Per accedere con l'Apple ID, su Xcode cliccare nella status bar in alto a sinistra su Xcode > Preferences > Accounts e aggiungere l'account desiderato. Una volta effettuato l'accesso, dovrebbero essere mostrati tutti i team di cui l'account fa parte.

### Info

Cliccare Runner e poi sul project Runner. In questa sezione verificare:

iOS Deployment Target : la versione minima di iOS per installare l'app. Flutter richiede almeno iOS 9, ma alcune librerie potrebbero richiedere una versione più alta. È consigliato selezionare almeno iOS 10 (al momento, alcune librerie compatibili con flutter 2.10 richiedono anche iOS 11).

Localizations : aggiungere tutte le lingue supportate dall'applicazione. Anche se l'app supporta diverse lingue, se non vengono inserite in questo punto, sull'App Store verrà sempre mostrata come lingua dell'app l'inglese.

### General

Cliccare Runner e di nuovo sul target Runner. Nella sezione General, verificare i seguenti parametri:
- Display Name: il nome dell'app da visualizzare nello store  
- Bundle Identifier: il Bundle ID. Deve corrispondere all'Identifier creato in Bundle ID.
- Version: dovrebbe corrispondere a quella in ``pubspec.yaml.  
- Build : dovrebbe corrispondere a quella in ``pubspec.yaml``. Assicurarsi che sia comunque un valore superiore all'ultimo Build Number caricato nell'App Store

oppure il processo di caricamento darà errore.

### Signing & Capabilities

Nella sezione Signing & Capabilities, verificare i seguenti parametri:

- Automatically manage signing: controllare che sia attivato.
- Team: selezionare il team dell'account che possiede l'applicazione. Per vedere il team corretto è necessario che l'account con cui si è effettuato l'accesso su Xcode sia stato invitato al team dall'amministratore dell'account Apple Developer (vedi sezione App Store Connect). 
- Bundle Identifier: il Bundle ID. Deve corrispondere a quello visto nella sezione General.
- Capabilities: verificare che tutte le Capabilities utilizzate dall'app siano presenti nella configurazione. Se non sono presenti, aggiungere cliccando sul + in alto a sinistra.

Nota: anche se durante la creazione del Bundle ID nei certificati del pannello Apple Developer è stata selezionata qualche Capability (es: notifiche push), è comunque necessario aggiungere la Capability anche da Xcode se non presente, viceversa il servizio non funzionerà correttamente. In ogni caso, in genere per implementare una Capability è richiesto di installare qualche libreria di Flutter (o nativa) e a questa sarà associata una documentazione su come implementare il servizio correttamente. Questa documentazione dovrebbe coprire anche i dettagli su come abilitare la Capability per l'app.

### Build Settings

iOS Deployment Target: la versione minima di iOS per installare l'app. Dovrebbe essere uguale a quella impostata su  ``Project > Runner > iOS Deployment Target``.

## Compilazione e Archiviazione

Una volta che si è sicuri che l'applicazione sia pronta per la pubblicazione, si procede alla creazione dell'archivio (o bundle) che verrà caricato nell'App Store. Nota: per la compilazione e distribuzione dell'app è assolutamente necessario avere un Mac con Xcode installato.

### Aprire Xcode

Una volta aperto Xcode, se non si presenta la pagina Runners, cliccare sull'icona a forma di cartella nella colonna di sinistra e cliccare su Runner. Nella pagina appena comparsa, cliccare su Runner presente sotto la scritta TARGETS. In questo modulo verranno mostrati il nome dell'applicazione, il suo Bundle ID, la versione e il numero di build. Verificare qui che il numero di build e versione del pacchetto corrispondano a quelli impostati su Flutter nel ``pubspec.yaml`` . Molte volte accade che questi valori non siano sincronizzati.

### Firma dell'App

Senza selezionando Runner tra i TARGETS, spostarsi sulla tab Signing & Capabilities. Se non è già stato fatto precedentemente, abilitare Automatically manage signing e selezionare il team appropriato per la firma dell'applicazione. Il team corretto è quello dell'account da cui verrà pubblicata l'applicazione.

### Compilazione

Prima di procedere alla compilazione è consigliato pulire la cache cliccando, nella barra del menu di macOS in alto, ``Product > Clean Build Folder``. 

Completata la pulizia, cambiare tipo di build cliccando sulla barra degli strumenti di Xcode e selezionando Any iOS Device.
![[https://github.com/lawrentzoh/docs/blob/2a02af8438174661e6996d7d75d96e2fc8d19611/Screenshot%202023-10-30%20alle%2012.59.36.png]]

Cliccare poi su ``Product > Build`` per iniziare la compilazione. La compilazione potrebbe richiedere parecchi minuti in funzione della potenza di calcolo della macchina e delle dimensioni dell'app.

### Archiviazione

Se la build ha avuto successo, è possibile finalmente procedere al caricamento dell'app sull'App Store. Per fare ciò, cliccare su Product > Archive. Alla conclusione dell'operazione, si aprirà una finestra con tutte le versioni dell'app archiviate localmente. Cliccare sulla versione appena compilata e poi su Distribute App. 

Cliccare avanti mantenendo tutte le impostazioni di default fino ad arrivare all'ultimo passaggio, e cliccare su Upload. Il pacchetto verrà caricato direttamente sull'App Store e sarà disponibile nell'App Store Connect per la pubblicazione.

Una volta caricato l'archivio, è possibile cancellarlo dalla schermata della cronologia archivi per liberare spazio sul disco.

Nota: una volta caricato l'archivio, è necessario attendere la sua elaborazione prima che sia effettivamente visibile nell'App Store Connect. In genere ci vogliono circa 30 minuti.

## TestFlight

Prima del rilascio ufficiale dell'applicazione, è buona norma adibire una fase di test interno o esterno. In Apple questa funzione si chiama TestFlight.

### Test Interni

Accedere all'App Store Connect e cliccare sull'app che si vuole testare. Cliccare poi nella tab TestFlight. Nella colonna di sinistra, creare un nuovo gruppo cliccando sul pulsante + in Test interni. Creato il gruppo, cliccare su di esso ed aggiungere i tester cliccando sul +. Gli utenti riceveranno un invito che dovranno accettare prima di poter accedere al test.

Nota: le E-Mail degli invitati devono corrispondere alle E-Mail utilizzare nei loro Apple ID. Nota: nei test interni, solo gli utenti facenti parte del team possono essere invitati al test.

Le build caricate nell'App Store Connect dovrebbero essere automaticamente disponibili ai tester interni. Se così non fosse, cliccare suBuild > iOS nella colonna di sinistra, cliccare sulla build interessata ed assegnarla ai gruppi desiderati. Molte volte, prima di poter fare ciò verrà richiesto di compilare il questionario di conformità sull'esportazione (vedi sezione Pubblicazione).

### Test Esterni

Per invitare tester che non appartengono al team, è necessario prima compilare le Informazioni per il test, cliccando nell'omonima sezione della barra laterale sinistra. Una volta inserite tutte le informazioni richieste, dovrebbe essere possibile creare gruppi ed invitare tester esterni per provare l'applicazione.

### Scaricare un'App in Test

Le applicazioni in test non sono presenti nell'App Store. Per scaricare l'applicazione in test è necessario innanzitutto scaricare dall'App Store l'app [TestFlight](https://apps.apple.com/it/app/testflight/id899247664) ed accedere con l'Apple ID in cui si è ricevuto l'invito al test. Una volta dentro, verrà mostrato l'elenco di tutte le app a cui si è stati invitati per il test. Per scaricarle cliccare semplicemente su installa.

## Prima Pubblicazione

Il processo di pubblicazione avviene principalmente nell'App Store Connect. Creazione dell'App

Nell'App Store Connect, cliccare su My Apps ed aggiungere una nuova App cliccando su pulsante (+). 
Selezionare:
- Piattaforme: iOS.  
- Nome: nome dell'applicazione (sarà visibile nell'App Store).  
- Lingua primaria: selezionare la lingua dell'applicazione.  
- ID Pacchetto: selezionare il Bundle ID appena creato.  
- SKU: inserire un identificativo univo. Potrebbe essere il Bundle ID, oppure un codice SKU generato casualmente, o qualsiasi ID univoco.
- Accesso Utenti: quali utenti dell'Apple Developer Team possono visualizzare l'applicazione.

### Configurazione dell'App

Vi sono varie informazioni da fornire ad Apple per poter pubblicare l'applicazione. Cliccare sull'app appena creata per accedere alla pagina di gestione dell'applicazione. Nella pagina iniziale, completare le seguenti informazioni:

- Screenshots: inserire gli screenshot dell'app. Almeno 3 schermate devono essere presenti. Le dimensioni devono corrispondere a quelle suggerite da Apple. Descrizione: descrizione per esteso dell'applicazione.  
- Parole Chiave: tag utilizzati per facilitare la ricerca dell'app nello store.  
- Url Assistenza: url per il portale di assistenza, visualizzato nella pagina dell'app nello store.
- Versione: verificare che la versione dell'app sia corretta. Copyright: inserire il copyright nel formato richiesto.

Nella sezione Informazioni per il team di verifica delle app dovranno essere inserite le informazioni necessarie al team di verifica dell'applicazione per testarla e approvarla. 

Se l'app richiede un login, sarà necessario inserire le credenziali di accesso.

Inserire inoltre il contatto di un responsabile che il team di verifica può contattare per informazioni. Se l'applicazione è complessa, o se il test e l'utilizzo delle funzionaliità richiede una situazione particolare (es: funzionamento con geolocalizzazione solo in certi luoghi), inserire anche una nota esplicativa sul funzionamento e l'obiettivo dell'app. 

Se si vuole si può anche allegare un video che mostra l'app in funzione per chiarire le idee al team di verifica.

Nella pagina informazioni app completare tutte le informazioni richieste:

- Nome App: dovrebbe già essere inserito, è il nome dell'app come viene visualizzato nello store. 
- Sottotitolo: una breve frase che viene visualizzata in piccolo sotto il nome dell'app.  
- Categoria: selezionare le categorie più affini con l'app.

Nella pagina Prezzi e disponibilità:

- Inserire il prezzo dell'applicazione (se a pagamento).  
- Selezionare la disponibilità geografica dell'app (in quali Paesi l'applicazione sarà disponibile).

Nella pagina Privacy dell'app dovranno essere inserite moltissime informazioni sull'utilizzo e condivisione dei dati nell'app:

- Url per le norme sulla privacy: un link che punti ad una pagina web o un documento con l'informativa sulla privacy dell'app.  

- Tipologia di dati: selezionare ogni tipologia di dati che l'applicazione utilizza, salva e/o condivide. Per ogni tipologia di dati raccolti dovrà essere compilato un questionario su come vengono utilizzati i dati, per quale motivo, con chi vengono condivisi e perché. Compilare il tutto il più precisamente possibile, avendo premura di indicare ogni tipo di dato effettivamente utilizzato dall'applicazione **Questo processo potrebbe essere lungo e tedioso**.

Una volta completato l'inserimento di tutte queste informazioni, l'applicazione dovrebbe essere pronta per essere inviata al team di verifica. 

Il processo di pubblicazione, a questo punto, segue gli stessi passaggi visti sulla sezione Pubblicazioni Successive

### Encryption Export Regulations

Ogni volta che viene caricato un App Bundle nell'App Store Connect, verrà chiesto di compilare un piccolo questionario sull' Encryption Export Regulations. Questo questionario riguarda alcune leggi americane sulla criptazione dei dati. Se l'applicazione (o qualsiasi libreria utilizzata nell'app) utilizza solo metodi di encrypt pubblici, opensource o esenti da restrizioni (es: SSL, HTTPS, MD5 ecc.) allora l'applicazione sarà esente da restrizione. In genere, ogni applicazione che ci connette a internet utilizzerà almeno il protocollo HTTPS per cui il 99% delle volte il questionario dovrà essere completato in questo modo:

L'applicazione utilizza un metodo di encrypt di qualsiasi tipo? SI L'applicazione è esente dal regolamento sull'export? SI

A meno che l'applicazione non utilizzi un metodo di encrypt di proprietà, questa dovrebbe sempre essere esente.

Nota: è possibile aggiungere nell' Info.plist la chiave ITSAppUsesNonExemptEncryption con valore NO per evitare che ad ogni upload dell'app venga chiesto il questionario.

IMPORTANTE: pur essendo esente, per rispettare al 100% le leggi americane andrebbe inviato ogni anno (entro il primo di febbraio) un autodichiarazione sulle applicazioni pubblicate sull'app store che utilizzano metodo di encrypt, anche se esenti. Questo obbligo parte dall'anno successivo alla pubblicazione dell'app sullo store. Esistono alcuni siti che facilitano la compilazione di questo modello, come Open Source Self-Classification Report Generator. Procedere in questo modo:

1. Accedere alla web app per generare il report.
2. Inserire nome, cognome, numero di telefono ed indirizzo.
3. Selezionare NO su Non-U.S.Components e scrivere N/A su Non-U.S. Manufacturing locations.
4. Nella scheda Products inserire:
    - Model Number e Manufacturer: N/A  
    - Export Control Classification Number: 5D992 Authorization Type: MMKT  
    - Item Type: Mobility e mobile applications n.e.s.
5. Cliccare su Add Product e ripetere la procedura per ogni app nell'AppStore
6. Esportare il file.
7. Inviare il fil e acrypt-supp8@bis.doc.gov e enc@nsa.gov con oggetto self-classification report e specificare nella mail qualche informazione di contatto del responsabile e il periodo di riferimento del report (es: year 2021).

**Nota Bene**: se l'applicazione é esente e gratuita, è necessario inviare il self-report solo una volta, all'inizio dell'anno successivo a quello di pubblicazione dell'app sullo store.

## Pubblicazioni Successive

Le successive release saranno estremamente più veloci da effettuare.

1. Creareunanuovaversionedell'appdapubblicare,cliccaresul+asinistraedinizializzareunanuovarelease.
    
2. Inserireilnumerodellaversione(chedovrebbecorrispondereallaversionedell'appcompilataedarchiviatasuXcode).
    
3. InserireilCHANGELOGnellasezioneNovitàdiquestaversione.Verificareanchecheilnumerodiversionesiacorrettonelriquadropocosotto.
    
4. Selabuildhacompletatol'elaborazione,dovrebbeesserepossbileselezionarlatraleBuilddisponibiliallapubblicazionenell'appositoriquadro.
    
5. Inaltoadestra,cliccaresuSalvaepoisuInviaalTeamdiverificaperiniziareilprocessodirevisione.
    
6. Aquestopunto,ènecessarioattenderecheilteamdirevisioneverifichiilfunzionamentodell'applicazioneeapprovilapubblicazioneneglistore.Mediamente
    

il tempo di attesa è di 24h.

## Problemi Comuni

### Bug in Release

Se sono presenti dei bug che non sono stati scoperti in test, o bug che sono presenti solo in produzione, Apple potrebbe rifiutare l'applicazione citando Performance Issues e consigliando di procedere con un Beta Testing su TestFlight. Si consiglia di chiedere ai reviewer più informazioni riguardo al problema.

### Login con Apple ID  
Se viene utilizzato un qualsiasi Login Social, Apple rende obbligatorio l'utilizzo del Login con Apple ID, pena il rifiuto della pubblicazione dell'app.

### Accettazione Contratti e Privacy

Se viene effettuato il Login con Apple ID, il flusso di accesso non può mai essere interrotto. Il che significa che l'utente deve poter cliccare su Accedi con Apple ID e poter, una volta effettuato l'accesso, utilizzare l'applicazione senza ulteriori interruzioni. Questo significa che non è possibile far accettare contratti vari e informativa sulla privacy durante il Login con Apple ID, ne obbligare l'utente ad accettarli bloccando le funzionalità dell'applicazione una volta effettuato l'accesso. Per ovviare a questo problema, una soluzione può essere quella di far accettare esplicitamente i contratti ancora prima di effettuare qualsiasi accesso o registrazione. Ad esempio, nella pagina di introduzione all'applicazione, l'ultima slide potrebbe mostrare i contratti e obbligare l'utente ad accettarli prima ancora di poter vedere la prima pagina dell'applicazione.

### Controllo del Contenuto Generato dagli Utenti

Se nell'app è presente contenuto generato dall'utente e visibile a persone diverse dall'utente stesso, Apple pretenderà che sia implementato anche un sistema di controllo e moderazione per rimuovere il contenuto illecito e disabilitare gli utenti che non seguono le regole. Un sistema di questo tipo potrebbe essere un semplice pulsante o azione che gli utenti possono usare per segnalare il contenuto agli amministratori.

### Link a Siti esterni di Proprietà

Se nell'applicazione vi sono link che portano a siti web di proprietà dello sviluppatore/azienda dell'applicazione, Apple potrebbe accorgersene e presumere che l'utente venga tracciato attraverso dei cookies all'esterno dell'app ma sempre di proprietà dell'azienda. Per evitare problemi, potrebbe essere necessario chiedere il permesso App Tracking Transparency mostrando un avviso all'apertura dell'app oppure prima dell'apertura del link.

### Contenuti non Completi e Placeholders

Apple non vuole che i contenuti visibili nell'applicazione contengano frasi di placeholder o incomplete (ad esempio il classico Lorem Ipsum). Se ci sono screenshot dell'applicazione nello store o contenuti nell'app che usano contenuti di placeholder (sia stringhe che media) Apple potrebbe rifiutare l'applicazione. Inoltre, se sono presenti nel bundle asset non utilizzati in runtime, questi dovrebbero essere rimossi per alleggerire l'applicazione e per aderire alle guidelines di Apple.

