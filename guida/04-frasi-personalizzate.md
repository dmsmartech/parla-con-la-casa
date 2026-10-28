# 4. Le frasi che vuoi tu

[← Torna all'indice](../README.md)

## Come ragiona Assist

L'assistente vocale integrato di Home Assistant funziona come gli assistenti vocali senza intelligenza artificiale: segue dei **binari**. Conosce un elenco di frasi, per esempio «accendi *nome* », «spegni *nome*» o «che temperatura c'è in *stanza*». Se dici una frase che rientra in quei modelli la esegue, altrimenti risponde «non ho capito».

La differenza rispetto agli altri assistenti è che **i binari li puoi costruire tu**:

- puoi insegnargli **qualsiasi frase**, anche lunga e discorsiva: «perfetto, ci sono porte o finestre rimaste aperte?»;
- puoi decidere **cosa fa**: accendere luci, attivare un allarme, avviare uno script, mandare una notifica, qualsiasi cosa sappia fare Home Assistant;
- puoi decidere **cosa risponde**, parola per parola, anche con informazioni prese dalla casa.

La conversazione del video funziona esattamente così. Non c'è un'intelligenza artificiale: c'è un'automazione con tre frasi preparate.

Ci sono tre modi per dare nuove frasi ad Assist, dal più semplice al più potente.

## Modo 1: gli alias, cioè altri nomi per le stesse cose

Un alias è un nome in più per un dispositivo. Serve quando chiami una cosa diversamente da come si chiama in Home Assistant.

Esempio: la luce si chiama «Lampada Hue 3», ma tu dici «luce del divano».

1. **Impostazioni → Assistenti vocali → Esponi**.
2. Tocca il dispositivo.
3. In **Alias** aggiungi `luce del divano` e salva.

Ora «accendi la luce del divano» funziona. Gli alias si possono dare anche alle **stanze** e ai **piani**, dalle loro impostazioni.

> [!TIP]
> La dettatura dell'iPhone scrive i numeri in lettere: «IKEA 1» diventa «IKEA uno». Se un dispositivo ha un numero nel nome, aggiungi un alias con il numero scritto in lettere.

## Modo 2: le automazioni con frase (il più usato)

Un'automazione può partire quando dici una frase. In più può **rispondere** con il testo che vuoi. È lo strumento più comodo, e quello usato nel video.

### Creare un'automazione con frase

1. **Impostazioni → Automazioni e scene → Crea automazione → Crea nuova automazione**.
2. In **Quando**, tocca **Aggiungi attivazione** → **Frase**, che può comparire anche come «Conversazione».
3. Scrivi la frase, per esempio `buonanotte casa`. Puoi aggiungerne quante vuoi con **Aggiungi frase**.
4. In **Allora fai**, aggiungi le azioni che vuoi: spegni le luci, chiudi le tapparelle, attiva l'allarme...
5. Come ultima azione aggiungi **Imposta risposta della conversazione** e scrivi cosa deve rispondere, per esempio `Buonanotte! Ho spento tutto e chiuso le tapparelle.`
6. Salva.

Da questo momento «buonanotte casa» esegue tutto e ti risponde.

### Scrivere una frase che capisca tanti modi di dire

Le persone dicono la stessa cosa in tanti modi. Invece di scrivere decine di frasi, usa questi simboli:

| Simbolo | Significa | Esempio | Capisce |
|---|---|---|---|
| `[ ]` | parola **facoltativa** | `[per favore] accendi la tv` | «accendi la tv», «per favore accendi la tv» |
| `( \| )` | **una tra** queste parole | `(attiva\|inserisci) l'allarme` | «attiva l'allarme», «inserisci l'allarme» |
| `[( \| )]` | **una tra** queste parole, oppure nessuna | `[(subito\|adesso)]` | «subito», «adesso» o niente |
| `{ }` | **una parola qualsiasi**, che poi puoi usare | `metti in lista {cosa}` | «metti in lista il latte», «metti in lista le uova» |

Esempio completo:

```text
[(ok|perfetto)] (attiva|inserisci|accendi) [subito] (l'allarme|l'antifurto) [per favore]
```

Questa sola riga capisce «attiva l'allarme», «ok, inserisci subito l'antifurto», «perfetto, accendi l'allarme per favore» e tutte le combinazioni.

Punteggiatura, maiuscole e minuscole non contano: «Attiva l'allarme!» e «attiva l'allarme» sono la stessa frase.

### Risposte che leggono la casa

La risposta non deve essere per forza fissa. Può contenere informazioni prese da Home Assistant:

```yaml
set_conversation_response: "In salotto ci sono {{ states('sensor.temperatura_salotto') }} gradi."
```

Nell'[esempio reale](05-esempio-del-video.md#la-versione-reale) la risposta dice **quali** finestre sono aperte, leggendole dai sensori.

### Dove funziona e dove no

- Le frasi delle automazioni funzionano con l'**agente integrato** di Home Assistant, cioè `conversation.home_assistant`, quello che il comando usa di serie.
- Hanno la **precedenza** sui comandi standard. Se la tua frase assomiglia a un comando standard, vince la tua.
- Se nel comando imposti un agente con intelligenza artificiale, le frasi delle automazioni non vengono usate: l'AI decide da sola. Lo spieghiamo nel [passo 6](06-intelligenza-artificiale.md).

## Modo 3: scene e script

Scene e script esposti ad Assist si avviano a voce con il loro nome. Per esempio, una scena chiamata «Cena» si attiva con «attiva Cena». Esponili in **Impostazioni → Assistenti vocali → Esponi** e dai loro un alias facile da dire.

Se vuoi una frase più naturale, come «mettiamo l'atmosfera per la cena», usa il Modo 2: un'automazione con quella frase che avvia la scena.

> [!NOTE]
> Per chi è esperto esiste anche un quarto modo: i file di frasi personalizzate nella cartella `custom_sentences` della configurazione, insieme a `intent_script`. Sono più potenti ma si scrivono a mano in YAML. Per quasi tutti i casi le automazioni con frase bastano e avanzano.

## Prova le frasi senza parlare

Prima di provarle a voce, controlla le frasi scrivendole:

- **Dall'app o dal sito di Home Assistant**: tocca l'icona di **Assist** in alto a destra in qualsiasi dashboard e scrivi la frase.
- **Strumenti per sviluppatori → Assist**: scrivi una frase e Home Assistant ti mostra cosa ha capito e quale automazione o comando userebbe.

Se scritta funziona ma a voce no, il problema è la dettatura. Succede per esempio con «porte o finestre», che la dettatura può scrivere come una parola sola, «portefinestre». Aggiungi alla frase anche quella variante.

## Fattele scrivere da un'intelligenza artificiale

Non serve imparare la sintassi a memoria. Puoi chiedere a ChatGPT o Gemini di scrivere l'automazione per te. Usa un messaggio come questo, cambiando la parte in mezzo:

```text
Scrivimi un'automazione di Home Assistant in YAML con un'attivazione di tipo
"conversation" (frase). Quando dico una frase come "buonanotte casa" deve:
spegnere tutte le luci, chiudere le tapparelle del soggiorno (cover.soggiorno)
e attivare l'allarme (alarm_control_panel.casa).
Poi deve rispondere con set_conversation_response: "Buonanotte, ho chiuso tutto".
Le frasi devono capire tante varianti naturali in italiano: usa [ ] per le
parole facoltative e ( | ) per le alternative.
```

Poi incolla il risultato in Home Assistant: **Crea nuova automazione → ⋮ in alto a destra → Modifica in YAML**.

Se la tua intelligenza artificiale è **collegata direttamente a Home Assistant**, per esempio tramite un server MCP, puoi chiederle di creare e provare l'automazione da sola, con i nomi veri dei tuoi dispositivi.

---

[← Indietro](03-avvio-da-notifica.md) · [Avanti: L'esempio del video, da rifare →](05-esempio-del-video.md)
