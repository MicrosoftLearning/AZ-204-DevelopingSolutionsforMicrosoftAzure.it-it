---
lab:
  title: Creare risorse di Azure Cosmos DB con per NoSQL usando .NET
  description: Informazioni su come creare risorse di database e contenitori in Azure Cosmos DB con Microsoft .NET SDK v3.
---

# Creare risorse di Azure Cosmos DB con per NoSQL usando .NET

In questo esercizio si crea un'app console che crea un contenitore, un database e un elemento in Azure Cosmos DB.

Attività eseguite in questo esercizio:

* Creare un account Azure Cosmos DB
* Creare l'applicazione console
* Eseguire l'app console e verificare i risultati

Il completamento di questo esercizio richiederà circa **30** minuti.

## Prima di iniziare

Prima di iniziare, verificare che siano soddisfatti i requisiti seguenti:

* Una sottoscrizione di Azure. Se non si dispone ancora di una sottoscrizione, è possibile [registrarsi per una](https://azure.microsoft.com/).

## Creare un account Azure Cosmos DB

In questa sezione dell'esercizio si creano un gruppo di risorse e un account Azure Cosmos DB. È anche possibile registrare l'endpoint e la chiave di accesso per l'account.

1. Nel browser passare al portale di Azure [https://portal.azure.com](https://portal.azure.com); accedere con le credenziali di Azure, se richiesto.

1. Usare il **pulsante [\>_]** a destra della barra di ricerca nella parte superiore della pagina per creare una nuova cloud shell nella portale di Azure, selezionando un ***ambiente Bash***. Cloud Shell fornisce un'interfaccia della riga di comando in un riquadro nella parte inferiore del portale di Azure.

    > **Nota**: se in precedenza è stata creata una cloud shell che usa un *ambiente PowerShell* , passare a ***Bash***.

1. Nella barra degli strumenti di Cloud Shell scegliere **Vai alla versione classica** dal menu **Impostazioni**. Questa operazione è necessaria per usare l'editor di codice.

1. Creare un gruppo di risorse con le risorse necessarie per questo esercizio. Sostituire **\<myResourceGroup>** con un nome da usare per il gruppo di risorse. Se necessario, è possibile sostituire **useast** con un'area vicina. 

    ```
    az group create --location useast --name <myResourceGroup>
    ```

1. Eseguire il comando seguente per creare l'account Azure Cosmos DB. Sostituire **\<myCosmosDBacct>** con un nome *univoco* per identificare l'account di Azure Cosmos DB. Sostituire **\<myResourceGroup>** con il nome scelto in precedenza.

    >**Nota:** il nome dell'account può contenere solo lettere minuscole, numeri e il trattino (-). Deve avere una lunghezza compresa tra 3 e 31 caratteri. *Il completamento di questo comando richiede alcuni minuti.*

    ```
    az cosmosdb create -n <myCosmosDBacct> -g <myResourceGroup>
    ```

1.  Eseguire il comando seguente per recuperare documentEndpoint **** per l'account Azure Cosmos DB. Registrare l'endpoint dai risultati del comando, che sarà necessario più avanti nell'esercizio. Sostituire **\<myCosmosDBacct>** e **\<myResourceGroup>** con i nomi creati.

    ```bash
    az cosmosdb show -n <myCosmosDBacct> -g <myResourceGroup> --query "documentEndpoint" --output tsv
    ```

1. Recuperare la chiave primaria per l'account usando il comando seguente. Registrare primaryMasterKey **** dai risultati del comando da usare nel codice. Sostituire **\<myCosmosDBacct>** e **\<myResourceGroup>** con i nomi creati.

     ```
    # Retrieve the primary key
    az cosmosdb keys list -n <myCosmosDBacct> -g <myResourceGroup>
    ```

## Creare l'applicazione console

Dopo aver distribuito le risorse necessarie in Azure, il passaggio successivo consiste nel configurare l'applicazione console usando la stessa finestra del terminale in Visual Studio Code.

1. Creare una cartella per il progetto e passare alla cartella.

    ```bash
    mkdir cosmosdb
    cd cosmosdb
    ```

1. Creare un'app console .NET.

    ```dotnetcli
    dotnet new console --framework net8.0
    ```

1. Eseguire i comandi seguenti per aggiungere il **pacchetto Microsoft.Azure.Cosmos** al progetto e anche il pacchetto Newtonsoft.Json** di supporto**.

    ```dotnetcli
    dotnet add package Microsoft.Azure.Cosmos --version 3.*
    dotnet add package Newtonsoft.Json --version 13.*
    ```

È ora possibile sostituire il codice del modello nel **file Program.cs** usando l'editor in Cloud Shell.

### Aggiungere il codice iniziale per il progetto

1. Eseguire il comando seguente in Cloud Shell per iniziare a modificare l'applicazione.

    ```bash
    code Program.cs
    ```

1. Sostituire qualsiasi codice esistente con il frammento di codice seguente dopo le **istruzioni using** . Assicurarsi di sostituire i valori segnaposto per **\<documentEndpoint>** e **\<primaryKey>** seguendo le indicazioni nei commenti del codice.

    Il codice fornisce la struttura complessiva dell'app e alcuni elementi necessari. Esaminare i commenti nel codice, aggiungere il codice nelle aree specificate nelle istruzioni. 

    ```csharp
    using Microsoft.Azure.Cosmos;
    
    namespace CosmosExercise
    {
        // This class represents a product in the Cosmos DB container
        public class Product
        {
            public string? id { get; set; }
            public string? name { get; set; }
            public string? description { get; set; }
        }
    
        public class Program
        {
            // Cosmos DB account URL - replace with your actual Cosmos DB account URL
            static string cosmosDbAccountUrl = "<documentEndpoint>";
    
            // Cosmos DB account key - replace with your actual Cosmos DB account key
            static string accountKey = "<primaryKey>";
    
            // Name of the database to create or use
            static string databaseName = "myDatabase";
    
            // Name of the container to create or use
            static string containerName = "myContainer";
    
            public static async Task Main(string[] args)
            {
                // Create the Cosmos DB client using the account URL and key
    
    
                try
                {
                    // Create a database if it doesn't already exist
    
    
                    // Create a container with a specified partition key
    
    
                    // Define a typed item (Product) to add to the container
    
    
                    // Add the item to the container
                    // The partition key ensures the item is stored in the correct partition
    
    
                }
                catch (CosmosException ex)
                {
                    // Handle Cosmos DB-specific exceptions
                    // Log the status code and error message for debugging
                    Console.WriteLine($"Cosmos DB Error: {ex.StatusCode} - {ex.Message}");
                }
                catch (Exception ex)
                {
                    // Handle general exceptions
                    // Log the error message for debugging
                    Console.WriteLine($"Error: {ex.Message}");
                }
            }
        }
    }
    ```

### Aggiungere il codice per creare il client ed eseguire operazioni 

In questa sezione dell'esercizio si aggiunge codice nelle aree specificate dei progetti per creare: client, database, contenitore e aggiungere un elemento di esempio al contenitore.

1. Aggiungere il codice seguente nello spazio dopo la creazione del ** client Cosmos DB usando l'URL dell'account e il commento della chiave** . Questo codice definisce il client usato per connettersi all'account Azure Cosmos DB.

    ```csharp
    CosmosClient client = new(
        accountEndpoint: cosmosDbAccountUrl,
        authKeyOrResourceToken: accountKey
    );
    ```

    >Nota: è consigliabile usare **DefaultAzureCredential** dalla *libreria di identità* di Azure. Ciò può richiedere alcune richieste di configurazione aggiuntive in Azure a seconda della configurazione della sottoscrizione. 

1. Aggiungere il codice seguente nello spazio dopo il ** commento Crea un database se non esiste** già. 

    ```csharp
    Microsoft.Azure.Cosmos.Database database = await client.CreateDatabaseIfNotExistsAsync(databaseName);
    Console.WriteLine($"Created or retrieved database: {database.Id}");
    ```

1. Aggiungere il codice seguente nello spazio dopo il ** commento Creare un contenitore con una chiave** di partizione specificata. 

    ```csharp
    Microsoft.Azure.Cosmos.Database database = await client.CreateDatabaseIfNotExistsAsync(databaseName);
    Console.WriteLine($"Created or retrieved database: {database.Id}");
    ```

1. Aggiungere il codice seguente nello spazio dopo ** Definire un elemento tipizzato (Product) da aggiungere al commento del contenitore** . Definisce l'elemento aggiunto al contenitore.

    ```csharp
    Product newItem = new Product
    {
        id = Guid.NewGuid().ToString(), // Generate a unique ID for the product
        name = "Sample Item",
        description = "This is a sample item in my Azure Cosmos DB exercise."
    };
    ```

1. Aggiungere il codice seguente nello spazio dopo l'aggiunta dell'elemento ** al commento contenitore** . 

    ```csharp
    ItemResponse<Product> createResponse = await container.CreateItemAsync(
        item: newItem,
        partitionKey: new PartitionKey(newItem.id)
    );
    ```

1. Ora che il codice è stato completato, salvare lo stato di avanzamento usare **CTRL+Q** per salvare il file e **ctrl + q** per uscire dall'editor.

1. Eseguire il comando seguente in Cloud Shell per verificare eventuali errori nel progetto. Se vengono visualizzati errori, aprire il *file Program.cs* nell'editor e verificare la presenza di codice mancante o errori di incollamento.

    ```bash
    dotnet build
    ```

Ora che il progetto è terminato, è possibile eseguire l'applicazione e verificare i risultati nella portale di Azure.

## Eseguire l'applicazione e verificare i risultati

1. Eseguire il `dotnet run` comando se in Cloud Shell. L'output dovrebbe essere simile all'esempio seguente.

    ```
    Created or retrieved database: myDatabase
    Created or retrieved container: myContainer
    Created item: c549c3fa-054d-40db-a42b-c05deabbc4a6
    Request charge: 6.29 RUs
    ```

1. Nella portale di Azure passare alla risorsa di Azure Cosmos DB creata in precedenza. Selezionare **Esplora dati** nel riquadro di spostamento a sinistra. In **Esplora dati selezionare **myDatabase** e quindi espandere **myContainer****. È possibile visualizzare l'elemento creato selezionando **Elementi**.

    ![Screenshot che mostra la posizione degli elementi nel Esplora dati.](./media/09/cosmos-data-explorer.png)

## Pulire le risorse

Dopo aver completato l'esercizio, è necessario eliminare le risorse cloud create per evitare l'utilizzo delle risorse non necessarie.

1. Passare al gruppo di risorse creato e visualizzare il contenuto delle risorse usate in questo esercizio.
1. Sulla barra degli strumenti selezionare **Elimina gruppo di risorse**.
1. Immettere il nome del gruppo di risorse e confermarne l'eliminazione.
