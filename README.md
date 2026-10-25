# RADICATI · Worship Team — Black & White Edition

Webapp statica pronta per GitHub Pages. Design bianco e nero, schermata d'accesso condivisa, sessioni, repertorio, accordi trasponibili, player MP3 e stampa.

## Pubblicare online
1. Crea un repository pubblico GitHub denominato `radicati-worship-team`.
2. Carica **il contenuto estratto** dello ZIP nella radice del repository (non lo ZIP intero).
3. In Settings → Pages seleziona Deploy from a branch, branch `main`, folder `/(root)` e Save.
4. La URL sarà `https://TUO-UTENTE.github.io/radicati-worship-team/`.

## Accesso dimostrativo
Password iniziale: `Radicati2026!`

**ATTENZIONE:** questo login è un semplice filtro VISIVO nel browser (hash FNV incorporato nello script, stato salvato nel browser), **non** un sistema di sicurezza. Il repository pubblico, il file `repertoire.js` e ogni MP3 dentro `audio/` saranno accessibili pubblicamente anche senza il login. Non inserire informazioni riservate o file di cui non hai i diritti di distribuzione. Per controllo accessi reale usa Supabase Auth e archiviazione privata con policy RLS.

## Modificare la scaletta
Apri `repertoire.js`. In `sessions` puoi rinominare o aggiungere sessioni, e in ogni `songs` impostare:
- `title`: nome del brano
- `artist`: artista
- `key`: tonalità originale, es. `D`
- `bpm`: tempo
- `audio`: percorso come `audio/nome-brano.mp3` (metti il file in `audio/`)
- `chart`: sezioni indicate con `## STROFA`, accordi tra parentesi quadre come `[D]`, `[F#m]`, `[A/C#]`.

I brani di default sono **esempi inventati**, non rappresentano la scaletta della Conferenza Radicati.

## Cambiare la password
Nel file `index.html` trova `const PASSWORD_FNV='138af3cd'`. Sostituisci il valore con l'hash FNV-1a a 32 bit (esadecimale, 8 cifre) della password che scegli. Per esempio da Python:

```python
password='LA_TUA_PASSWORD'
h=2166136261
for c in password:
    h=((h ^ ord(c))*16777619)&0xffffffff
print(f'{h:08x}')
```

Per semplicità evita caratteri Unicode fuori dall'ASCII nella password; l'implementazione JS fa hashing delle unità UTF-16.

## Uso
Apri `index.html` in browser per un controllo rapido. Per testare i media con i percorsi relativi puoi usare un server locale (`python -m http.server 8000`). Il lettore rimane montato durante la navigazione e l'audio non si interrompe quando apri altre schede brano.
