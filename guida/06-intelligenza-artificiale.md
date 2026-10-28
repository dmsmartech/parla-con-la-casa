# 6. Con l'intelligenza artificiale

[← Torna all'indice](../README.md)

Con l'agente integrato, Assist capisce solo le frasi che conosce: i comandi standard più quelle che gli hai insegnato tu. Se colleghi un'**intelligenza artificiale** ad Assist, i binari spariscono:

- parli come con una persona, senza frasi preparate: «ho freddo», «com'è messa la casa?», «sto uscendo, c'è qualcosa da sistemare?»;
- l'AI guarda lo stato della casa, capisce cosa vuoi, esegue e ti risponde;
- **ricorda il discorso**: dopo «accendi la luce della cucina» puoi dire «spegnila», e capisce di cosa parli.

Il comando è già pronto: basta dirgli quale agente usare.

## Quale intelligenza artificiale

Home Assistant ne supporta diverse:

| Servizio | Costo | Note |
|---|---|---|
| **Google Gemini** | Piano gratuito con limiti giornalieri | Il più semplice da provare gratis. È quello che usiamo in questa guida |
| **OpenAI (ChatGPT)** | A consumo | Si paga in base a quanto lo usi, di solito pochi centesimi |
| **Ollama** | Gratis | Gira in casa tua, ma serve un computer potente sempre acceso. Un Raspberry Pi non basta |

I prezzi e i limiti cambiano spesso: controllali sul sito del servizio prima di iniziare.

## Collegare Google Gemini, passo passo

### 1. Crea la chiave gratuita

1. Vai su **[aistudio.google.com](https://aistudio.google.com)** e accedi con un account Google.
2. Apri **Get API key**, oppure **API Keys** nel menu, e tocca **Create API key**.
3. Se ti chiede un progetto e non ne hai, creane uno nuovo chiamato per esempio `Home Assistant`.
4. Copia la chiave e salvala nell'app Note. È come una password: non darla a nessuno.
5. Nell'elenco delle chiavi, accanto alla tua, controlla che come piano ci sia **Free tier**.

> [!NOTE]
> **Non ti viene addebitato niente** finché non colleghi un metodo di pagamento. Non toccare **Set up billing**. Quando superi il limite gratuito, Gemini smette di rispondere fino al giorno dopo, senza costi.
>
> Sul piano gratuito Google può usare le richieste per migliorare i suoi servizi. Non dire all'assistente cose che non vorresti far leggere a nessuno.

### 2. Aggiungi Gemini a Home Assistant

1. **Impostazioni → Dispositivi e servizi → Aggiungi integrazione**.
2. Cerca **Google Gemini**. Nelle versioni meno recenti si chiama **Google Generative AI**.
3. Incolla la chiave e conferma.

### 3. Permettigli di comandare la casa

1. Apri l'integrazione appena aggiunta.
2. Accanto all'agente di conversazione, di solito «Google AI Conversation», tocca l'**ingranaggio** o **⋮ → Riconfigura**.
3. In **Controlla Home Assistant** spunta **Assist**. Senza questa spunta Gemini risponde alle domande ma non può accendere né spegnere niente.
4. Nelle **Istruzioni** sostituisci il testo in inglese con questo:

```text
Sei l'assistente vocale di casa. Rispondi sempre in italiano, con frasi brevi e semplici,
perché le risposte vengono lette ad alta voce. Niente elenchi, simboli o emoji.
Quando esegui un'azione conferma in poche parole cosa hai fatto.
```

5. Tocca **Invia**.

Gemini vede e comanda solo i dispositivi **esposti ad Assist** (**Impostazioni → Assistenti vocali → Esponi**). Esponi solo quelli che ti servono a voce: meno sono, più risponde veloce e preciso.

### 4. Trova il nome dell'agente

1. **Impostazioni → Dispositivi e servizi → Entità**.
2. Cerca `conversation`.
3. Trovi l'agente di Gemini, con un nome come **`conversation.google_ai_conversation`**. Copia quel nome.

### 5. Collega il comando all'AI

1. In Comandi tieni premuto **Parla con la casa** → **Modifica**.
2. Nella **terza** azione Testo sostituisci `conversation.home_assistant` con il nome del punto 4, per esempio `conversation.google_ai_conversation`.
3. Tocca **Fine**.

Ora prova con una domanda libera: «quali luci sono accese?», «com'è la temperatura in casa?», poi «accendi la luce della cucina» e subito dopo «spegnila».

Per tornare all'assistente con le frasi preparate, rimetti `conversation.home_assistant` nella terza azione Testo.

## Cosa cambia rispetto all'agente integrato

| | Agente integrato | Intelligenza artificiale |
|---|---|---|
| **Cosa capisce** | Comandi standard e frasi che hai preparato | Qualsiasi frase |
| **Velocità** | Istantaneo, sotto il secondo | Qualche secondo, di solito tra 4 e 8 sul piano gratuito |
| **Memoria del discorso** | No | Sì |
| **Frasi delle automazioni** (come la demo) | Sì | **No**, decide l'AI |
| **Precisione sui numeri** | Esatta, legge lo stato reale | Può sbagliare un conteggio |
| **Costo** | Gratis | Gratis entro i limiti, oppure a consumo |
| **Funziona senza internet** | Sì, se usi l'indirizzo locale | No, a meno di usare Ollama in casa |

Un consiglio pratico: per le conversazioni avviate da una notifica, come la demo, usa l'**agente integrato** con le tue frasi. È istantaneo e fa esattamente quello che hai deciso. Usa l'AI quando vuoi chiacchierare liberamente con la casa.

## Se Gemini dà errore

- **«This model is currently experiencing high demand» (503):** i server di quel modello sono sovraccarichi, di solito per pochi minuti. Se succede spesso, riconfigura l'agente, togli la spunta da **Impostazioni del modello consigliate** e scegli un altro modello dal menu **Modello**, preferibilmente uno con «flash-lite» nel nome.
- **«This model … is no longer available to new users» (404):** quel modello è stato ritirato. Scegline uno più recente dallo stesso menu, come suggerisce il messaggio.
- **Risponde in inglese o in modo lungo:** controlla le istruzioni del punto 3.
- **Risposte lente:** nella stessa schermata metti **Livello di ragionamento** su **Minimo**, e riduci i dispositivi esposti.

---

[← Indietro](05-esempio-del-video.md) · [Avanti: Se qualcosa non va →](07-problemi.md)
