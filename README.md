# Parla con la casa

Un comando rapido per iPhone che trasforma le notifiche di Home Assistant in una conversazione a voce.

Succede qualcosa in casa, Home Assistant ti manda una notifica, e l'iPhone **te la legge ad alta voce e resta in ascolto**. Tu rispondi a voce, la casa esegue e ti risponde. Poi puoi chiedere altro, senza toccare il telefono, finché non dici «basta».

```
iPhone  › «Ho rilevato un movimento in giardino, ma l'allarme non è inserito.»
Tu      › «Attiva subito l'allarme!»
iPhone  › «Fatto! Allarme perimetrale attivato.»
Tu      › «Ci sono porte o finestre rimaste aperte?»
iPhone  › «No, tutto in sicurezza!»
Tu      › «Grazie, ho finito.»
```

> [!TIP]
> Nel video l'iPhone parla con **Assist**, l'assistente vocale di Home Assistant, che capisce le frasi che gli insegni tu con un'automazione: risponde all'istante, è gratis e funziona anche senza intelligenza artificiale. Nella guida trovi il codice completo per rifarlo a casa tua, collegato ai tuoi dispositivi. E se vuoi parlare in totale libertà, puoi collegarci anche un'AI.

## Scarica il comando

**[➜ Aggiungi «Parla con la casa» al tuo iPhone](https://www.icloud.com/shortcuts/df9651cbaa704b548ee2871ba8ff76cf)**

Poi segui la guida qui sotto: ti porta passo passo dall'installazione alla prima conversazione.

## La guida

| | Cosa trovi | Tempo |
|---|---|---|
| 1 | [**Prima di iniziare**](guida/01-prima-di-iniziare.md): cosa serve e come funziona | 3 min |
| 2 | [**Installa il comando**](guida/02-installa-il-comando.md): token, indirizzo e importazione | 10 min |
| 3 | [**Fallo partire da una notifica**](guida/03-avvio-da-notifica.md): l'avvio automatico | 5 min |
| 4 | [**Le frasi che vuoi tu**](guida/04-frasi-personalizzate.md): come Assist capisce i comandi e come insegnargli le tue frasi | 10 min |
| 5 | [**L'esempio del video, da rifare**](guida/05-esempio-del-video.md): l'automazione completa, spiegata riga per riga | 15 min |
| 6 | [**Con l'intelligenza artificiale**](guida/06-intelligenza-artificiale.md): conversare senza frasi preparate | 15 min |
| 7 | [**Se qualcosa non va**](guida/07-problemi.md): i problemi più comuni e come risolverli | |

Per la prima conversazione servono i passi **1**, **2** e **3**: il comando parte solo da una notifica di Home Assistant.

## Cosa serve, in breve

- Un **iPhone con iOS 27 o successivo**, con l'app **Comandi** (c'è già di serie).
- **Home Assistant** con l'**app Home Assistant** sull'iPhone, già collegata alla tua casa.
- Un account di Home Assistant con permessi da **amministratore**, per creare il token e le automazioni.

Non serve nessun abbonamento e nessun servizio a pagamento.

## Esempi pronti

- [`esempi/demo-del-video.yaml`](esempi/demo-del-video.yaml): l'automazione del video ridotta all'osso: abbiamo tolto la nostra logica e lasciato solo lo scheletro, con risposte fisse, così vedi come funziona e la adatti ai tuoi scopi. Si prova in 5 minuti e non tocca nessun dispositivo.
- [`esempi/esempio-reale.yaml`](esempi/esempio-reale.yaml): la stessa conversazione, ma con un sensore di movimento, un allarme e porte e finestre veri.

## Licenza

Distribuito con licenza [MIT](LICENSE).
