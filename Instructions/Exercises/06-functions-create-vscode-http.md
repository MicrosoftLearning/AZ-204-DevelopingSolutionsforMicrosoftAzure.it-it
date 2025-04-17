---
lab:
  title: Creare una funzione di Azure con Visual Studio Code
  description: 'Informazioni su come creare una funzione di Azure con un trigger HTTP. Dopo aver creato e testato il codice in locale in Visual Studio Code, distribuire la funzione in Azure.'
---

# Creare una funzione di Azure con Visual Studio Code

In questo esercizio si apprenderà come creare una funzione C\# che risponde alle richieste HTTP. Dopo aver creato e testato il codice in locale in Visual Studio Code, distribuire e testare la funzione in Azure.

Attività eseguite in questo esercizio:

* Creare una risorsa del servizio app Azure per un'app in contenitori
* Visualizzare i risultati
* Pulire le risorse

Il completamento di questo esercizio richiederà circa **30** minuti.

## Prima di iniziare

Prima di iniziare, verificare che siano soddisfatti i requisiti seguenti:

* Una sottoscrizione di Azure. Se non si dispone ancora di una sottoscrizione, è possibile [registrarsi per una](https://azure.microsoft.com/).

* [Funzioni di Azure Core Tools](https://github.com/Azure/azure-functions-core-tools#installing) versione 4.x.

* [Visual Studio Code](https://code.visualstudio.com/) in una delle [piattaforme supportate](https://code.visualstudio.com/docs/supporting/requirements#_platforms).

* [.NET 8](https://dotnet.microsoft.com/en-us/download/dotnet/8.0) è il framework di destinazione.

* [C# Dev Kit](https://marketplace.visualstudio.com/items?itemName=ms-dotnettools.csdevkit) per Visual Studio Code.

* [Estensione Funzioni di Azure](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurefunctions) per Visual Studio Code.

## Creare il progetto locale

In questa sezione si userà Visual Studio Code per creare un progetto di Funzioni di Azure locale in C#. Più avanti in questo esercizio il codice della funzione verrà pubblicato in Azure.

1. In Visual Studio Code premere F1 per aprire il riquadro comandi e cercare ed eseguire il comando `Azure Functions: Create New Project...`.

1. Selezionare la posizione della directory per l'area di lavoro del progetto e quindi scegliere **Seleziona**. È necessario creare una nuova cartella o scegliere una cartella vuota per l'area di lavoro del progetto. Non scegliere una cartella di progetto che fa già parte di un'area di lavoro.

1. Quando richiesto, immettere le informazioni seguenti:

    | Richiesta | Azione |
    |--|--|
    | Selezionare la cartella che conterrà i progetti di funzione | Selezionare **Sfoglia per** selezionare una cartella per l'app.
    | Selezionare una lingua | Selezionare **C#**. |
    | Selezionare un runtime .NET | Selezionare **.NET 8.0 Isolato** |
    | Selezionare un modello per la prima funzione del progetto | Selezionare **Trigger** HTTP.<sup>1</sup> |
    | Specificare un nome di funzione | Immetti `HttpExample`. |
    | Specificare uno spazio dei nomi | Immetti `My.Function`. |
    | Livello di autorizzazione | Selezionare **Anonimo**, che consente a chiunque di chiamare l'endpoint della funzione. |

    <sup>1</sup> A seconda delle impostazioni di VS Code, potrebbe essere necessario usare l'opzione **Modifica filtro** modello per visualizzare l'elenco completo dei modelli.

1. Visual Studio Code usa le informazioni fornite e genera un progetto di Funzioni di Azure con un trigger HTTP. È possibile visualizzare i file di progetto locali in Explorer.

### Eseguire la funzione in locale

Visual Studio Code si integra con Azure Functions Core Tools per consentire l'esecuzione di questo progetto nel computer di sviluppo locale prima della pubblicazione in Azure.

1. Assicurarsi che il terminale sia aperto in Visual Studio Code. È possibile aprire il terminale selezionando **Terminale** e quindi **Nuovo terminale** nella barra dei menu. 

1. Premere **F5** per avviare il progetto di app per le funzioni nel debugger. L'output dagli strumenti di base viene visualizzato nel pannello **Terminale**. L'app viene avviata nel pannello **Terminale**. È possibile visualizzare l'endpoint dell'URL della funzione attivata da HTTP eseguita in locale.

    ![Lo screenshot dell'endpoint della funzione attivata tramite HTTP viene visualizzato nel pannello Terminale.](./media/06/run-function-local.png)

1. Con Core Tools in esecuzione, passare all'area **Azure: Funzioni**. In **Funzioni** espandere **Progetto locale** > **Funzioni**. Fare clic con il pulsante destro del mouse sulla **funzione HttpExample** e scegliere **Esegui funzione ora...**.

    ![Screenshot che mostra il percorso della funzione Execute Now... passo.](./media/06/execute-function-local.png)

1. In **Immettere il corpo** della richiesta immettere il valore del corpo del messaggio di richiesta di `{ "name": "Azure" }`. Premere **INVIO** per inviare il messaggio di richiesta alla funzione. Quando la funzione viene eseguita in locale e restituisce una risposta, viene generata una notifica in Visual Studio Code.

    selezionare l'icona a forma di campana di notifica per visualizzare la notifica. Le informazioni sull'esecuzione della funzione sono visualizzate nel riquadro **Terminale**.

1. Premere **MAIUSC + F5** per arrestare Core Tools e disconnettere il debugger.

Dopo aver verificato che la funzione viene eseguita correttamente nel computer locale, è possibile usare Visual Studio Code per pubblicare il progetto direttamente in Azure.

## Distribuire ed eseguire la funzione in Azure

In questa sezione si crea una risorsa dell'app per le funzioni di Azure e si distribuisce la funzione nella risorsa.

### Accedere ad Azure

Prima di potere pubblicare l'app, è necessario accedere ad Azure. Se è già stato eseguito l'accesso, passare alla sezione successiva.

1. Se non è ancora stato effettuato l'accesso, selezionare l'icona di Azure sulla barra attività, quindi nell'area **Azure: Funzioni** scegliere **Accedi ad Azure**.

    ![Screenshot del pulsante Accedi ad Azure.](./media/06/functions-sign-into-azure.png)

1. Quando viene visualizzata la richiesta nel browser, scegliere l'account Azure e accedere con le credenziali corrispondenti.

1. Dopo avere eseguito l'accesso, è possibile chiudere la nuova finestra del browser. Le sottoscrizioni che appartengono all'account Azure vengono visualizzate nella barra laterale.

### Creare risorse in Azure

In questa sezione vengono create le risorse di Azure necessarie per distribuire l'app per le funzioni locale.

1. Selezionare l'icona di Azure nella barra attività e quindi nell'area **Risorse** selezionare il pulsante **Crea risorsa**.

    ![Screenshot del pulsante Crea risorse.](./media/06/create-resource.png)    

1. Quando richiesto, immettere le informazioni seguenti:

    | Richiesta | Azione |
    |--|--|
    | Selezionare una risorsa da creare | Selezionare **Create Function App in Azure** (Crea un'app per le funzioni in Azure) |
    | Selezionare la sottoscrizione | Selezionare la sottoscrizione da usare. *Non verrà visualizzato se si ha una sola sottoscrizione.* |
    | Immettere un nome univoco a livello globale per l'app per le funzioni: | Immettere un nome valido in un percorso URL, ad esempio `myfunctionapp`. Il nome immesso viene convalidato per assicurarsi che sia univoco. |
    | Selezionare una località per le nuove risorse | Per prestazioni ottimali, scegliere un'area vicina. |
    | Selezionare uno stack di runtime | Selezionare **.NET 8.0 Isolato**. |
    | Selezionare una dimensione di memoria dell'istanza | Selezionare **2048 Impostazione predefinita** |
    | Selezionare il numero massimo di istanze | Accettare il valore predefinito **100**. |

    L'estensione mostra lo stato delle singole risorse durante la creazione nell'area **azure** della finestra del terminale.
    
1. Al termine, nella sottoscrizione vengono create le risorse di Azure seguenti con i nomi basati sul nome dell'app per le funzioni:

    * Un gruppo di risorse, ovvero un contenitore logico di risorse correlate.
    * Un account di Archiviazione di Azure standard, che mantiene lo stato e altre informazioni sul progetto.
    * Piano a consumo Flex, che definisce l'host sottostante per l'app per le funzioni serverless.
    * Un'app per le funzioni, che fornisce l'ambiente per l'esecuzione del codice della funzione. Un'app per le funzioni consente di raggruppare le funzioni come un'unità logica per semplificare la gestione, la distribuzione e la condivisione delle risorse all'interno dello stesso piano di hosting.
    * Un'istanza di Application Insights connessa all'app per le funzioni, che tiene traccia dell'utilizzo della funzione serverless.

### Distribuire il progetto in Azure

> **! Importante:** la pubblicazione in una funzione esistente sovrascrive le distribuzioni precedenti.

1. Nel riquadro comandi cercare ed eseguire il comando **Funzioni di Azure: Distribuisci nell'app per le funzioni...**.

1. Selezionare la sottoscrizione usata durante la creazione delle risorse.

1. Selezionare l'app per le funzioni creata. Quando viene richiesto di sovrascrivere le distribuzioni precedenti, selezionare **Distribuisci** per distribuire il codice della funzione nella nuova risorsa dell'app per le funzioni.

1. Al termine della distribuzione, selezionare **Visualizza output** per visualizzare i dettagli dei risultati della distribuzione. Se si perde la notifica, selezionare l'icona a forma di campana di notifica nell'angolo in basso a destra per visualizzarla di nuovo.

    ![Screenshot del pulsante Visualizza output.](./media/06/function-view-output.png)

### Eseguire la funzione in Azure

1. Tornare all’area **Risorse** nella barra laterale, espandere la sottoscrizione, la nuova app per le funzioni e **Funzioni**. **Fare clic con il pulsante destro del mouse sulla** **funzione HttpExample** e scegliere **Esegui funzione ora...**.

    ![Screenshot dell'opzione Esegui funzione ora.](./media/06/execute-function-remote.png)

1. In **Immettere il corpo della richiesta** viene visualizzato il valore `{ "name": "Azure" }` del corpo del messaggio di richiesta. Premere INVIO per inviare il messaggio di richiesta alla funzione.

1. Quando la funzione viene eseguita in locale e restituisce una risposta, in Visual Studio Code viene generata una notifica. selezionare l'icona a forma di campana di notifica per visualizzare la notifica.

## Pulire le risorse

Dopo aver completato l'esercizio, è necessario eliminare le risorse cloud create per evitare l'utilizzo delle risorse non necessarie.

1. Nel browser passare al portale di Azure [https://portal.azure.com](https://portal.azure.com); accedere con le credenziali di Azure, se richiesto.
1. Passare al gruppo di risorse creato e visualizzare il contenuto delle risorse usate in questo esercizio.
1. Sulla barra degli strumenti selezionare **Elimina gruppo di risorse**.
1. Immettere il nome del gruppo di risorse e confermarne l'eliminazione.
