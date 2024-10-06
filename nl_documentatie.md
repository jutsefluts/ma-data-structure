Max Assist Data Structuur Documentatie

Dit document legt de structuur uit van de lesgegevens die worden gebruikt in ons lesgeneratorsysteem.

## Algemene Structuur

De lesgegevens zijn gestructureerd als een JSON-array (aangegeven door vierkante haken []) die een enkel object bevat met de volgende topniveau velden:

- `lesson_prerequisites`: Een array van voorbereidende vragen voor de les
- `lesson_structure`: De hoofdstructuur van de les, verdeeld in fasen

## Voorbereidende Vragen (Lesson Prerequisites)

De `lesson_prerequisites` is een array van vraagobjecten. Elk vraagobject heeft de volgende structuur:

```json
{
  "question_key": "",
  "question_text": "",
  "answer": ""
}
````


Het aantal vragen is flexibel en kan naar behoefte worden aangepast.

## Lesstructuur (Lesson Structure)

De `lesson_structure` bevat vier fasen van een les:

- `instruction`: De instructiefase
- `processing`: De verwerkings- of oefenfase
- `conclusion`: De afrondingsfase
- `introduction`: De introductiefase

Elke fase heeft een `content`-array die meerdere elementen kan bevatten. De `processing`-fase heeft een extra `initial_questions`-array vóór de `content`-array.

## Elementtypen

Elk element in de content-array van een fase kan een van de volgende typen zijn:

### Verwerkte Tekst (Processed Text)

### Document Bestand (Document File)

Het Document File-object is een uniek elementtype dat specifiek is ontworpen voor gebruik met het Dubbelklik-platform. Het dient als een antwoord-indiening object voor het uploaden van bestanden.

```json
{
  "document_file": {
    "uuid": "",
    "#type": "document_file",
    "#title": ""
  }
}
````


Dit objecttype moet alleen worden gebruikt wanneer integratie met de bestandsuploadfunctionaliteit van het Dubbelklik-platform vereist is. Het stelt gebruikers in staat om op bestanden gebaseerde antwoorden in te dienen binnen de lesstructuur.

Belangrijke punten:
- Specifiek voor Dubbelklik-platformintegratie
- Gebruikt voor het indienen van bestandsupload-antwoorden
- Moet niet worden gebruikt voor algemene documentreferenties of bijlagen

### Meerkeuzevraag (Multiple Choice Question)

### Open Vraag (Open Question)

## UUID-veld

Het `"uuid": ""` veld moet worden ingevuld met een unieke identifier voor elk element. Deze identifier wordt meestal gegenereerd door het systeem en zorgt ervoor dat elk element uniek kan worden geïdentificeerd binnen de les en in de hele applicatie.

Het formaat van deze identifier kan variëren afhankelijk van de systeemvereisten. Het kan een standaard UUID zijn, een kortere unieke string, of een ander formaat dat uniciteit garandeert. Bijvoorbeeld:

- Standaard UUID: "123e4567-e89b-12d3-a456-426614174000"
- Kortere unieke string: "a1b2c3d4"
- Aangepast formaat: "ELEM_001_XYZ"

Het specifieke formaat moet consistent zijn binnen het systeem en apart worden gedocumenteerd als het een bepaald patroon of generatiemethode volgt.

## Flexibiliteit

- De content-array van elke fase kan een willekeurig aantal (inclusief nul) van elk type inhoudselement bevatten.
- De volgorde en combinatie van elementen binnen een fase zijn flexibel.
- Niet alle fasen of elementtypen hoeven in elke les te worden gebruikt.

## Gebruik

Deze structuur maakt flexibele lescreatie mogelijk. Het systeem dat deze gegevens genereert of verwerkt, moet ervoor zorgen dat:

1. Elk element de juiste inhoud bevat.
2. De algemene structuur (lesson_prerequisites, lesson_structure) voor elke les is voltooid.
3. UUID's worden gegenereerd en toegewezen aan elk element naar behoefte.

## YAML-conversie

Elk object in deze JSON-structuur kan worden geconverteerd naar een overeenkomstig YAML-formaat. Voor gedetailleerde informatie over hoe elk objecttype wordt weergegeven in YAML, raadpleeg het `yaml_element_types_states.yaml` bestand. Dit bestand bevat de specifieke YAML-structuur voor elk elementtype, waaronder:

- Verwerkte Tekst (in verschillende toestanden: tekst, grote afbeelding, tekst en kleine afbeelding)
- Document Bestand
- Meerkeuzevraag (radios)
- Open Vraag (textarea)

De YAML-representatie biedt een alternatief formaat voor de lesstructuur, wat nuttig kan zijn voor bepaalde integraties of verwerkingstaken.