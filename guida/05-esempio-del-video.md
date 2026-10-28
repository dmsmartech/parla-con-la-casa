# 5. L'esempio del video, da rifare

[← Torna all'indice](../README.md)

Qui trovi l'automazione del video in due versioni:

1. **La demo**: l'automazione del video ridotta all'osso. Abbiamo tolto la nostra logica e lasciato solo lo scheletro, con risposte fisse e senza comandare dispositivi, così capisci come funziona e la adatti ai tuoi scopi. Si prova in 5 minuti.
2. **La versione reale**, dove ogni frase fa davvero qualcosa in casa. È il modello da copiare per le tue idee.

## La demo

### Passo 1: crea il pulsante che avvia la demo

Nella demo non c'è un vero sensore di movimento: la «chiamata» parte da un pulsante.

1. **Impostazioni → Dispositivi e servizi → Aiutanti → Crea aiutante**.
2. Scegli **Pulsante**.
3. Come nome scrivi esattamente `Demo conversazione` e tocca **Crea**.

### Passo 2: crea l'automazione

1. **Impostazioni → Automazioni e scene → Crea automazione → Crea nuova automazione**.
2. Tocca **⋮** in alto a destra → **Modifica in YAML**.
3. Cancella tutto e incolla il contenuto del file [`esempi/demo-del-video.yaml`](../esempi/demo-del-video.yaml).
4. Cerca la riga `action: notify.mobile_app_IL_TUO_IPHONE` e mettici il nome del tuo iPhone, quello trovato al [passo 3.3](03-avvio-da-notifica.md#33-trova-il-nome-del-tuo-iphone-in-home-assistant).
5. Tocca **Salva**.

### Passo 3: provala

1. Premi il pulsante **Demo conversazione**, da una dashboard oppure da **Impostazioni → Dispositivi e servizi → Aiutanti**.
2. L'iPhone dice: «Ehi, ho rilevato un movimento in giardino, ma l'allarme non è inserito.» e poi «Ti ascolto».
3. Rispondi: **«Attiva subito l'allarme!»** → «Fatto! Allarme perimetrale attivato.»
4. Chiedi: **«Perfetto! Ci sono porte o finestre rimaste aperte?»** → «No, tutto in sicurezza!»
5. Chiudi con **«Grazie, ho finito»**.

Funzionano anche tante varianti: «inserisci l'antifurto», «attivalo subito», «puoi attivare l'allarme?», «c'è qualche finestra aperta?», «ho lasciato qualcosa aperto?», «è tutto chiuso?»...

## Come è fatta, pezzo per pezzo

L'automazione ha **tre attivazioni** e, per ognuna, **una reazione**. Ogni attivazione ha un nome (`id`) che la distingue.

### Le tre attivazioni

```yaml
triggers:
  - trigger: state
    entity_id: input_button.demo_conversazione
    id: inizio
```

**«inizio»**: quando premi il pulsante. È lui che fa partire tutto.

```yaml
  - trigger: conversation
    id: allarme
    command:
      - "[(sì|si|ok|...)] (attiva|inserisci|accendi|...) [subito] (l'allarme|l'antifurto|...)"
```

**«allarme»**: quando dici una frase sull'attivazione dell'allarme. `trigger: conversation` vuol dire «quando l'utente dice una di queste frasi». Ogni riga sotto `command` è un modello di frase, scritto con i simboli spiegati nel [passo 4](04-frasi-personalizzate.md#scrivere-una-frase-che-capisca-tanti-modi-di-dire).

```yaml
  - trigger: conversation
    id: porte
    command:
      - "[(perfetto|ok|...)] ci sono (porte|finestre|portefinestre|...) [(o|e) (porte|finestre)] [rimaste] aperte"
```

**«porte»**: quando chiedi di porte e finestre. Nota la variante `portefinestre`: la dettatura dell'iPhone a volte unisce «porte o finestre» in una parola sola.

### Le reazioni

Il blocco `choose` sceglie cosa fare in base a quale attivazione è scattata.

```yaml
      - conditions:
          - condition: trigger
            id: inizio
        sequence:
          - action: notify.mobile_app_IL_TUO_IPHONE
            data:
              title: VOICE ASSISTANT
              message: "Ehi, ho rilevato un movimento in giardino, ma l'allarme non è inserito."
```

Se è scattato **«inizio»**, manda la notifica con titolo `VOICE ASSISTANT`. È quel titolo che fa partire il comando sull'iPhone.

```yaml
      - conditions:
          - condition: trigger
            id: allarme
        sequence:
          - delay:
              milliseconds: 400
          - set_conversation_response: "Fatto! Allarme perimetrale attivato."
```

Se è scattato **«allarme»**, aspetta un attimo per sembrare più naturale, poi **risponde**. `set_conversation_response` è la frase che l'iPhone ti leggerà.

```yaml
      - conditions:
          - condition: trigger
            id: porte
        sequence:
          - set_conversation_response: "No, tutto in sicurezza!"
```

Se è scattato **«porte»**, risponde con una frase fissa.

### Perché `mode: parallel`

L'automazione può essere attivata più volte di seguito, per esempio dalla notifica e subito dopo dalla tua risposta. `parallel` fa sì che ogni attivazione venga gestita subito, senza aspettare la precedente.

## La versione reale

Nella demo le risposte sono finte. Nella versione reale, al posto delle risposte fisse, ci sono **azioni vere**:

| Nella demo | Nella versione reale |
|---|---|
| La conversazione parte da un pulsante | Parte da un **sensore di movimento**, ma solo se l'allarme è spento |
| «Attiva l'allarme» risponde e basta | **Attiva davvero l'allarme**, poi risponde |
| «Ci sono porte aperte?» risponde sempre «no» | **Controlla i sensori** e ti dice quali sono aperte |

Il file completo è [`esempi/esempio-reale.yaml`](../esempi/esempio-reale.yaml). Per usarlo cambia questi nomi con quelli dei tuoi dispositivi:

| Nel file | Cosa metterci |
|---|---|
| `binary_sensor.movimento_giardino` | Il tuo sensore di movimento |
| `alarm_control_panel.allarme_casa` | Il tuo allarme |
| `binary_sensor.porte_e_finestre` | Un gruppo con i sensori di porte e finestre. Si crea da **Aiutanti → Crea aiutante → Gruppo → Gruppo di sensori binari** |
| `notify.mobile_app_IL_TUO_IPHONE` | Il tuo iPhone |

I nomi esatti dei tuoi dispositivi li trovi in **Impostazioni → Dispositivi e servizi → Entità**.

### Le parti nuove, spiegate

**Partire solo quando serve:**

```yaml
          - condition: trigger
            id: movimento
          - condition: state
            entity_id: alarm_control_panel.allarme_casa
            state: disarmed
```

Ti chiama solo se c'è movimento **e** l'allarme è spento. Se l'allarme è già attivo non ti disturba.

**Fare davvero qualcosa, poi rispondere:**

```yaml
          - action: alarm_control_panel.alarm_arm_away
            target:
              entity_id: alarm_control_panel.allarme_casa
          - set_conversation_response: "Fatto! Allarme attivato."
```

Prima l'azione, poi la risposta. Al posto dell'allarme puoi mettere qualsiasi azione: accendere luci, chiudere tapparelle, avviare uno script.

**Una risposta che cambia in base alla casa:**

```yaml
          - if:
              - condition: state
                entity_id: binary_sensor.porte_e_finestre
                state: "on"
            then:
              - set_conversation_response: >-
                  Attenzione, sono ancora aperte:
                  {{ expand('binary_sensor.porte_e_finestre')
                     | selectattr('state', 'eq', 'on')
                     | map(attribute='name') | join(', ') }}.
            else:
              - set_conversation_response: "No, tutto in sicurezza!"
```

Se nel gruppo c'è almeno un sensore aperto, ti dice **quali**: «Attenzione, sono ancora aperte: Finestra bagno, Porta garage». Altrimenti risponde «No, tutto in sicurezza!».

## Rifallo con le tue idee

Lo schema è sempre lo stesso, qualunque cosa tu voglia fare:

1. **Un'attivazione che ti chiama**: un sensore, un orario, un evento. Manda una notifica con titolo `VOICE ASSISTANT` e il messaggio da leggerti.
2. **Una o più attivazioni a frase**, con le risposte che ti aspetti di dare.
3. **Per ogni frase**, le azioni da eseguire e la risposta da leggerti.

Qualche idea:

- **Lavatrice finita** → «Il bucato è pronto, vuoi che ti ricordi di stenderlo tra mezz'ora?» → «Sì, ricordamelo» → crea un promemoria.
- **Qualcuno al cancello** → «C'è qualcuno al cancello» → «Apri» → apre il cancello.
- **Finestra aperta con il riscaldamento acceso** → «La finestra della camera è aperta e il riscaldamento è acceso» → «Spegni il riscaldamento in camera» → lo spegne.
- **Esci di casa con le luci accese** → «Hai lasciato accese tre luci» → «Spegnile tutte» → le spegne.

Se non vuoi scrivere il codice a mano, chiedi a un'intelligenza artificiale di farlo per te, come spiegato nel [passo 4](04-frasi-personalizzate.md#fattele-scrivere-da-unintelligenza-artificiale). Dalle questa pagina come esempio.

---

[← Indietro](04-frasi-personalizzate.md) · [Avanti: Con l'intelligenza artificiale →](06-intelligenza-artificiale.md)
