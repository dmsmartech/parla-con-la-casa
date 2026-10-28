# 2. Installa il comando

[← Torna all'indice](../README.md)

In questo passo crei il **token** (la chiave con cui il comando entra in Home Assistant), e aggiungi il comando all'iPhone.

Il comando parte **solo da una notifica** di Home Assistant: se lo avvii toccandolo in Comandi non fa niente. La prima prova la fai nel [capitolo 3](03-avvio-da-notifica.md), dopo aver impostato l'avvio.

## 2.1 Crea il token in Home Assistant

Il token è una chiave lunga che permette al comando di parlare con la tua casa.

1. Apri Home Assistant dal browser o dall'app.
2. In basso a sinistra tocca **il tuo nome** (il tuo profilo).
3. Apri la scheda **Sicurezza**.
4. Scorri fino a **Token di accesso a lungo termine** e tocca **Crea token**.
5. Come nome scrivi `Parla con la casa` e conferma.
6. Compare il token: **copialo subito**. Home Assistant te lo mostra una volta sola.
7. Incollalo nell'app **Note** dell'iPhone, così lo ritrovi tra poco.

> [!WARNING]
> Il token è come la chiave di casa: chi lo ha può comandare il tuo Home Assistant. Non mandarlo a nessuno e non pubblicarlo. Se pensi che qualcuno lo abbia visto, cancellalo dalla stessa schermata e creane un altro.

## 2.2 Trova l'indirizzo di Home Assistant

È l'indirizzo che usi per aprire Home Assistant dal browser. Ce ne sono di due tipi:

| Tipo | Esempio | Funziona |
|---|---|---|
| **Locale** | `http://192.168.1.10:8123` | Solo quando l'iPhone è sul Wi-Fi di casa |
| **Esterno** | `https://abcd1234.ui.nabu.casa` | Ovunque, anche fuori casa |

Se hai l'abbonamento **Home Assistant Cloud** (Nabu Casa), l'indirizzo esterno lo trovi in **Impostazioni → Home Assistant Cloud → Accesso remoto**. Se hai un tuo dominio, usa quello.

Se non hai un indirizzo esterno, usa quello locale: il comando funzionerà solo in casa.

## 2.3 Aggiungi il comando all'iPhone

Tieni a portata di mano l'**indirizzo** del punto 2.2 e il **token** del punto 2.1, salvato nell'app Note.

1. Dall'iPhone apri il link: **[Aggiungi «Parla con la casa»](https://www.icloud.com/shortcuts/df9651cbaa704b548ee2871ba8ff76cf)**.
2. Si apre l'app Comandi, con la schermata di configurazione del comando. Ti chiede i dati uno alla volta:

| Cosa ti chiede | Cosa scrivere |
|---|---|
| **Indirizzo** di Home Assistant | L'indirizzo del punto 2.2, per esempio `http://192.168.1.10:8123`. **Scrivilo a mano** con la tastiera |
| **Token** | Apri Note, copia il token del punto 2.1, torna in Comandi e incollalo |
| **Agente** | È già compilato: lascia quello che vedi. Se in futuro vuoi usare un'intelligenza artificiale, lo cambi come spiegato nel [capitolo 6](06-intelligenza-artificiale.md) |

3. Tocca **Aggiungi comando rapido**.

Il comando ora è nella tua libreria di Comandi, con il nome **Parla con la casa**.

Ora controlla che l'avvio automatico sia abilitato:

4. Nell'app **Comandi** apri la sezione **Automazione**.
5. Cerca l'automazione **Quando ricevo una notifica da Home Assistant** collegata a **Parla con la casa**.
6. Controlla che sia **abilitata**. Se è disattivata, aprila e attivala.

Senza questa automazione abilitata, la notifica arriva ma il comando non parte.

> [!IMPORTANT]
> **Scrivi l'indirizzo a mano**, senza incollarlo. Se lo incolli da una pagina web, iOS si porta dietro la formattazione e il comando si ferma con un «errore di conversione».
>
> Il **token** invece incollalo dall'app Note, che toglie la formattazione. Controlla che non ci siano spazi prima o dopo.

> [!TIP]
> **Se toccando «Aggiungi comando rapido» non succede niente**, tocca **Salta configurazione**. Il comando viene aggiunto lo stesso, e i dati li inserisci a mano come spiegato nel punto 2.4. Su alcune versioni di iOS la schermata di configurazione dei comandi condivisi si blocca: è un comportamento di iOS, non del comando.

## 2.4 Cambiare indirizzo, token o agente dopo

Ti serve questo punto se hai toccato **Salta configurazione**, oppure se in futuro vuoi cambiare un dato: un nuovo token, un altro indirizzo, o un agente con l'intelligenza artificiale come nel [capitolo 6](06-intelligenza-artificiale.md).

1. Apri l'app **Comandi** e tieni premuto **Parla con la casa** → **Modifica**.
2. In cima trovi tre azioni **Testo**, una sotto l'altra:

| Azione | Cosa contiene |
|---|---|
| **Prima** | L'indirizzo di Home Assistant |
| **Seconda** | Il token |
| **Terza** | L'agente, di solito `conversation.home_assistant` |

3. Tocca il testo da cambiare, cancellalo e scrivi quello nuovo. Valgono le stesse regole di prima: indirizzo **scritto a mano**, token **incollato da Note**.
4. Tocca **Fine** in alto a destra.

---

[← Indietro](01-prima-di-iniziare.md) · [Avanti: Fallo partire da una notifica →](03-avvio-da-notifica.md)
