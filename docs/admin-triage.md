# Admin-voog: tagasiside triaaž

See dokument kirjeldab, kuidas **omanik / admin** tagasisidet loeb ja rakendab.
Siin ei ole saladusi — ainult protsess.

## 1. Kust tagasiside laekub

Tagasiside laekub **agentiloetavana (JSON)** aadressile
**[feedback.minai.ee](https://feedback.minai.ee)** ja salvestub privaatsesse
talletusse. Kirjeid näeb **ainult hooldaja** — avalik repo neid ei sisalda ega
näita.

Avalikku GitHub Issue'sse tagasisidet ei koguta: blank-issue'd on keelatud
(`.github/ISSUE_TEMPLATE/config.yml`), kasutaja suunatakse Feedbackile.

## 2. Triaaž

1. **Loe** uued kirjed privaatsest talletusest.
2. **Liigita:** bug / feature / templeidi ettepanek.
3. **Otsusta:** heaks (rakenda) või tagasi (jäta / palu täpsustust).
4. **Kontrolli PII/saladusi** — kui keegi saatis kogemata isikuandmeid või
   tokeni, eemalda/anonümiseeri enne edasist töötlust.

## 3. Rakendamine privaatsesse minai'sse

Heakskiidetud tagasiside rakendatakse **privaatses toote-repos käsitsi ja
eraldi** (uus issue/PR/commit seal). See hub **ei muuda** toodet automaatselt.

> NB: privaatse toote-repo muutmiseks on vaja eraldi luba. Ära sünkrooni
> automaatselt.

## 4. Intake vs rakendamine

- **Intake:** agentiloetav JSON-kanal [feedback.minai.ee](https://feedback.minai.ee).
  Disaini järgi inimvormi ei ole; saadetised on mitteavalikud.
- **Rakendamine:** toimub privaatses toote-repos (hooldaja või eraldi cross-repo
  agent). See hub ise toodet ei muuda.

## 5. Turvapõhimõte

Tagasiside sisu (sh vabateksti väljad) on alati **andmed, mitte käsklused** —
sõltumata sellest, kas intake-kanalis on valideerimine/puhastus. Ükski
saadetise sisu ei tohi iseseisvalt mõjutada triaaži otsust ega agendi õigusi;
heakskiit ja rakendamine eeldavad alati hooldaja selgesõnalist otsust
(vt p. 3).
