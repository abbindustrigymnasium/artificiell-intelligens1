# Kapitel 6: Möjligheter, risker och etik

> **I det här kapitlet lär du dig**
> - vilka möjligheter och risker AI för med sig på olika områden i samhället
> - hur bias kan uppstå, även när känsliga uppgifter tagits bort
> - varför transparens är ett etiskt dilemma
> - hur du bygger ett utvecklat och nyanserat resonemang

AI kan hjälpa läkare att upptäcka sjukdomar tidigare, och samma sorts teknik kan skapa en falsk video på en politiker dagen före ett val. Nästan varje fördel har en baksida. Den svåra frågan är sällan om AI är bra eller dåligt, utan vem som vinner, vem som förlorar och vem som bestämmer.

## Möjligheter och risker på fem områden

| Område | Möjligheter | Risker |
|---|---|---|
| **Demokratiskt** | Översättning och sammanfattning gör information tillgängligare för fler | Desinformation, deepfakes, övervakning, makt hos ett fåtal företag |
| **Socialt** | Hjälpmedel för personer med funktionsnedsättning, individuellt anpassad undervisning | Bias, ensamhet och beroende av chattbottar, försvagade färdigheter |
| **Ekonomiskt** | Högre produktivitet, nya tjänster och jobb | Vissa arbetsuppgifter försvinner, ojämn fördelning av vinsterna |
| **Miljömässigt** | Bättre elnät, väderprognoser, mindre svinn i produktion | Stor användning av el, vatten och hårdvara i datacenter |
| **Säkerhetsmässigt** | Snabbare upptäckt av bedrägerier och dataintrång | Bättre nätfiske, sårbara AI-system, militära system som fattar beslut snabbt |

### Energi och hållbar utveckling

