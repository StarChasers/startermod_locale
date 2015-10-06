# startermod_locale
Example mod of adding a new language to stonehearth. WILL NOT WORK UNTIL ALPHA 12!!

Instructions for use: Download the mod. Unzip to your stonehearth mods directory, as a peer to stonehearth.smod and radiant.smod. Make sure the folder is named startermod_locale, not startermod_locale-master.

Inside the startermod_locale folder, you should see a manifest.json file, a added_languages.json file and a translations folder which has two files in it: en-XA.json and en-DEV.json.

The mod adds a pseudolocalization of stonehearth's en.json file. The en-DEV.json file is the plain english used to generate en-XA.json. Pseudolocalization replaces all the characters in stonehearth's en.json file with characters that have accents. This mimics what foreign languages will look like when displayed in the game.

When you start up Stonehearth with this mod installed, open the settings menu and go to the system tab. You will see that a language named "[!!Ēņģľĭšħ!!]" will be added to the list of languages. Selecting the "[!!Ēņģľĭšħ!!]" language and clicking "OK" will change the game's language.

How it works:
1) startermod_locale's manifest.json uses this line:
   "mixintos" : {
      "stonehearth/locales/supported_languages.json" : "file(added_languages.json)"
   }
   This causes all the data in added_languages.json to be added to the list of supported languages recognized by the stonehearth mod.
2) added_languages.json specifies a new language, en-XA like so:
      "en-XA": {
         "display_name": "[!!Ēņģľĭšħ!!]",
         "path": "/startermod_locale/translations/en-XA.json"
      }
   display_name is what the settings language drop down will show for the name of the language. You can use this to display the name of a language in its native form.
   path is the path to the .json file that contains the translations. Note you have to specify the mod as the first portion of the path.
   the name "en-XA" is the language code of the translation. See: http://www.science.co.il/Language/Locale-codes.asp
   Most languages and language variants have a language code. In this case, en means English and the XA is a made up name for the pseudolocale.
   The German translation will be de-DE.json, and the Chinese Mandarin translation will be zh-CN.json
   Note: If you have a region specific translation, the last 2 letters of the translation MUST be capitalized!
3) The file that is pointed to "path" is the en-XA.json file under the translations folder. This is the file that contains all the translated strings.

Note: This mod (startermod_locale) is only meant for translators who are looking to translate the main stonehearth game!
For modders looking to create their own mods (ex: a Cafe Mod), do not use this mod as an example.
Explanation:
Internationalization works with all mods. It is currently necessary to include all translation files with the mod. So it's currently not possible to install mod A that only comes with English and then install a German translation for mod A with mod B. To get German support for mod A, the creator of mod A needs to include that German translation with the files for mod A.
The main stonehearth game is the only one that supports installing a mod that grants it additional languages. In the future, we could add support for mod B to grant mod A additional languages. It's just not implemented yet.

How to translate en.json:
Only translate strings that come after a ':'' in the json file. You can more easily view the json on a website such as http://codebeautify.org/jsonviewer
Do not modify the strings that come on the left side of a ':'
Also, do not modify strings that are surrounded by brackets '[' or ']'

Example:
  "ai": {
   "actions": {
      "status_text": {
         "chase_entity": "chasing [name(data.target)]",


Here, the string that needs to be translated is "chasing [name(data.target)]"
Note, DO NOT translate the "[name(data.target)]" portion. This is a special string replacement. The name of the target will replace "[name(data.target)]" in the game.

EX: If a hearthling is chasing a goblin named "Jib", the game will replace "[name(data.target)]" with "Jib" and the final string will read: "chasing Jib"

The replacement is character sensitive, so do not change whether the string is upper or lower case, and do not replace any of the string with a different key. It is best
to copy and past the special portion into your translated text.

You can move "[name(data.target)]" around to different locations within the string.
EX:
The japanese translated file might show something like this:
  "ai": {
   "actions": {
      "status_text": {
         "chase_entity": "[name(data.target)]を追う",

The Chinese file might look like:
  "ai": {
   "actions": {
      "status_text": {
         "chase_entity": "追逐[name(data.target)]",
