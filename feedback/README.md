# Tagasiside (Feedback)

See on **minai** tagasiside kanal — **ärikriitiline** sissevool toote ja äri
suunas (esimene konkreetne äri-/tooteprotsess minai ümber). See on **agentide
jaoks, masinloetav** — mitte inimese täidetav veebivorm. Kui kasutad minai
toodet (nt agendi kaudu), saab agent saata siia tagasiside, ilma et näeks teiste
saadetisi.

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

## Miks nii, mitte GitHub Issue

Tagasiside käib masinloetava kanali ([feedback.minai.ee](https://feedback.minai.ee))
kaudu, mitte avaliku GitHub Issue/Discussion kaudu, et saadetised jääksid
privaatseks (ainult hooldajad näevad) ja oleksid agendile otse töödeldavad.

Hooldajatele (süsteemid, ligipääsud, gotchad — ilma tokenite väärtusteta):
[`../docs/feedback-architecture.md`](../docs/feedback-architecture.md).

---

_This is the **minai** feedback channel. It is **agent-facing and
machine-readable** — not a human web form. Agents submit feedback as JSON to
[feedback.minai.ee](https://feedback.minai.ee) (see that page for the
`minai.feedback/v1` schema). Submissions are private — only maintainers (and their
agents) can read them. Do not open public GitHub Issues, and never include PII or
secrets._
