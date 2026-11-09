# Projekt: AI LLMer

## Syfte

Stora språkmodeller finns i allt från skolarbete till kundtjänst och programmering. I det här projektet tar du reda på hur de fungerar på insidan och bygger ett eget program som använder en språkmodell via ett API. Du undersöker också vad som skiljer en språkmodell från mänsklig intelligens, vilka lagar som gäller och vilka möjligheter och risker tekniken för med sig.

## Koppling till kursen

**Kriterier i vanliga ord**

| Kriterium | E | C | A |
|---|---|---|---|
| Du jämför mänsklig och artificiell intelligens | enkla jämförelser | välgrundade jämförelser | välgrundade och nyanserade jämförelser |
| Du redogör för lagar och andra bestämmelser om AI | godtagbart | utvecklat | välutvecklat |
| Du resonerar om möjligheter och risker med AI och konsekvenser för samhället | enkla resonemang | utvecklade resonemang | utvecklade och nyanserade resonemang |

**Centralt innehåll** som behandlas: generativ AI och NLP, jämförelser mellan AI och människa, situationer där den ena är överlägsen den andra, normer och lagar, etiska dilemman samt möjligheter och risker för samhället.

**Kapitel som förbereder**

| Kapitel | Används till |
|---|---|
| [1: Vad är AI?](../../kapitel/01-vad-ar-ai.md) | Grundbegrepp |
| [2: Hur fungerar en språkmodell?](../../kapitel/02-sprakmodeller.md) | Tokens, embeddings, träning |
| [3: Bygg program med en språkmodell](../../kapitel/03-bygga-med-llm.md) | Din app |
| [4: Människa och AI](../../kapitel/04-manniska-och-ai.md) | Jämförelsen i din reflektion |
| [5: Lagar, regler och normer](../../kapitel/05-lagar-och-regler.md) | AI-förordningen och GDPR |
| [6: Möjligheter, risker och etik](../../kapitel/06-mojligheter-och-risker.md) | Reflektionen om risker |

## Vad du ska göra

1. Arbeta igenom lektionerna i kursmaterialet: första AI-appen, promptteknik, strukturerad utdata, RAG och verktygsanrop.
2. Diskutera och jämför hur en LLM och en människa lär sig, förstår och gör fel.
3. Sätt dig in i EU:s AI-förordning och GDPR och vad de betyder för AI-tjänster.
4. Bygg ett eget litet program som använder en LLM via API och löser ett verkligt eller kreativt problem.
5. Redovisa projektet tillsammans med en reflektion om möjligheter, risker och regler kopplade till din app.

## Krav och leverabler

- Ett eget program som använder en språkmodell via ett API.
- En redovisning där du visar appen och berättar hur den använder en LLM och vilka risker du ser.
- En skriftlig reflektion om människa och AI, lagar samt möjligheter och risker.
- Inlämning av kod och reflektion.

API-nycklar får aldrig finnas i koden du lämnar in.

## Arbetsgång

| Lektion | Innehåll |
|---|---|
| 1 | Kursstart: vad generativ AI och en LLM är, tokens och hur modellen förutsäger nästa ord. Testa och jämför några chattbottar (lektion 01 i kursmaterialet). |
| 2 | Hur en LLM tränas: förträning, finjustering och embeddings. Diskussion om hur modellens "förståelse" skiljer sig från en människas. |
| 3 | Kom igång med kodmiljön och skriv din första AI-app med systemmeddelande och temperature (lektion 02). |
| 4 | Promptteknik (lektion 03): zero-shot, few-shot och chain-of-thought. Testa och jämför prompter i din egen kod. |
| 5 | Strukturerad utdata (lektion 04): få modellen att svara i JSON så att programmet kan använda svaret. |
| 6 | RAG (lektion 05): låt modellen svara utifrån egen data och bygg en enkel RAG-lösning. |
| 7 | Verktygsanrop (lektion 06) och en kort titt på MCP (lektion 07). |
| 8 | Lagar och regler: AI-förordningen och dess riskklasser, GDPR och personuppgifter i AI-tjänster. Diskussion i grupp. |
| 9 | Möjligheter och risker: hallucinationer, bias, deepfakes, arbetsmarknad och energi. Välj idé för ditt eget projekt. |
| 10 | Eget projekt: planera appen (problem, användare, prompt och API) och börja bygga. |
| 11 | Eget projekt: bygg vidare. Avstämning med läraren om hur långt du kommit. |
| 12 | Eget projekt: färdigställ huvudfunktionerna och testa appen. Fundera på vilka risker och regler som gäller för din app. |
| 13 | Färdigställ projektet och förbered redovisningen. Skriv reflektionen om människa och AI, lagar samt möjligheter och risker. |
| 14 | Redovisning: visa din app för klassen och berätta hur den använder en LLM och vilka risker du ser. |
| 15 | Fortsatt redovisning, inlämning av kod och reflektion samt gemensam avslutning. |

## Bedömning

Du bedöms på hur väl du förklarar hur språkmodeller fungerar, hur säkert du använder en LLM för att lösa problemet i ditt program, och hur väl du resonerar om skillnader mellan människa och AI, lagar som AI-förordningen och GDPR samt möjligheter och risker för samhället. Underlaget är ditt program, din redovisning och din reflektion.

## Material

- [Generativ AI: kursrepo](https://github.com/abbjetmus/Generative-AI-Hitachigymnasiet)
- [Generative AI with JavaScript](https://github.com/abbjetmus/generative-ai-with-javascript)
- [Lektionerna 01–08](https://github.com/abbjetmus/generative-ai-with-javascript/tree/main/lessons)
- [Lektion 05 om RAG](https://github.com/abbjetmus/generative-ai-with-javascript/tree/main/lessons/05-rag)

Kursmaterialet använder på flera ställen GitHub Models, som har [stängts av GitHub](https://docs.github.com/en/github-models/quickstart). Fråga läraren vilken tjänst och vilka inställningar som gäller, och se avsnittet om din första app i [kapitel 3](../../kapitel/03-bygga-med-llm.md).

## Tips

- Börja litet. En app som gör en sak bra är bättre än en stor som inte fungerar.
- Skriv ner vilka testfrågor du använder, så ser du om appen blir bättre när du ändrar prompten.
- Prova din app med frågor den inte borde klara. Då har du konkreta exempel till reflektionen.
- Använd frågorna i [kapitel 4](../../kapitel/04-manniska-och-ai.md) och [kapitel 6](../../kapitel/06-mojligheter-och-risker.md) och bedömningsschemat i [kapitel 5](../../kapitel/05-lagar-och-regler.md) när du skriver reflektionen.
- Klistra inte in personuppgifter om andra i prompter eller testdata.

[Till innehåll](../../README.md)
