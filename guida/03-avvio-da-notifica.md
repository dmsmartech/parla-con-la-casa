# 3. Fallo partire da una notifica

[← Torna all'indice](../README.md)

Il bello dei Comandi Rapidi in **iOS 27** è che possono **partire automaticamente quando arriva la notifica di un'app**. Basta scegliere come avvio le notifiche di una o più app e decidere cosa eseguire.

Con le notifiche di Home Assistant, quindi, puoi far fare al tuo iPhone delle azioni in base a quello che succede in casa. «Parla con la casa» sfrutta proprio questo: quando Home Assistant vuole dirti qualcosa ti manda una notifica, il comando parte da solo, te la legge ad alta voce e resta in ascolto della tua risposta. Funziona così:

1. In Home Assistant succede qualcosa e un'automazione manda una notifica al tuo iPhone, con un **titolo speciale**: `VOICE ASSISTANT`.
2. L'iPhone riconosce quel titolo e avvia «Parla con la casa».
3. Il comando legge il testo della notifica e si mette in ascolto.

Le altre notifiche di Home Assistant, con titoli diversi, restano normali notifiche.

## 3.1 Controlla l'avvio nel comando

1. In Comandi tieni premuto **Parla con la casa** → **Modifica**.
2. In cima al comando deve esserci il blocco **Quando ricevo una notifica da Home Assistant**.

**Se c'è già**, controlla che sia impostato così, poi passa al punto 3.2:

| Impostazione | Valore |
|---|---|
| App | **Home Assistant** |
| Filtro | **Titolo** contiene `VOICE ASSISTANT` |
| Automazione | **attivo** |
| Avvisa | **disattivo**, così parte senza chiederti conferma |

**Se non c'è**, aggiungilo:

1. Nella barra **Cerca** in basso scrivi `notifica`.
2. Scegli **Quando ricevo una notifica** e trascinalo in cima al comando.
3. Tocca il campo dell'app e scegli **Home Assistant**.
4. Tocca **Aggiungi filtro** → **Titolo** → **contiene** → scrivi `VOICE ASSISTANT`.
5. Attiva **Automazione** e disattiva **Avvisa**.

> [!NOTE]
> I nomi delle voci possono cambiare leggermente tra una versione di iOS e l'altra.

## 3.2 Fai leggere il testo della notifica

Sotto le tre azioni Testo trovi un blocco **Se … ha un valore** con dentro **Leggi ad alta voce**. È la parte che ti legge la notifica.

1. Tocca la variabile nel blocco **Se** e scegli **Notifica → Corpo**.
2. Fai lo stesso nell'azione **Leggi ad alta voce** subito sotto.

«Corpo» è il messaggio della notifica. Non scegliere «Titolo», altrimenti l'iPhone leggerebbe «VOICE ASSISTANT».

## 3.3 Trova il nome del tuo iPhone in Home Assistant

Per mandare una notifica al tuo iPhone, Home Assistant usa un nome come `notify.mobile_app_iphone_di_marco`.

1. In Home Assistant apri **Strumenti per sviluppatori → Azioni**.
2. Nel campo **Azione** scrivi `mobile_app`.
3. Compare l'elenco dei telefoni collegati: trova il tuo e **annotati il nome completo**, per esempio `notify.mobile_app_iphone_di_marco`.

## 3.4 Prova con una notifica

1. Resta in **Strumenti per sviluppatori → Azioni**.
2. In basso tocca **Passa alla modalità YAML**.
3. Cancella tutto e incolla questo testo:

```yaml
action: notify.mobile_app_IL_TUO_IPHONE
data:
  title: VOICE ASSISTANT
  message: "Ciao, sono la tua casa. Come posso aiutarti?"
  data:
    tag: voiceassistant
```

4. Nella prima riga sostituisci `notify.mobile_app_IL_TUO_IPHONE` con il nome del punto 3.3.
5. Tocca **Esegui azione**.

Dopo pochi secondi l'iPhone dice «Ciao, sono la tua casa. Come posso aiutarti?», poi «Ti ascolto».

6. La prima volta iOS ti chiede alcuni permessi: **microfono**, **riconoscimento vocale** e **connessione** al tuo indirizzo di Home Assistant. Tocca **Consenti** ogni volta.
7. Prova con un comando semplice, per esempio «che ore sono?» oppure «accendi la luce della cucina».
8. Ascolta la risposta. Poi prova un'altra richiesta, oppure di' «basta» per chiudere.

Se hai sentito la risposta, il comando funziona. Se qualcosa non va, guarda i [problemi più comuni](07-problemi.md).

> [!TIP]
> Il comando capisce solo i dispositivi che hai **esposto ad Assist**. Li controlli in **Impostazioni → Assistenti vocali → Esponi**.

### Cosa vuol dire ogni riga

| Riga | Significato |
|---|---|
| `action:` | A quale telefono mandare la notifica |
| `title: VOICE ASSISTANT` | Il titolo che fa partire il comando. Deve essere **esattamente** quello del filtro del punto 3.1 |
| `message:` | La frase che l'iPhone ti legge ad alta voce |
| `tag: voiceassistant` | Un'etichetta che permette di cancellare la notifica in un secondo momento. È facoltativa |

Da qui in poi, ogni volta che vuoi che la casa «ti chiami», basta mandare una notifica con titolo `VOICE ASSISTANT` da qualsiasi automazione.

---

[← Indietro](02-installa-il-comando.md) · [Avanti: Le frasi che vuoi tu →](04-frasi-personalizzate.md)
