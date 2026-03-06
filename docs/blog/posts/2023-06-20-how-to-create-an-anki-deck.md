---
title: "How to Create an Anki Deck"
date: 2023-06-20
tags:
  - blog
---

# How to Create an Anki Deck

Anki is a flashcard-based spaced-repetition-system (SRS). When reviewing flashcards traditionally you'll see cards you know easily the same amount as you'll review cards you're struggling with. An SRS resolves this inefficiency by increasing the time between reviews for cards you get right and decreasing the time between review on cards you may be struggling with. 

## Preparation
Decide what to study and plan your cards. I'm using Anki to study Japanese vocabulary. For each flashcard, I want to review the Japanese vocabulary on the front, then the Furigana, English definition, and audio on the back. 

### Create Media Clips
Audacity is a free audio editor. Each chapter of my Japanese book has audio that plays the title of each section, the Japanese audio, then the English audio of each word. Audacity is able to label these audio clips. Press `Ctrl + a` to highlight the audio track -> `Analyze` -> `Label Sounds`. I used the following settings to ensure I was capturing the full audio of each word. Depending on the source audio, these settings will likely have to be tweaked. 

| Settings | Value |
| --- | --- |
| Minimum silence duration | .3s |
| Minimum label interval | .5s |
| Maximum leading silence | .1s |
| Maximum trailing silence | .2s |

Once each audio clip is labeled, I deleted all by the Japanese clips. Each label can be edited individually by clicking the label name. Quicker bulk edits can be done under `Edit` -> `Labels` -> `Edit Labels`. To save the finished clips go to `File` -> `Export` -> `Export Multiple`

### Create Spreadsheet

There's multiple ways to create an Anki deck. Each card can be made individually. However, the method I prefer, and will detail here, is to create a spreadsheet first for import into Anki. 

