# Evolution Document Web (English)
A swedish translation av this text can be found at the bottom of this file
## document-web-public-api
### Evolution document web solution. Combining front-end (Angular 5) and back-end (Asp.Net.Core) in one project.

Evolution Document Web is a public API for Evolution that combines a front-end user interface for customers who wants a ready to use web interface that can be used directly or implemented as iframes in their already existing web sites and a back-end for customers who want to develop their own customized frontend.

## Back-end
If you want to develop your own front-end, see back-end api documentation by ctrl+click on <a href="https://demo-evolution-document-web.sokigohosting.com/swagger/index.html" target="_blank">swagger</a>.

## Front-end
To test the iframe solution copy or download **iframe-example.html** to your local computor and just double click on it.

### Iframe URL configuration:
The front-end implementation can be customized by adding parameters to the URL. Within this section all the details regarding configuration of the iframe is presented.

#### Columns:
It's possible to configure wich columns to be shown i folder and document lists. Any piece of data avaliable within either the Document class or the Folder class is possible to show as columns within an iframe. To add a column to the iframe add it as parameter to the query string part of URL:

&columns=COLUMN_NAME

COLUMN_NAME should correspond to the path of the field within the object and is case sensitive. If not already present add a localization string for that field in your local IIS site installation under /wwwroot/assets/i18n/sv.json. This is also where you change display name if you want another column name than provided by default. 

Example:
&columns=createDate will add the create date as a column to lists.

The name column of any resource (Document, Folder) is always present and is not needed in query string. The default locale(sv) respresentation of name is 'Resursnamn'.

Example locale(sv):
```
{
    "headers": {
        "name": "Resursnamn",
        "publishCategory": "Kategori",
        "publishType": "Publiceringstyp",
        "unitCode": "Enhetskod",
        "createDate": "Skapad datum",
        "version": "Version",
        "hid": "Hid",
        "contact": {
            "name": "Kontaktnamen",
            "address": "Gatuadress",
            "zipCode": "Postnummer",
            "region": "Ort"
        }
    }
}
```

Example URL:
```
<iframe src="http://example.domain?columns=createDate&columns=version" />
```
#### Tags:
The tags parameter is used to filter which folders that will be included in the result regarding to the category the folder is published with in the Evolution main client. To filter the result add it as parameter to the query string part of url:

&tags=TAG_NAME

TAG_NAME should correspond to the category one or more folders is published with in Evolution.

Example:
&tags=Policies will only return folders published with the category "Policies".

Example:
&tags=Policies&tags=Protocols will only return folders published with the category "Policies" or the category "Protocols".

Example URL:
```
<iframe src="http://example.domain?tags=Policies&tags=Protocols" />
```

#### Virtual folder:
In addition to tags, as shown in the tags section, which filters folders and documents from the root folder down, the category parameter can be used to show all documents in a single list that is located in any folder published with a specific category. When the category parameter is used the parameter type must also be included as a parameter to the URL. To filter the result and show documents as a single list add it as parameter to the query string part of url:

&category=SOME_CATEGORY<br>
&type=PUBLISH_TYPE (all, approved or public)

SOME_CATEGORY should correspond to the category one or more folders is published with in Evolution and PUBLISH_TYPE should be either all, approved or public to correspond to what types of documents the list should include. In virtual folders type must be included because multiple folders with the same category can be published with different types.

Example:
&category=Policies&type=approved will return all documents in folders published with category "Policies" that are approved. 

NOTE: If the category parameter is used the tags and folderId parameters can not be included in the URL parameters.

Example URL:
```
<iframe src="http://example.domain?category=Policies&type=approved" />
```

#### Folder published by id:
The folderId parameter is used to display content of folder published by the folders id. To filter the result and show documents as a single list add it as parameter to the query string part of url:

&folderId={guid}

{guid} should correspond to the folder id of the published folder. The folder id for a specific folder is displayed in the folder publish dialog in the Evolution main client.

NOTE: If category and type is supplied it will be regarded as a virtual and folderId is ignored.

Example URL:
```
<iframe src="http://example.domain?folderId=59830ECD-5674-4AC6-A48B-F0460AC9413D" />
```

#### Page Size:
The url also allows for configuration of how many items are shown on each page. Add parameter to the query string part of the URL:

&pageSize=PAGE_SIZE

PAGE_SIZE is corresponding to the number of items to be shown as an integer (default is 10).

Example:
```
<iframe src="http://example.domain?pagesize=5" />
```
#### Hide meta bar and table header:

If you want to hide meta bar (published root folder name) or table head (table column headers), add the parameters to the query string:

&hideMetaBar=true<br>
&hideTableHead=true

Example:
```
<iframe src="http://example.domain?hideMetaBar=true&hideTableHead=true" />
```

### Example URL combining multiple parameters:
This is en example showing folders and documents published with the category "Policies". The list has column headers name, createDate and version. The meta bar (root folder name) is hidden and each page will show 5 items. 

Example URL:
```
<iframe src="http://example.domain?columns=createDate&columns=version&tags=Policies&hideMetaBar=true&pagesize=5" />
```
# Evolution Document Web (Swedish)
## document-web-public-api
### Evolution Document Web. Kombinerad lösning med front-end (Angular 5) och back-end (Asp.Net.Core) i ett och samma projekt.

Evolution Document Web är ett publikt API till Evolution som kombinerar ett front-end användargränssnitt för kunder som vill använda ett färdigt webbgränssnitt som kan användas direkt eller implementerat som iframes på sin befintliga webbplats och ett back-end API för kunder som vill utveckla sitt eget anpassade användargränssnitt.

## Back-end
Om du vill utveckla ditt eget användargränssnitt, se back-end API-dokumentationen genom ctrl+click på <a href="http://31.216.227.251:5001/swagger/" target="_blank">swagger</a>.

