
# How to Translate

To add or remove languages in the system, you need to update two key files:

## File 1: Language Picker

**Path:** `Client > Components > Language-picker > Language-picker.html`

This file controls the language dropdown available to users or admins for selection.

### Instructions:
- Add or remove language abbreviations in this file to update the dropdown list.
- Edit lines 4 and 13 to include new languages in the dropdown.

### Example:
```html
<span ng-if="type === 'navbar'"
    ng-repeat="lang in ['ru', 'en', 'es']"
    ng-show="currentLanguage !== lang">
    <a href="" ng-click="switchLanguage(lang)">{{'languages.'+lang | translate}}</a>
</span>

<div ng-if="type === 'settings'" class="btn-group">
    <button class="btn btn-default"
        ng-repeat="lang in ['ru', 'en', 'es']"
        ng-if="currentLanguage !== lang" 
        ng-click="switchLanguage(lang)">
        {{'languages.'+lang | translate}}
    </button>
</div>
```
- In the example above, `'ru'`, `'en'`, and `'es'` represent Russian, English, and Spanish, respectively. To add a new language, such as French (`'fr'`), add it to the list: `['ru', 'en', 'es', 'fr']`.

## File 2: Translation Files

**Path:** `Assets > i18n`

This folder contains the language variables used for translations. Each language has its own folder with corresponding translation files.

### Instructions:
- To **add a language**, duplicate the `en` (English) folder, rename it to the desired language code (e.g., `fr` for French), and translate all strings inside each file.
- To **remove a language**, delete the folder for that specific language.

### Example:
- Open `account.json` in the `es` (Spanish) folder and compare it with the `en` folder to see how translations are structured.
- Translate each string in every file within the new language folder.

### Notes:
- Ensure consistency in the naming of language codes throughout the application.
- Double-check all translations to maintain accuracy and clarity.
