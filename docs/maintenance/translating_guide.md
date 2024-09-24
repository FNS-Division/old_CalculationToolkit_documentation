#### How to translate

There are 2 files you need to add or remove languages

**File 1 :**

**Client> Components > Language-picker > Language-picker.html**

In this file , you add or remove the language abbreviation. This helps provide the dropdown for the user/admin to select

<!-- Edit line 4 and 13 to add new languages on dropdown -->

<span ng-if="type === 'navbar'

" ng-repeat="lang in ['ru', 'en', 'es']"

ng-show="currentLanguage !== lang">
    `<a href="" ng-click="switchLanguage(lang)">`{{'languages.'+lang | translate}}`</a>`

<div ng-if="type === 'settings'" class="btn-group">
    <button class="btn btn-default"

    ng-repeat="lang in ['ru', 'en', 'es']"

    ng-if="currentLanguage !== lang" ng-click="switchLanguage(lang)">{{'languages.'+lang | translate}}`</button>`

</div>

**File 2 :**

 **Assets > i18n**

* This folder contains the variables needed to translate. It has been grouped into folders, each containing the language.
  Currently, we have En - english, Es - Spanish , Ru - Russian
* To delete , delete the folder language
  To add, i suggest you duplicate the En folder first , then rename it to the language you wish to translate to ,
  then edit all the strings in each file and do the string translation

* For example...you can open account.json in es folder, and check also  en folder to see how transaction has been done.
* translate all the strings in all the files .