## Front-end
För att testa det fördiga användargränssnittet som en iframe kopiera eller ladda ned **iframe-example.html** till din dator och dubbelklicka på filen.

### Iframe URL-konfiguration:
Användargränssnittet kan anpassas genom att lägga till parametrar till URL:en. I detta avsnitt behandlas de konfigurationsmöjligheter som finns.

#### Kolumner:
Det är möjligt att konfigurera vilka kolumner som ska visas i mapp- och dokumentlistor. All information som finns i mapp- och dokumentobjekten kan användas för att visas som kolumner i en iframe. För att lägga till en kolumn i en iframe lägg till den som en parameter till URL:en:

&columns=COLUMN_NAME

COLUMN_NAME ska motsvara fältnamnet för ett objekt och är skiftlägeskänsligt (case sensitive). Om fältnamnet inte redan finns kan det läggas till i installationen på webbservern (IIS) under /wwwroot/assets/i18n/sv.json. Det är även här som man kan ändra visningsnamnet för kolumnen om så önskas. 

Exempel:
&columns=createDate lägger till skapaddatum som en kolumn i dokumentlistor.

Namnkolumnen (mappnamn/dokumentnamn) finns alltid med och behöver inte läggas till som en parameter. Defaultnamnet för denna kolumn är 'Resursnamn'.

Exempel locale(sv):
```
{
    "headers": {
        "name": "Resursnamn",
        "publishCategory": "Kategori",
        "publishType": "Publiceringstyp",
        "unitCode": "Enhetskod",
        "createDate": "Skapad datum",
        "version": "Version",
        "hid": "Hid",
        "contact": {
            "name": "Kontaktnamen",
            "address": "Gatuadress",
            "zipCode": "Postnummer",
            "region": "Ort"
        }
    }
}
```

Exempel URL:
```
<iframe src="http://example.domain?columns=createDate&columns=version" />
```
#### Taggar:
Parametern tags används för att filtrera vilka mappar som visas beroende på vilken kategori som mappen är publicerad med i Evolutions klient. För att filtrera mapparna lägg till parametern till URL:en:

&tags=TAG_NAME

TAG_NAME ska motsvara kategorin som en eller flera mappar är publicerad med i Evolution.

Exempel:
&tags=Policies kommer göra att endast mappar publicerade med kategorin "Policies" visas.

Exempel:
&tags=Policies&tags=Protokoll kommer göra att endast mappar publicerade med kategorin "Policies" eller kategorin "Protokoll" visas.

Example URL:
```
<iframe src="http://example.domain?tags=Policies&tags=Protokoll" />
```

#### Virtuell mapp:
Som ett alternativ till att visa mappstrukturer för en viss kategori av publicerade mappar kan man välja att publicera en rak lista på dokument som ligger i mappar publicerade med en viss kategori. Detta görs med parametern category istället för parametern tags. När parametern category används behöver man även ange parametern type för att ange vilken typ av dokument som ska visas; alla, godkända gällande dokument eller allmänna handlingar (all, approved, public). För att filtrera dokument och visa en rak lista på dessa lägg till parametrarna till URL:en:

&category=SOME_CATEGORY<br>
&type=PUBLISH_TYPE (all, approved or public)

SOME_CATEGORY ska motsvara kategorin en eller flera mappar är publicerade med i Evolution och PUBLISH_TYPE ska vara antingen all, approved eller public för att motsvara vilken typ av dokument som ska visas. I virtuella mappar behöver type vara med som parameter eftersom olika mappar i Evolution som publicerats med samma kategori kan ha olika typ angiven.

Example:
&category=Policies&type=approved kommer visa alla dokument i mappar publicerade med kategorin "Policies" som är godkända och inom sin giltighetstid. 

OBS: Om parametern kategori används kan inte parametrarna tags eller folderId användas samtidigt.

Exempel URL:
```
<iframe src="http://example.domain?category=Policies&type=approved" />
```

#### Mapp publicerad med mappid:
Parametern folderId används om man vill visa dokument för en viss mapp baserat på mappens id (istället för kategori). För att filtrera dokument publicerade i en specifik mapp och visa en rak lista på dessa lägg till parametern till URL:en:

&folderId={guid}

{guid} ska motsvara den publicerade mappens id. Mappens id visas i publiceringsdialogen i Evolutions klient.

OBS: Om parametrarna category och type är med i URL:en kommer det hanteras som en virtuell mapp och folderId ignoreras.

Exempel URL:
```
<iframe src="http://example.domain?folderId=59830ECD-5674-4AC6-A48B-F0460AC9413D" />
```

#### Sidlängd:
Det går också att konfigurera hur många mappar/dokument som ska visas på varje sida. För att ange detta lägg till parametern till URL:en:

&pageSize=PAGE_SIZE

PAGE_SIZE motsvarar antalet poster som ett heltal (default är 10).

Exempel:
```
<iframe src="http://example.domain?pagesize=5" />
```
#### Dölja huvudrubrik och kolumnrubriker:
Om du vill dölja huvudrubriken (den publicerade rotmappens namn) eller kolumnrubriker, lägg till parametrarna till URL:en:

&hideMetaBar=true<br>
&hideTableHead=true

Exempel:
```
<iframe src="http://example.domain?hideMetaBar=true&hideTableHead=true" />
```

### Exempel på URL som kombinerar multipla parametrar:
Detta är ett exempel på en URL som visar mappar och dokument publicerade med kategorin "Policies". I listan visas kolumnrubrikerna skapaddatum och version. Huvudrubriken är dold och listan visar 5 poster (mappar/dokument).

Exempel URL:
```
<iframe src="http://example.domain?columns=createDate&columns=version&&tags=Policies&hideMetaBar=true&pagesize=5" />
```