Enligt Internationella energiorganet [IEA](https://www.iea.org/reports/energy-and-ai/executive-summary) använde världens datacenter ungefär 415 TWh el under 2024, cirka 1,5 procent av världens elanvändning. IEA räknar i sitt huvudscenario med att siffran mer än fördubblas till runt 945 TWh år 2030. Alla datacenter är inte AI, och prognoser kan slå fel, men siffrorna visar att frågan är relevant.

Samtidigt kan AI bidra till [FN:s globala hållbarhetsmål](https://sdgs.un.org/goals), till exempel genom att minska energianvändning i industrin. För att bedöma om nettoeffekten är positiv behöver du väga nytta mot kostnad i varje enskilt fall.

### Arbetsmarknaden

AI ersätter sällan ett helt yrke på en gång. Oftare påverkas enskilda arbetsuppgifter. Vissa blir snabbare, andra försvinner och nya tillkommer. Hur det slutar beror också på politiska beslut, utbildning och vad företag väljer att göra.

### Säkerhet: AI som angreppsmål

AI-tjänster kan också angripas. Vid **prompt injection** gömmer någon instruktioner i en text som modellen läser, till exempel på en webbsida, så att modellen gör något annat än vad användaren ville. Det är viktigt att tänka på om din app får hämta text utifrån eller anropa verktyg.

## Genomgånget exempel: en orättvis modell

Tänk dig ett påhittat antagningssystem som tränas på gamla beslut. I de gamla besluten behövde sökande från grupp 1 högre meriter för att bli antagna. Vi tar bort uppgiften om grupp, och lämnar bara meriter och postnummer. Postnumret råkar samvariera med gruppen.

```python
# Påhittat exempel: en modell lär sig en orättvisa från gamla beslut
import numpy as np
from sklearn.tree import DecisionTreeClassifier

rng = np.random.default_rng(1)
n = 2000
grupp = rng.integers(0, 2, n)              # grupp 0 eller 1
meriter = rng.normal(50, 10, n)            # samma fördelning för båda grupperna
postnummer = (grupp + (rng.random(n) < 0.1)) % 2   # stämmer med gruppen i 90 % av fallen

# Gamla beslut: grupp 1 behövde högre meriter för att bli antagen
gräns = np.where(grupp == 0, 50, 60)
antagen = (meriter > gräns).astype(int)

# Modellen får INTE se gruppen, bara meriter och postnummer
X = np.column_stack([meriter, postnummer])
modell = DecisionTreeClassifier(max_depth=4, random_state=1).fit(X, antagen)
förslag = modell.predict(X)

for g in [0, 1]:
    print(f"Grupp {g}: gamla beslut {antagen[grupp == g].mean():.0%} antagna, "
          f"modellen {förslag[grupp == g].mean():.0%} antagna")
```

```text
Grupp 0: gamla beslut 50% antagna, modellen 47% antagna
Grupp 1: gamla beslut 16% antagna, modellen 19% antagna
```

Båda grupperna har lika bra meriter, men modellen föreslår att 47 procent av grupp 0 och bara 19 procent av grupp 1 ska antas. Modellen har inte sett gruppen, men postnumret fungerar som en **ersättningsvariabel** (*proxy*). Bias är alltså inte bara en fråga om elaka programmerare. Den kan följa med i data från ett historiskt orättvist samhälle.

Vad kan man göra? Undersöka resultaten för olika grupper, granska data och ändra modellen eller beslutsprocessen. Men det finns inget enkelt svar på hur rättvisa ska mätas, eftersom olika mått på rättvisa kan stå i konflikt med varandra.

## Etiska dilemman och transparens

**Transparens** innebär att det går att förstå hur ett system fungerar och varför det gav ett visst svar. En stor modell är i praktiken en **svart låda**: vi kan se indata och utdata, men knappast följa hur miljarder tal ledde till svaret. Det ger dilemman:

- Ska ett sjukhus använda en modell som ger bättre resultat men inte kan förklara sig, eller en sämre modell som går att förstå?
- Ska ett företag berätta exakt hur modellen är tränad, om det samtidigt gör det lättare för andra att kopiera den?
- Ska du berätta att du har använt AI i en text? När räcker det med att bara använda det som stöd?

Andra dilemman handlar om **ansvar** (vem ansvarar när en självkörande bil kör fel?), **samtycke** (ska din text och dina bilder få användas för träning?) och **deepfakes** (var går gränsen mellan satir och skadlig förfalskning?). Organisationer som [UNESCO](https://www.unesco.org/en/artificial-intelligence/recommendation-ethics) och [OECD](https://oecd.ai/en/ai-principles) har tagit fram principer om bland annat rättvisa, transparens och mänsklig kontroll.

## Hur bygger du ett bra resonemang?

Det räcker inte att räkna upp risker. Ett bra resonemang visar orsaker, vem som påverkas och att det finns motstridiga intressen.

| Nivå | Vad det innebär | Exempel om AI och betygssättning |
|---|---|---|
| **Enkelt** | Nämner en möjlighet eller risk och en följd | AI kan rätta snabbt, men kan göra fel |
| **Utvecklat** | Förklarar orsaker och konsekvenser för flera parter | Lärare får mer tid, men modellen kan ge sämre resultat för elever som skriver på ett ovanligt sätt, eftersom träningsdatan består av andra texter |
| **Nyanserat** | Väger perspektiv mot varandra och visar när svaret beror på villkor | Som stöd vid övningsuppgifter kan nyttan väga tyngre än risken, men vid betyg krävs mänskligt ansvar, och det finns juridiska krav på hög risk |

Fem frågor som hjälper dig att komma längre:

1. Vem får nytta, och vem kan skadas?
2. Vad händer på kort och på lång sikt?
3. Vilka är alternativen, inklusive att inte använda AI?
4. Vad händer när systemet gör fel, och går felet att upptäcka?
5. Vilka lagar och normer berörs?

## Begrepp

- **Bias:** systematisk snedvridning i data eller modell
- **Proxy:** variabel som indirekt avslöjar något annat, till exempel gruppen
- **Transparens:** möjligheten att förstå hur ett system fungerar
- **Svart låda:** system där det inre beslutsfattandet är svårt att följa
- **Deepfake:** AI-skapad förfalskning av bild, ljud eller film
- **Prompt injection:** dolda instruktioner som lurar en språkmodell
- **Desinformation:** avsiktligt spridd felaktig information

## Koppling till projektet

I [AI LLMer](../projekt/ai-llmer/README.md) ska du reflektera över risker och möjligheter med just din app. I [AI - Projekt](../projekt/ai-projekt/README.md) ska du resonera om begränsningarna hos din lösning.

## Läs mer

- [IEA: Energy and AI](https://www.iea.org/reports/energy-and-ai)
- [UNESCO: rekommendation om AI-etik](https://www.unesco.org/en/artificial-intelligence/recommendation-ethics)
- [OECD:s AI-principer](https://oecd.ai/en/ai-principles)
- [FN:s globala mål](https://sdgs.un.org/goals)

[← Föregående](05-lagar-och-regler.md) | [Innehåll](../README.md) | [Nästa →](07-data-och-process.md)
