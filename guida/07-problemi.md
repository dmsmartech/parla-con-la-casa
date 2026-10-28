# 7. Se qualcosa non va

[← Torna all'indice](../README.md)

## Installazione

| Cosa succede | Cosa fare |
|---|---|
| Tocco **Aggiungi comando rapido** e non succede niente | Tocca **Salta configurazione**: il comando viene aggiunto lo stesso. Poi inserisci indirizzo e token come al [passo 2.4](02-installa-il-comando.md#24-cambiare-indirizzo-token-o-agente-dopo). È un comportamento di alcune versioni di iOS |
| Errore **«non ha potuto convertire da RTF a URL»** | L'indirizzo contiene testo formattato. Cancellalo e **riscrivilo a mano** con la tastiera, senza incollarlo |
| Il comando dice **«Non riesco a parlare con Home Assistant. Controlla indirizzo e token»** | Indirizzo o token sbagliati. Controlla che l'indirizzo si apra dal browser dell'iPhone e che il token sia incollato per intero, senza spazi |
| Funziona a casa ma **non fuori** | Stai usando l'indirizzo locale. Metti quello esterno, vedi il [passo 2.2](02-installa-il-comando.md#22-trova-lindirizzo-di-home-assistant) |
| Errore di **connessione** o **tempo scaduto** | Home Assistant non è raggiungibile in quel momento: controlla la rete dell'iPhone e che Home Assistant sia acceso |

## Avvio da notifica

| Cosa succede | Cosa fare |
|---|---|
| La notifica arriva ma il comando **non parte** | In Comandi → **Automazione** controlla che l'automazione di **Parla con la casa** sia **abilitata**. Poi controlla che il titolo della notifica sia **esattamente** `VOICE ASSISTANT` e che nel comando il filtro sia **Titolo contiene `VOICE ASSISTANT`**, con **Automazione** attivo |
| Il comando parte ma **non legge** la notifica | Nel blocco **Se** e in **Leggi ad alta voce** la variabile deve essere **Notifica → Corpo**, vedi il [passo 3.2](03-avvio-da-notifica.md#32-fai-leggere-il-testo-della-notifica) |
| Legge «VOICE ASSISTANT» invece del messaggio | Hai scelto **Titolo** invece di **Corpo** |
| La notifica **non arriva** | Controlla il nome del telefono nell'azione `notify.mobile_app_…` e che l'app Home Assistant abbia il permesso di mandare notifiche, in **Impostazioni iPhone → Notifiche → Home Assistant** |
| Mi chiede conferma prima di partire | Nel blocco **Quando ricevo una notifica** disattiva **Avvisa** |

## Conversazione

| Cosa succede | Cosa fare |
|---|---|
| Risponde **«Mi dispiace, non ho capito»** | La frase non rientra nei comandi che Assist conosce. Riprova con parole più semplici, oppure insegnagli la frase come nel [passo 4](04-frasi-personalizzate.md) |
| Risponde **«Non conosco nessun dispositivo chiamato …»** | Ha capito un comando ma non il nome del dispositivo. Controlla che il dispositivo sia esposto ad Assist e aggiungi un alias con il nome che usi a voce |
| Una mia frase funziona **scritta** ma non **a voce** | La dettatura scrive la frase in modo diverso: numeri in lettere («uno» invece di «1»), parole unite («portefinestre»). Aggiungi la variante alla frase |
| Le mie frasi delle automazioni **non vengono riconosciute** | Nel comando la terza azione Testo deve essere `conversation.home_assistant`. Con un agente AI le frasi delle automazioni non vengono usate |
| Si ferma dopo «Perfetto!» o «Ok» | Hai fatto una pausa: la dettatura ha chiuso la frase lì. Di' la frase tutta d'un fiato |
| Si chiude da solo | Dopo 3 silenzi o 3 «non ho capito» di fila il comando si chiude. È voluto, per non restare in ascolto all'infinito |

## Le frasi per chiudere

Il comando si chiude quando dici una di queste frasi.

**Da sole**, eventualmente precedute da «ok», «no», «sì», «va bene», «perfetto», «niente» o «grazie»:

grazie · grazie mille · niente · nulla · ciao · stop · esci · fine · basta · ok · no · va bene · perfetto · a posto · annulla · chiudi · fatto · finito · tutto qui · è tutto · non importa · buonanotte · a dopo · a presto · alla prossima

**Anche dentro una frase più lunga:**

basta · ho finito · abbiamo finito · nient'altro · arrivederci · a posto così · termina · lascia perdere · lascia stare · non mi serve altro · non importa · chiudi la conversazione · fine conversazione · smetti di ascoltare · puoi andare

Le frasi come «chiudi il cancello», «è tutto chiuso?» o «accendi la luce grazie» **non** chiudono la conversazione: vengono mandate a Home Assistant.

---

[← Indietro](06-intelligenza-artificiale.md) · [Torna all'indice](../README.md)
