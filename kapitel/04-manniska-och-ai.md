# Kapitel 4: Människa och artificiell intelligens

> **I det här kapitlet lär du dig**
> - likheter och skillnader mellan mänsklig och artificiell intelligens
> - hur enkla AI-lösningar och människor löser samma problem på olika sätt
> - i vilka situationer AI är bättre än människan, och tvärtom
> - varför frågan om AI "förstår" fortfarande är omdiskuterad

Ett litet barn som har sett två katter kan peka ut katter resten av livet. En bildmodell kan behöva tusentals bilder för att lära sig samma sak, men sedan kan den granska en miljon bilder innan barnet ens har ätit frukost. Människor och AI är bra på olika saker, och det är sällan rättvist att bara fråga vem som är "smartast".

## Likheter och skillnader

Neurala nätverk är inspirerade av hjärnan. Båda består av många enkla enheter som samverkar, och i båda ändras kopplingarnas styrka när något lärs in. Likheten är ändå ganska ytlig: en nervcell är mycket mer komplicerad än en nod i en datormodell.

| Aspekt | Människa | Dagens AI |
|---|---|---|
| **Inlärning** | Lär sig ofta av få exempel och i ett sammanhang | Behöver ofta väldigt mycket data |
| **Kropp och omvärld** | Lär sig genom kropp, sinnen och andra människor | Lär sig oftast från data som samlats in i förväg |
| **Energi** | Hjärnan använder ungefär [20 watt](https://www.nist.gov/blogs/taking-measure/brain-inspired-computing-can-help-us-create-faster-more-energy-efficient) | Träning av stora modeller kräver stora datacenter |
| **Byggstenar** | Runt [86 miljarder nervceller](https://pubmed.ncbi.nlm.nih.gov/19226510/) | Beror på modellen, ofta miljarder justerbara tal |
| **Minne** | Glömmer, men kan koppla ihop erfarenheter | Kan lagra exakt, men bara det som finns i modellen eller kontexten |
| **Fel** | Blir trött och påverkas av känslor och fördomar | Tröttnar inte, men kan göra oväntade och konstiga fel |
| **Sunt förnuft** | Förstår fysik och människor intuitivt | Saknas ofta utanför träningsdatan |
| **Mål och ansvar** | Kan välja egna mål och hållas ansvarig | Följer mål människor gett den, och ansvaret ligger hos människor |
| **Upplevelser** | Har medvetande och känslor | Det finns inga belägg för att dagens AI upplever något |

## Ett genomgånget experiment: siffror

Vi tränar ett neuralt nätverk att känna igen handskrivna siffror, och ändrar två saker: hur mycket data det får, och hur testbilderna ser ut. Du behöver inte förstå varje rad än. Kapitel 9 förklarar neurala nätverk.

```python
# Hur mycket träningsdata behöver modellen, och vad händer med ovanliga bilder?
from sklearn.datasets import load_digits
from sklearn.model_selection import train_test_split
from sklearn.neural_network import MLPClassifier

siffror = load_digits()
X = siffror.data / 16      # gör alla pixelvärden till tal mellan 0 och 1
y = siffror.target
X_tr, X_te, y_tr, y_te = train_test_split(X, y, test_size=0.3, random_state=42, stratify=y)

for antal in [10, 50, 200, len(X_tr)]:
    modell = MLPClassifier(hidden_layer_sizes=(50,), max_iter=800, random_state=42)
    modell.fit(X_tr[:antal], y_tr[:antal])
    print(f"{antal:>5} träningsbilder: {modell.score(X_te, y_te):.2f} rätt på testbilder")

# Samma testbilder med omvända färger: ljusa siffror blir mörka
omvända = 1 - X_te
print(f"Omvända färger:      {modell.score(omvända, y_te):.2f} rätt på testbilder")
```

```text
   10 träningsbilder: 0.52 rätt på testbilder
   50 träningsbilder: 0.78 rätt på testbilder
  200 träningsbilder: 0.94 rätt på testbilder
 1257 träningsbilder: 0.98 rätt på testbilder
Omvända färger:      0.00 rätt på testbilder
```

Modellen blir bättre med mer data, och till slut klarar den 98 procent av testbilderna. Men när ljust och mörkt byter plats faller den till 0 procent på just de här bilderna. En människa skulle knappt märka skillnaden. Modellen har inte lärt sig vad en sjua är. Den har lärt sig ett mönster av siffervärden i just den sortens bilder den har sett.

Du kan också jämföra hur samma problem löses på olika sätt.

| Problem | Så löser människan det | Så löser AI det |
|---|---|---|
| **Känna igen en siffra** | Tittar på formen, klarar även ovanliga stilar | Räknar med pixelvärden och lär sig från exempel |
| **Spelet Nim** (kapitel 10) | Upptäcker en strategi och förklarar den | Går igenom alla möjliga drag |
| **Kortaste rutten** (kapitel 10) | Ser mönster och gissar en bra rutt | Söker systematiskt eller gör många små förbättringar |
| **Skriva en text** | Vet vad hen vill säga och till vem | Räknar fram en trolig fortsättning |

## När är AI bättre, och när är människan bättre?

AI har ofta övertaget när uppgiften har tydliga regler, mycket data och behov av snabbhet och uthållighet:

- Spel med tydliga regler, som schack och go.
- Att söka igenom stora mängder text eller bilder.
- Att upprepa samma kontroll miljontals gånger utan att tappa koncentrationen.
- Att hitta mönster i data med väldigt många variabler.

Människan har ofta övertaget när situationen är ny, otydlig eller handlar om värderingar:

- Att klara helt nya situationer med få exempel.
- Att avgöra vad som är rätt och rimligt i ett svårt fall.
- Att förstå känslor, ironi och sociala sammanhang på djupet.
- Att ta ansvar för ett beslut och förklara det för den som drabbas.
- Att använda händer och kropp i oförutsägbara miljöer.

Listan är inte huggen i sten. Vissa saker som länge ansågs vara mänskliga är AI numera bra på, till exempel att skriva flytande text. Därför är det klokt att alltid fråga *vilken* människa, *vilken* AI och *vilken* uppgift du jämför.

## Förstår AI?

**Turingtestet** kommer från Alan Turings artikel från 1950. Tanken är att en maskin kan betraktas som intelligent om en människa inte kan skilja den från en annan människa i ett skriftligt samtal.

Filosofen John Searle argumenterade 1980 emot det med sitt tankeexperiment **det kinesiska rummet**. Föreställ dig att du sitter i ett rum och följer en regelbok för att svara på kinesiska tecken, utan att kunna kinesiska. Utifrån verkar du kunna språket, men du förstår ingenting. Är en språkmodell som rummet?

Det finns olika svar. Vissa menar att modeller bara återger statistiska mönster. Andra menar att det krävs någon form av intern representation av världen för att kunna förutsäga text så bra, och att det är ett slags förståelse. Frågan är inte avgjord. Du kan utveckla din egen ståndpunkt, så länge du stöder den med exempel.

## Människa och AI tillsammans

I praktiken handlar det sällan om antingen eller. En läkare som använder AI som stöd för bildgranskning kan få hjälp att upptäcka sådant som annars skulle ha missats, men läkaren behöver fortfarande bedöma om förslaget är rimligt. En risk i samspelet är **automationsbias**: att man litar för mycket på datorns förslag och slutar tänka själv.

Du kan använda de här frågorna för att göra en bra jämförelse:

1. Vilken uppgift gäller det, och hur mäter vi vem som är bäst?
2. Hur lär sig människan respektive AI:n, och av vad?
3. Hur ser felen ut, och hur allvarliga är de?
4. Vem bär ansvaret om något går fel?
5. Skulle en kombination av människa och AI bli bättre?

## Begrepp

- **Mänsklig intelligens:** förmågan att lära, förstå, anpassa sig och agera med hjälp av hjärna, kropp och erfarenheter
- **Turingtest:** idé om att bedöma en maskins intelligens genom samtal
- **Det kinesiska rummet:** tankeexperiment om att följa regler utan att förstå
- **Automationsbias:** att överdrivet lita på förslag från datorer
- **Generalisering:** att klara nya fall som liknar eller skiljer sig från träningsfallen

## Testa dig själv

1. Nämn två likheter och tre skillnader mellan människa och AI.
2. Varför föll modellens resultat med omvända färger?
3. Ge ett exempel på en uppgift där AI är bättre än människan, och förklara varför.
4. Ge ett exempel på en uppgift där människan är bättre än AI, och förklara varför.
5. Vad försöker Searles kinesiska rum visa?
6. Vad är automationsbias, och hur kan det minskas?

## Koppling till projektet

Reflektionen i [AI LLMer](../projekt/ai-llmer/README.md) ska jämföra hur en LLM och en människa lär sig, förstår och gör fel. Den här frågelistan är ett bra sätt att strukturera den.

## Läs mer

- [Artikel om antalet nervceller i hjärnan](https://pubmed.ncbi.nlm.nih.gov/19226510/)
- [NIST om hjärnans energieffektivitet](https://www.nist.gov/blogs/taking-measure/brain-inspired-computing-can-help-us-create-faster-more-energy-efficient)

[← Föregående](03-bygga-med-llm.md) | [Innehåll](../README.md) | [Nästa →](05-lagar-och-regler.md)
