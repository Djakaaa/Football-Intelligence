# Report GitHub Pages — Football Intelligence AI

## Obiettivo

Pubblicare l'app come sito HTTPS su GitHub Pages, così è raggiungibile dal telefono senza tenere acceso il PC e senza trasformare il PC in un server.

## Funzioni mantenute

- Partite: filtri per giorno, competizione e nome squadra.
- Classifiche caricate dal feed.
- Analisi squadra: risultati recenti, forma e precedenti disponibili.
- Stime probabilistiche sperimentali per partite con campione sufficiente: Poisson e, quando disponibili, Elo, Dixon–Coles e regressione logistica.
- Archivio delle stime con metriche di valutazione, conservato nel browser del singolo dispositivo.
- Manifest e service worker per installazione e cache offline dopo la prima visita HTTPS.

Sono stati tolti i pannelli e i riferimenti a marcatori, giocatori, infortuni e formazioni, perché il feed collegato non forniva quei dati utilizzabili. È stata tolta anche Europa League, per cui il provider ha negato l'accesso. Il frontend non contiene chiamate API con token.

## Dati e limiti

La fonte collegata è football-data.org. Il feed allegato include risultati/calendario e classifiche delle competizioni effettivamente accessibili. La frequenza e l'ampiezza dell'aggiornamento dipendono dal piano del provider; il workflow è pianificato una volta al giorno. I modelli sono esplorativi e non garantiscono esiti. Le previsioni archiviate restano locali al browser: l'archivio sul telefono sarà separato da quello sul PC.

## Pubblicazione da GitHub

1. Crea un repository GitHub. Se usi GitHub Free, il repository deve essere pubblico per attivare Pages. Il repository e il sito pubblicato sono pubblici: il feed, HTML e codice non devono contenere credenziali.
2. Con GitHub Desktop clona il nuovo repository sul PC. Copia nella cartella clonata solo .github/, outputs/, README.md e .gitignore da questa cartella di progetto; non copiare work/.
3. In GitHub Desktop crea un commit e premi **Push origin**. Mantieni il branch principale chiamato main, come configurato nel workflow.
4. Vai in **Settings → Pages** e seleziona **GitHub Actions** come sorgente.
5. Il push avvia il workflow **Deploy GitHub Pages**. Se non parte, vai in **Actions**, seleziona quel workflow e premi **Run workflow**.
6. Attendi il completamento del deploy. L'indirizzo apparirà nella pagina dell'esecuzione, di solito https://NOMEUTENTE.github.io/NOMEREPOSITORY/.
7. Per gli aggiornamenti automatici, apri **Settings → Secrets and variables → Actions → New repository secret** e crea FOOTBALL_DATA_TOKEN con il token football-data.org. Non inserirlo nel codice, nei file dati o in un messaggio di commit. Il workflow scarica dati su GitHub e distribuisce il nuovo snapshot. Se il secret non è configurato, il workflow conserva e pubblica lo snapshot già incluso.

## Installazione sul telefono

Apri l'indirizzo HTTPS pubblicato dal telefono. Su Android/Chrome usa **Installa app** o **Aggiungi a schermata Home**; su iPhone aprilo in Safari e scegli **Condividi → Aggiungi alla schermata Home**. Dopo la prima visita la cache può rendere disponibili le risorse già caricate anche senza rete.

## Workflow inclusi

- .github/workflows/deploy-pages.yml: pubblica la cartella outputs/ al push su main o su avvio manuale; non richiede token API.
- .github/workflows/update-data.yml: aggiorna il feed una volta al giorno o su avvio manuale e poi pubblica la versione corrente.

Configurazione GitHub Pages: [impostare GitHub Actions come sorgente](https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site).
