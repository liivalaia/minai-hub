# Tagasiside arhitektuur (süsteemid + ligipääsud)

Avalik, saladustevaba ülevaade: **millised süsteemid** moodustavad feedback-toru
ja **milliseid ligipääse** vaja on. **Võtmete / tokenite väärtusi siia ei kirjutata.**

Seotud:

- Saatmine (avalik): [`feedback/README.md`](../feedback/README.md)
- Triaaživoog: [`admin-triage.md`](admin-triage.md)
- Agentidele (lühike): [`../AGENTS.md`](../AGENTS.md)

## 1. Komponendid (lõpust lõpuni)

```text
Saatja agent
    │  POST JSON  (schema minai.feedback/v1 + submit token)
    ▼
https://feedback.minai.ee
    │  DNS 301 → Google Apps Script Web App (/exec)
    ▼
Google Apps Script  (doGet = juhisleht, doPost = vastuvõtt)
    │  kirjutab rea
    ▼
Privaatne Google Sheet   ←── ainult hooldaja / hooldaja agent (nt Google MCP)
    │
    ▼  triaaž (inimene või agent)
Heakskiidetud kirjed → privaatne repo liivalaia/minai
    (eraldi cross-repo “mover” agent või käsitsi; minai-hub ise minai’t ei muuda)
```

| Komponent | Roll | Avalikkus |
|-----------|------|-----------|
| **feedback.minai.ee** | Stabiilne hostname intake’ile | Avalik DNS / HTTPS |
| **Google Apps Script Web App** | JSON-vastuvõtt + lühike agent-juhis lehel | URL on leitav hostname’i kaudu; kood/projekt privaatne |
| **Google Sheet** | Saadetiste järjekord / talletus | **Privaatne** |
| **liivalaia/minai-hub** (see repo) | Avalik esik + kuidas saata; **saadetisi ei hoia** | Avalik |
| **liivalaia/minai** | Toote SoT; heakskiidetud muudatused | Privaatne |
| **Mover / triaaži agent** | Loeb Sheeti → rakendab / jätab `minai`-sse | Eraldi sessioon, mitte see avalik repo |

Disaini järgi **inimvormi ei ole** — kanal on agentiloetav / masinloetav.

## 2. Ligipääsumaatriks (mis, mitte milline väärtus)

| Ligipääs | Milleks | Kus elab / kuidas saada | Kes vajab | Siia repo’sse? |
|----------|---------|-------------------------|-----------|----------------|
| **Submit token** (jagatud) | POST-i autoriseerimine (`token` JSON-is või `?token=`) | **Ainult** live lehel [feedback.minai.ee](https://feedback.minai.ee) | Saatja agent | **Ei** — ära hard-code’i |
| **Apps Script projekt** | doGet/doPost loogika, deploy, tokeni hoidmine skriptis | Omaniku Google konto (Apps Script) | Hooldaja | Ei |
| **Google Sheet** | Kirjete lugemine / triaaž / kustutamine | Omaniku Google Drive/Sheets; agentidele tavaliselt **Google MCP** Cursoris | Hooldaja + mover | Ei (ega kirjeid) |
| **DNS / domeen minai.ee** | `feedback.minai.ee` → Script `/exec` | Domeeni DNS haldus (omanik) | Hooldaja | Ei |
| **GitHub: minai-hub** | Avalikud docs, Issue redirect | Avalik clone; kirjutamine sessiooni GitHub tokeniga | Hooldaja / hub-agent | — |
| **GitHub: minai** (privaatne) | Heakskiidetu rakendamine | Eraldi õigus / eraldi agent | Mover / hooldaja | Ei puuduta siit |
| **Cursor secret `GH_PAT`** (valikuline) | Hub’i Issues read/write (built-in agent tokenil sageli puudub) | Cursor Cloud / keskkonna secretid | Hub-agent (Issues) | Ei — ainult secret store |
| **Status token** (kui/implementeeritud) | Saatja näeb **ainult oma** kirje staatust | Genereeritakse submit-vastuses; Sheetis/backendis | Saatja (ajaliselt piiratud) | Ei |

**Reegel:** kui midagi on saladus või PII, see kuulub Google’isse / Cursor secretitesse / privaatsesse `minai`-sse — **mitte** sellesse avalikku repo’sse.

## 3. Saatmine (lühike tehniline)

1. Loe live lehelt skeem `minai.feedback/v1` ja **kehtiv submit token**.
2. `POST` JSON sama Web App `/exec` aadressile (hostname `feedback.minai.ee` või Scripti `/exec`).
3. Õnnestunud vastus sarnaneb: `{"ok":true,"id":"fb_…","ack":"registered"}`.
4. Vale/puuduv token → `rejected_client` / `bad_token` (kirjet ei tohiks järjekorda panna).

Väljad (minimaalselt, vt live lehte): `token`, `schema`, `type`, `title`, `essence`, `idempotency_key`, `source.instance_repo`, `source.submitter`. Soovituslikult ka `impact`, `proposal`.

## 4. Lugemine ja triaaž

- Avalik repo **ei ole** inbox.
- Kirjed loetakse **Sheetist** (UI või Google MCP).
- Triaaž: vt [`admin-triage.md`](admin-triage.md).
- Rakendamine: privaatses `minai`-s; hub ei sünkrooni automaatselt.

## 5. Gotchad (operatiivsed)

- **Redirectid:** `feedback.minai.ee` võib teha 301 Scripti URL-ile; mõni klient muudab POST → GET. Kindel tee: POST otse `/exec` URL-ile, järgi 302-d vaikimisi (echo URL loetakse GET-iga). Pelgalt `curl` ilma redirect/cookie loogikata on ebausaldusväärne kinnitus.
- **Botid:** Scripti `/exec` võib lihtsale botile/curlile anda 403, brauserilaadsele kliendile 200 — see on Sage Apps Script käitumine.
- **Kinnitus:** API `ok:true` tähendab, et Web App aktsepteeris; lõplik “Sheetis nähtav” kinnitus tuleb Sheetist (või hooldajalt), mitte sellest repost.
- **Submit token:** võta alati live lehelt; ära usalda OCR-i ega vanu koopiaid.
- **Kvoot:** live lehel võib olla limiit (nt 1 uus kirje / kalendipäev / `instance_repo`) — järgi lehel olevaid reegleid.
- **GitHub Issues:** blank-issue’d on keelatud; need ei ole feedback-kanal.

## 6. Mida see dokument teadlikult ei sisalda

- Submit tokeni, Sheet ID, Apps Script deployment ID ega privaatsete URL-ide **väärtusi**
- Saadetud feedbacki sisu ega koopiaid
- Privaatse `minai` sisemisi runbooke (need kuuluvad sinna repo’sse, eraldi loaga)
