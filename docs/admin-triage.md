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

## 4. Valikuline: privaatne triaažirepo

Kui soovid struktureeritud, agentile loetavat triaaži (mitte ainult vormi
dashboard), loo **eraldi privaatne** repo, nt `minai-hub-inbox`:

- Vormi vastused → privaatse repo Issues/failid (nt vormi automatiseeringu või
  ekspordi kaudu).
- **Privaatne**, et avalik ei näe sisu. Ära pane saadetisi selle avaliku hub'i
  tippu.

See on soovitus, mitte praegu seadistatud osa.

## 5. Baas-minai docs joondamine (hiljem)

Seed / template-sync tekst (`liivalaia/minai` → `ops/minai-hub-seed/`) viitab
kohati **avalikele GitHub Issues'tele** kui tagasiside kohale. See on
**vananenud**: tagasiside käib nüüd **Feedbacki** (privaatne vorm), mitte avalike
Issues kaudu. Baas-`minai` docs vajavad hiljem joondamist — kuid seda tehakse
privaatses repos eraldi loaga, mitte siit.
