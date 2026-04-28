# Fight Club 5e XML character format
This repository contains exported character files in the Fight Club 5e XML format.

### File structure overview
Each character file is a single XML document rooted at:

- `<pc version="5">`
  - `<character>`: the main character payload
  - `<imageData>`: optional base64 portrait data

A valid file is typically one character per file.

### Main character section (`<character>`)
The `<character>` block contains the character's core identity, stats, features, inventory, and resources.

Common child tags under `<character>`:
- `<name>`: character name
- `<race>`: race metadata and trait text
- `<class>`: class metadata, hit dice, armor, and progression values
- `<background>`: optional background name
- `<feat>`: features, traits, proficiencies, spells, and similar entries
- `<mod>`: numeric or boolean modifiers that affect the character
- `<tracker>`: counters and slot-like resources
- `<autolevel>`: automatic progression metadata added by the app
- `<abilities>`: comma-separated ability scores
- `<hpMax>` / `<hpCurrent>`: current and maximum HP
- `<wealth>`: base currency total
- `<container>` / `<item>`: inventory and equipment
- `<trait>`, `<personality>`, `<ideals>`, `<bonds>`, `<flaws>`: roleplaying notes
- `<age>`, `<height>`, `<eyes>`, `<skin>`, `<hair>`, `<align>`, `<alignment>`: character details
- `<speed>`, `<size>`, `<languages>`: movement and language metadata
- `<proficiency>`, `<skills>`: proficiency and skill-related data
- `<background>`: additional background or story fields

### Race section (`<race>`)
The `<race>` tag typically contains:
- `<name>`: race name
- `<text>`: descriptive traits and rules text
- `<type>` / `<value>` / `<detail>`: structured metadata for the race
- optional child tags such as `<source>` for origin pages

### Class section (`<class>`)
The `<class>` block contains numeric values and class details, including:
- `<id>`: class identifier
- `<hd>` / `<hdCurrent>`: hit dice total and current hit dice
- `<wealth>`: class-based starting wealth or currency
- `<numClassSkills>`: number of class skills
- `<armor>`: armor class or armor metadata
- `<weapons>`, `<tools>`, `<unarmed>`: proficiencies

### Feat / feature blocks (`<feat>`)
`<feat>` is one of the most common containers. It is used for:
- class features
- racial traits
- feat choices
- spells and spell-like abilities
- proficiencies and special actions

Common `<feat>` children:
- `<name>`: feature or spell name
- `<text>`: description and rules text
- `<type>`: a numeric or text type code
- `<optional>`: whether the feature is optional or conditional
- `<detail>`: short metadata, trait type, or subcategory
- `<value>`: a numeric value associated with the feature
- `<category>`: classification (for example, spell or feature category)
- `<source>`: reference book or page information

### Modifier blocks (`<mod>`)
`<mod>` entries represent contextual adjustments or toggles.
Common children are:
- `<type>`: modifier type code
- `<value>`: numeric value for the modifier
- `<activated>`: `true` / `false` toggle state
- `<label>` / `<detail>`: descriptive text

### Tracker blocks (`<tracker>`)
Trackers are used for expendable resources such as spell slots, abilities, or limited uses.
Common tags include:
- `<label>`: resource name
- `<formula>`: resource formula or roll expression
- `<roll>`: dice roll string
- `<slots>`: maximum slots or uses
- `<slotsCurrent>`: current remaining slots or uses
- `<resetType>`: recharge timing (long rest, short rest, etc.)
- `<spellSlotsOptional>`: optional spell slot tracking

### Spell-related tags
Many feature or spell entries include spell metadata tags:
- `<spell>`: spell level or spell label
- `<school>`: spell school
- `<time>`: casting time
- `<range>`: spell range
- `<duration>`: spell duration
- `<v>`, `<s>`, `<m>`: verbal, somatic, and material components
- `<materials>`: material component text
- `<ritual>`: ritual casting flag
- `<special>`: special spell notes
- `<spellAbility>`: ability used for spellcasting
- `<attackBonus>` / `<attack>` / `<damage>`: attack and damage values

### Inventory and equipment
These tags describe items, containers, and gear:
- `<container>`: bag, pack, or held container
- `<item>`: individual gear entry
- `<slot>`: equipment slot or carrying location
- `<weight>`: weight value
- `<quantity>`: quantity of an item
- `<value>`: monetary value per unit
- `<damage1H>` / `<damage2H>`: weapon damage templates
- `<damageType>`: damage type code
- `<weaponProperty>`: properties like finesse, versatile, reach
- `<weaponRange>` / `<weaponLongRange>`: ranged weapon distances
- `<carried>`: whether an item is carried

### Image and portrait data
The XML may embed portraits inside `<imageData>`:
- `<uid>`: image identifier
- `<encoded>`: base64-encoded image bytes

Note: embedded images increase file size significantly, so you can remove `<imageData>` if you want smaller repo files.

### Additional metadata tags
Fight Club exports also include other tags for character details and campaign references:
- `<source>`: book or page source
- `<note>`: extra notes or annotations
- `<skill>`: skill name or skill modifier data
- `<passive>`: passive perception or other passive values
- `<languages>`: language list or language proficiency
- `<proficiency>`: proficiency information
- `<personality>`, `<ideals>`, `<bonds>`, `<flaws>`: roleplay descriptors
- `<age>`, `<height>`, `<eyes>`, `<skin>`, `<hair>`: physical description
- `<align>`, `<alignment>`: alignment data
- `<speed>`, `<size>`: movement and creature size
- `<resist>`, `<immune>`, `<vulnerable>`, `<conditionImmune>`: resistance and immunity details
- `<xp>`: experience points

### How the format is assembled
- The app stores one character per XML file.
- Character text fields are stored as escaped XML text (`&#39;` for apostrophes, etc.).
- Numeric values appear as child tags like `<value>`, `<level>`, `<slots>`, and `<quantity>`.
- Repeating entries are represented by repeated tags (`<feat>`, `<tracker>`, `<item>`, `<container>`).
- Optional or conditional entries are usually flagged by `<optional>` or `<detail>`.

### Practical tips
- Use XML parsing libraries if you need to extract or transform data.
- Keep the root tag and `version="5"` intact when editing files.
- Remove `<imageData>` if you only need textual character data.
