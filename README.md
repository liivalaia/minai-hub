# minai-hub

> Avalik esik minai ümber. / The public front door around minai.

**minai-hub** on avalik "esik/hoov" privaatse **minai** projekti ümber. See ei ole
toote lähtekood ega tõeallikas (SoT) — kood ja tootesisu elavad privaatselt.
Siin on ainult see, mis on mõeldud avalikuks: lühike tutvustus ja **Tagasiside**
kanal. Tagasiside on **ärikriitiline** — esimene konkreetne äri- ja tootega
seotud protsess minai ümber (signaal → triaaž → toode).

- **minai** (privaatne) — toode ise; kood ja sisu ei ole siin avaldatud.
- **minai-hub** (see repo, avalik) — avalik uks + tagasiside vastuvõtt.

## Tagasiside / Feedback

Vearaport, funktsiooni soov või templeidi idee? Tagasiside minaile on
**agentiloetav / masinloetav** — see saadetakse agendi kaudu JSON-ina, mitte
inimvormina:

➡️ **[feedback.minai.ee](https://feedback.minai.ee)**

Täpsem juhis: [`feedback/`](feedback/).

Oluline:

- **Avalik ei näe teiste saadetisi.** Tagasiside läheb privaatselt minai
  hooldajatele; siia repo't midagi ei salvestata avalikult.
- **Ära ava avalikku GitHub Issue't** — tagasiside käib ainult
  [feedback.minai.ee](https://feedback.minai.ee) kaudu.

## Mida MITTE saata

Palun ära lisa tagasisidesse:

- **Isikuandmeid (PII)** — nimi, e-post, telefon, aadress, isikukood vms.
- **Saladusi** — paroolid, API-tokenid, ligipääsuvõtmed, privaatsed URL-id.

Ära lisa isikuandmeid — jäta need välja.

## Adminile

Hooldajad loevad tagasisidet **privaatsest talletusest** → teevad **triaaži**
(bug / feature / templeidi ettepanek, heaks või tagasi) → rakendavad
heakskiidetu **käsitsi privaatsesse `minai`'sse**. Vt
[`docs/admin-triage.md`](docs/admin-triage.md).

Süsteemid ja ligipääsud (ilma saladuste väärtusteta):
[`docs/feedback-architecture.md`](docs/feedback-architecture.md).

---

_This repo is the public front door around the private **minai** project. Feedback
(bug reports, feature/template ideas) is **agent-facing and machine-readable**: it
is submitted as JSON via [feedback.minai.ee](https://feedback.minai.ee), not a
human form. Submissions are not publicly visible — only maintainers (and their
agents) read them. Do not open public GitHub Issues, and never include PII or
secrets._
