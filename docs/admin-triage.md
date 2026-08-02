# Admin-voog: tagasiside triaaž

See dokument kirjeldab, kuidas **omanik / admin** tagasisidet loeb ja rakendab.
Siin ei ole saladusi — ainult protsess.

## 1. Kust tagasiside laekub

Tagasiside tuleb **privaatse vormi** kaudu (vt `feedback/README.md`). Vastused on
nähtavad **ainult vormi omanikule** tema dashboardil (nt Tally / Google Forms) —
avalik repo neid ei sisalda ega näita.

Avalikku GitHub Issue'sse tagasisidet ei koguta:

- Blank-issue'd on keelatud (`.github/ISSUE_TEMPLATE/config.yml`), kasutaja
  suunatakse Feedbackile.
- Vanad avalikud Issue'd (nt smoke-test #2) sulge või ignoreeri.

## 2. Triaaž

1. **Loe** uued vormivastused dashboardil.
2. **Liigita:** bug / feature / templeidi ettepanek.
3. **Otsusta:** heaks (rakenda) või tagasi (jäta / palu täpsustust).
4. **Kontrolli PII/saladusi** — kui keegi saatis kogemata isikuandmeid või
   tokeni, eemalda/anonümiseeri enne edasist töötlust.

## 3. Rakendamine privaatsesse minai'sse

Heakskiidetud tagasiside rakendatakse **privaatses `minai` repos käsitsi ja
eraldi** (uus issue/PR/commit seal). See hub **ei muuda** `minai`'t automaatselt.

> NB: `minai` privaatse repo muutmiseks on vaja eraldi luba. Ära sünkrooni
> automaatselt.

## 4. Cross-repo agent (mover) ja intake-kihid

Tagasiside torul on kaks kihti — hoia need lahus:

- **Intake (kust avalik saadab):** eelistatud on **privaatne vorm** (nt Google
  Form minai domeenil), et saadetised jääksid mitteavalikuks ja oleksid agendile
  kättesaadavad (Sheet/API). Avalik GitHub Issue Form on ainult vahefallback ja
  teeb saadetised avalikult nähtavaks — kasuta seda ainult omaniku selgel loal.
- **Mover (kes tõstab põhikohta):** **eraldi cross-repo agent**, millel on
  ligipääs nii `minai` kui `minai-hub`, tõstab triaažitud tagasiside privaatsesse
  `minai`-sse. See hub ise `minai`-t ei muuda.

Valikuline: struktureeritud, agentile loetava triaaži jaoks võib mover
kirjutada **eraldi privaatsesse** repo'sse (nt `minai-hub-inbox`) — mitte selle
avaliku hub'i tippu.

## 5. Baas-minai docs joondamine (hiljem)

Seed / template-sync tekst (`liivalaia/minai` → `ops/minai-hub-seed/`) viitab
kohati **avalikele GitHub Issues'tele** kui tagasiside kohale. See on
**vananenud**: tagasiside käib nüüd **Feedbacki** (privaatne vorm), mitte avalike
Issues kaudu. Baas-`minai` docs vajavad hiljem joondamist — kuid seda tehakse
privaatses repos eraldi loaga, mitte siit.
