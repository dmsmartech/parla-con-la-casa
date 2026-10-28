# 1. Prima di iniziare

[← Torna all'indice](../README.md)

## Cosa ti serve

| | Perché |
|---|---|
| **iPhone con iOS 27 o successivo** | Serve l'avvio «Quando ricevo una notifica» dell'app Comandi: il comando parte solo da una notifica di Home Assistant. |
| **App Comandi** | È già installata su ogni iPhone. Se l'hai cancellata, la riscarichi gratis dall'App Store. |
| **App Home Assistant** sull'iPhone | Riceve le notifiche della casa. Deve essere già collegata al tuo Home Assistant, con le notifiche attive. |
| **Accesso amministratore** a Home Assistant | Ti serve per creare il token e le automazioni. |

## Come funziona

Il comando fa sempre gli stessi passi, in ordine:

1. **Ascolta.** Dice «Ti ascolto» e accende il microfono. Quando fai una breve pausa, capisce che hai finito di parlare.
2. **Manda la frase a Home Assistant.** La frase arriva ad **Assist**, l'assistente vocale di Home Assistant.
3. **Legge la risposta.** L'iPhone ti legge ad alta voce quello che risponde Assist.
4. **Torna ad ascoltare**, da solo, senza toccare niente.

Prima del passo 1, se il comando è partito da una notifica, ti legge il testo della notifica. Così sai subito cosa è successo.

## Quando si ferma

La conversazione va avanti finché vuoi. Si chiude in tre casi:

- **Lo dici tu**, con frasi come «basta», «esci», «ho finito», «grazie», «niente grazie», «ciao», «arrivederci», «lascia perdere». L'elenco completo è nella [guida ai problemi](07-problemi.md#le-frasi-per-chiudere).
- **Tre silenzi di fila**: se non parli, dopo tre tentativi il comando si chiude da solo.
- **Tre «non ho capito» di fila**: se Assist non capisce tre richieste di seguito, il comando si chiude invece di insistere.

Ogni richiesta andata a buon fine azzera il conteggio di silenzi e «non ho capito».

## Cosa capisce Assist

Di base Assist capisce i comandi semplici sui dispositivi che hai esposto: «accendi la luce della cucina», «chiudi la tapparella», «che temperatura c'è in salotto?». Funziona seguendo dei **binari**: riconosce frasi costruite in un certo modo, come gli altri assistenti vocali senza intelligenza artificiale.

Il vantaggio di Home Assistant è che quei binari **li puoi allungare tu**. Puoi insegnargli qualsiasi frase, anche lunga e conversazionale, e decidere cosa deve fare e cosa deve rispondere. È proprio quello che fa l'esempio del video. Lo vediamo nel [passo 4](04-frasi-personalizzate.md).

Se colleghi un'intelligenza artificiale, i binari spariscono: parli come con una persona. Lo vediamo nel [passo 6](06-intelligenza-artificiale.md).

---

[Avanti: Installa il comando →](02-installa-il-comando.md)