I recommend using the free [LibreOffice Calc](https://www.libreoffice.org/discover/calc/) app to create the spreadsheet, for reasons detailed later under the Import section. I created a column for Japanese, English, Audio, and Tags. 

#### Ruby Characters

Ruby Characters: https://docs.ankiweb.net/templates/fields.html?highlight=tts#ruby-characters

Japanese uses complicated characters, called kanji, in some words. Furigana is the hiragana pronunciation of the kanji, displayed above the character. I had to include Anki's Ruby Character syntax in order to enable the display of the phonetic pronunciation of a word (furigana in my case) above the vocabulary word (or kanji characters in my case). 

Example: `日本語[にほんご]`

When multiple kanji were next to each other, a space needed to be included between the characters. If a space isn't included the the ruby text will be displayed across the entire word, instead of above the individual kanji. 

Example: `世[よ]の 中[なか]`

#### Audio

Importing Media: https://docs.ankiweb.net/importing.html#importing-media

Audio files must be written in a specific format in order to be accessed/played correctly. 

Example: `[sound:myaudio.mp3]`

Select all audio files (`Ctrl + a`), then in Windows hold `SHIFT` while `Right-Click` and select `Copy as path`. Paste the selection into Libre Calc. Used Find and Replace (Edit -> Find and Replace) to replace the path prefix with `[sound:`. In another column use the formula `=(A1&"]")` to add the ending `]` character. Note the A1 is the cell name of your audio file. Copy the column, then `Right-Click` -> `Paste special` -> `Text`. This pastes the full audio format(`[sound:myaudio.mp3]`) as text, instead of the formula. 

#### Tags

Adding Tags: https://docs.ankiweb.net/importing.html#adding-tags

The vocabulary I'm studying came from a specific book. I wanted nested tags matching the book's layout, so I could filters my cards by chapter, then content. Nested tags can be accomplished by using double colons. 

Example: `Genki::Lesson00::Greetings`

## Anki

Once the spreadsheet and audio files are prepped, there's some setup to complete in Anki before the files can be imported. An Anki deck is made of multiple flashcards. We'll need to create a template for our cards, then a deck for them to be added to. 

### Create Card Type

Anki has several `Basic`card types already created that have sections for a `Front` and `Back`. Instead, we'll create a custom card type with fields for each of the columns in the spreadsheet. 

Adding Cards and Notes: https://docs.ankiweb.net/editing.html#adding-cards-and-notes

To create a new Card Type: `Add` -> `Type` -> `Manage` -> `Add` -> `Add: Basic` -> Name the Card Type, then click `OK`. I used these steps to create a `Genki 1 Vocabulary` card type. 

Customizing Fields: https://docs.ankiweb.net/editing.html#customizing-fields

With the new card type created, select the card type, then click `Choose`. Next click `Fields`. This opens a screen that allows renaming, adding, and deleting fields. I renamed `Front` and `Back` to `Japanese` and `English` respectively, then added a field for `Audio`. `Save` changes when done. 

## Create Deck

Decks: https://docs.ankiweb.net/getting-started.html#decks

After creating a card type, there needs to be a deck to put new cards in. To create a new deck select `Create Deck` from the Anki home-screen, then name the deck. The deck I'm creating in this example is named "Genki 1 Vocabulary".

## Import

Importing: https://docs.ankiweb.net/importing.html#importing

Before importing can begin, we need to ensure our spreadsheet is formatted correctly. Anki imports every row of the spreadsheet, including headers. Therefore if there's headers in the spreadsheet, remove them before import. During preparation I recommended using Libre Calc, this is because Anki requires "UTF-8 encoding". Microsoft Excel uses UTF-16. You may create the spreadsheet in Excel, but the finished file will need converted, before it can be imported into Anki. 

**Using Microsoft Excel to Import Into Anki**: [Using Excel to Import into Anki - Google Docs](https://docs.google.com/document/d/12YE_FS6A9ANLTESJNtPP116ti4nNmCBghyoJBRtno_k/edit)

This guide is one way of converting, though I find it far easier to open the Excel document in Libre Calc for conversion or creating the spreadsheet in Libre Calc to begin with. Once in Libre Calc go to `File` -> `Save As` -> Change `Save as type` to `Text CSV (*.csv)` -> `Save`. A `Field Options` box will then pop-up. Leave the default options which will save using `Character set: Unicode (UTF-8)`. The spreadsheet is now ready for import into Anki. 

From the Anki home-screen select `Import File`, then select the CSV file.  Change the `Field separator` to `Comma`. Change the `Notetype` and `Deck` field to the note type and deck created earlier. In my example these are both `Genki 1 Vocabulary`. Then map each field to the spreadsheet columns.

## Styling

### Audio

The cards can start being used at this point, but audio is missing. To update styling select `Browse` from the Anki home-screen to bring up a list of all cards. Select a card from the deck to edit, then select `Cards`. This opens the `Template` screen where the `Front Template`, `Back Template`, and `Styling` can be edited. Field names can be added to a template using double curly braces. To add audio from my example I updated the back template to include `{{Audio}}`.  This adds a play button to the card. 

Audio Replay Buttons: https://docs.ankiweb.net/templates/styling.html#audio-replay-buttons

When audio is included on a card, the play button that appears can be styled or hidden. 

### Ruby Character Filters

Additional Ruby Character Filters: https://docs.ankiweb.net/templates/fields.html?highlight=furigana#additional-ruby-character-filters

Some of the Japanese vocabulary words contain text that should be display as furigana. We can use Ruby Character Filters to control how the Ruby Text is displayed. Without filters the card would display the full field text, including the square brackets (Example: `日本語[にほんご]`). With the filters the card can display either the kanji, kana, or both (furigana). 

### Custom Fonts

Installing Fonts: https://docs.ankiweb.net/templates/styling.html#installing-fonts

Anki supports using custom fonts. To use a custom font on a card a font file is needed. For my deck, I downloaded a few custom fonts from Google Fonts ([Browse Fonts - Google Fonts](https://fonts.google.com/)). Once the font file is downloaded: 

1. Rename the font file to include an underscore at the front of the filename (Example: `_NotoSansJP-Regular.otf`) 
2. Move the file to the Anki Media Collection folder (On Windows: `%appdata%\Anki2\User 1\collection.media`) 
3. Add the font face to the Card Styling 
```css
@font-face {
	font-family: "Noto Sans Japanese";
	src: url("_NotoSansJP-Regular.otf");
}
```

### Example Styling

For the deck I'm creating I want the style to match a kanji learning site I use called WaniKani. I accomplished this using the techniques above with some additional CSS.  Here's the styling I used for reference to create your own: 

**Front Template**
```html
<div class="vocab-reading">{{kanji:Japanese}}</div>
```

**Back Template**
```html
<div class="vocab-reading">{{furigana:Japanese}}</div>
<div class="vocab-meaning">
	<div class="definition">{{English}}</div>
	<div class="audio">{{Audio}}</div>
</div>
```

**Styling**
```css
@font-face {
font-family: "Source Sans Pro";
src: url("_SourceSansPro-Light.ttf");
font-weight: 300;
}

@font-face {
font-family: "Noto Sans Japanese";
src: url("_NotoSansJP-Regular.otf");
}

@font-face {
font-family: "Noto Sans Japanese";
src: url("_NotoSansJP-Light.otf");
font-weight: 300;
}

.card {
margin: 0;
background-color: #eee;
font-size: 16px;
text-align: center;
}

.vocab-reading {
background-image: linear-gradient(to bottom, #f69447, #f17d32);
color: #fff;
font-family: "Noto Sans Japanese", sans-serif;
font-size: 4rem;
text-shadow: 5px 5px 0 #f17d32;
padding: 20px 0;
}

.vocab-meaning {
background: #fff;
margin: 8px 0;
font-size: 2rem;
font-family: "Source Sans Pro", sans-serif;
box-shadow: 0 3px #e1e1e1;
}

rt {
font-size: .35em;
font-weight: 300;
text-align: center;
text-shadow: none;
}

.definition {
padding: 8px 0;
}

.audio {
padding-bottom: 8px;
}

.replay-button {
opacity: 0.5;
}

.replay-button svg circle {
fill-opacity: 0;
}
```

## Sharing

Syncing with AnkiWeb: https://docs.ankiweb.net/syncing.html#syncing-with-ankiweb

Now the deck is fully created and can be used on your local workstation. However, to review on multiple devices, with progress syncing, the deck can be uploaded to AnkiWeb. To sync, first create an AnkiWeb account: https://ankiweb.net/. Then go to the home-page of the Desktop application and select `Sync`. Anki will prompt for the AnkiWeb login credentials. The deck will then sync and become available on AnkiWeb. 

Sharing Decks Publicly: https://docs.ankiweb.net/contrib.html#sharing-decks-publicly

Others may benefit from created decks. To share a deck with the general public, logon to AnkiWeb and select "Share" from the menu next to the deck to be shared.