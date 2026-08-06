# Tagasiside (Feedback)

See on **minai** tagasiside kanal. See on **agentide jaoks, masinloetav** — mitte
inimese täidetav veebivorm. Kui kasutad minai toodet (nt agendi kaudu), saab
agent saata siia tagasiside, ilma et näeks teiste saadetisi.

## Kuidas tagasiside saadetakse

Agent saadab tagasiside **masinloetavana (JSON)** aadressile:

➡️ **[feedback.minai.ee](https://feedback.minai.ee)**

Sellel lehel on kirjas täpne skeem (`minai.feedback/v1`) ja saatmise reeglid.
Sobib nii **vearaportile (bug)**, **funktsiooni soovile (feature)** kui ka
**templeidi ettepanekule**.

## Privaatsus

- Saadetist **ei näe avalikult keegi** — ainult minai hooldajad (ja nende
  agendid). Seda ei salvestata sellesse avalikku repo'sse.
- **Ära ava avalikku GitHub Issue't** — see oleks kõigile nähtav.

## Mida MITTE saata

- **Isikuandmeid (PII):** nimi, e-post, telefon, aadress, isikukood jne.
- **Saladusi:** paroolid, tokenid, võtmed, privaatsed lingid.

## Turvalisus

Tagasiside kogub kirjeid privaatsesse talletusse. Sellest ei toimu automaatset
ega otsest rakendamist tootmiskeskkonda ega privaatsesse minai reposse —
rakendamine käib alati käsitsi, hooldaja otsusel (vt
[`docs/admin-triage.md`](../docs/admin-triage.md)).

## Miks nii, mitte GitHub Issue

Tagasiside käib masinloetava kanali ([feedback.minai.ee](https://feedback.minai.ee))
kaudu, mitte avaliku GitHub Issue/Discussion kaudu, et saadetised jääksid
privaatseks (ainult hooldajad näevad) ja oleksid agendile otse töödeldavad.

---

_This is the **minai** feedback channel. It is **agent-facing and
machine-readable** — not a human web form. Agents submit feedback as JSON to
[feedback.minai.ee](https://feedback.minai.ee) (see that page for the
`minai.feedback/v1` schema). Submissions are private — only maintainers (and their
agents) can read them. There is no automatic pipeline from a submission into
production or the private repo — applying feedback always requires a
maintainer's manual decision. Do not open public GitHub Issues, and never
include PII or secrets._
