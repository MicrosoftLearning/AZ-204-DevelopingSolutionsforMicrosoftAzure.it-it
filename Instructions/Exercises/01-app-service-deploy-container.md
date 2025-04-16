---
lab:
  title: Distribuire un'app in contenitori nel servizio app Azure
  description: Informazioni su come distribuire un'app in contenitori in app Azure Servizio.
---

# Distribuire un'app in contenitori nel servizio app Azure

In questo esercizio si distribuisce una semplice app in contenitori in app Azure Servizio. 

Attività eseguite in questo esercizio:

* Creare una risorsa del servizio app Azure per un'app in contenitori
* Visualizzare i risultati
* Pulire le risorse

Il completamento di questo esercizio richiede circa **15** minuti.

## Prima di iniziare

Per completare l'esercizio necessario:

* Una sottoscrizione di Azure. Se non si dispone ancora di una sottoscrizione, è possibile [registrarsi per una](https://azure.microsoft.com/).

## Creare una risorsa dell'app Web

1. Nel browser passare al portale di Azure [https://portal.azure.com](https://portal.azure.com); accedere con le credenziali di Azure, se richiesto.
1. Selezionare l'intestazione **+ Crea una risorsa** che si trova nell'intestazione **Servizi** di Azure nella parte superiore della home page. 
1. Nella barra di ricerca cerca nel **Marketplace** immettere *l'app* Web e premere **INVIO** per iniziare la ricerca.
1. Nel riquadro App Web selezionare l'elenco **a discesa Crea** e quindi selezionare **App** Web.

    ![Screenshot del riquadro App Web.](./media/01/create-web-app-tile.png)

Selezionando **Crea** verrà aperto un modello con alcune schede per compilare le informazioni sulla distribuzione. I passaggi seguenti illustrano le modifiche da apportare nelle schede pertinenti.

1. Compilare la **scheda Informazioni di base** con le informazioni nella tabella seguente:

    | Impostazione | Azione |
    |--|--|
    | **Abbonamento** | Mantenere il valore predefinito. |
    | **Gruppo di risorse** | Selezionare Crea nuovo, immettere `rg-WebApp`e quindi selezionare OK. |
    | **Nome** | Immettere un nome univoco, ad esempio `<your-initials>-containerwebapp`. Sostituire *\<your-initials>* con le proprie iniziali o con un altro valore. Il nome deve essere univoco, quindi potrebbe essere necessario apportare alcune modifiche. |
    | Dispositivo di scorrimento in **Impostazione nome** | Selezionare il dispositivo di scorrimento per disattivarlo. |
    | **Pubblicazione** | Selezionare l'opzione **Contenitore** . |
    | **Sistema operativo** | Verificare che **Linux** sia selezionato. |
    | **Area** | Mantenere la selezione predefinita o scegliere un'area nelle vicinanze. |
    | **Piano Linux** | Mantenere la selezione predefinita. |
    | **Piano tariffario** | Selezionare l'elenco a discesa e scegliere il **piano F1** gratuito. |

1. Selezionare o passare alla **scheda Contenitore** e immettere le informazioni nella tabella seguente:

    | Impostazione | Azione |
    |--|--|
    | **Supporto sidecar** | Mantieni la posizione predefinita disattivata. |
    | **Origine immagine** | Selezionare **Altri registri contenitori**. |
    | **Tipo di accesso** | Mantieni la selezione pubblica** predefinita**. |
    | **URL del server del Registro di sistema** | Immetti `mcr.microsoft.com/k8se`. |
    | **Immagine e tag** | Immetti `quickstart:latest`. |
    | **Comando di avvio** | Lasciare vuoto. |

1. Selezionare la scheda **Rivedi e crea**.
1. Esaminare le selezioni effettuate e quindi selezionare il **pulsante Crea** .

Il completamento della distribuzione richiederà alcuni minuti. Al termine, selezionare il **pulsante Vai alla risorsa** .

Ora che la distribuzione è stata completata, è possibile visualizzare l'app Web. Selezionare il collegamento all'app Web accanto al campo Dominio** predefinito nella **sezione Informazioni di base**.** Il collegamento aprirà il sito in una nuova scheda.

>**Nota:** l'esecuzione e la visualizzazione dell'app contenitore distribuita nella nuova scheda potrebbero richiedere alcuni minuti.

## Pulire le risorse

Dopo aver completato l'esercizio, è necessario eliminare le risorse cloud create per evitare l'utilizzo delle risorse non necessarie.

1. Passare al gruppo di risorse creato e visualizzare il contenuto delle risorse usate in questo esercizio.
1. Sulla barra degli strumenti selezionare **Elimina gruppo di risorse**.
1. Immettere il nome del gruppo di risorse e confermarne l'eliminazione.
