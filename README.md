# Evolution Document Web
## document-web-public-api
### Evolution document web solution. Combining front-end (Angular 5) and back-end (Asp.Net.Core) in one project.

Evolution Document Web is a public API for Evolution that combines a frontend user interface for customers who wants a ready to use web interface that can be used directly or implemented as iframes in their already existing web sites and a backend for customers who want to develop their own customized frontend.

## Back-end
If you want to develop your own front-end, see back-end api documentation by ctrl+click on <a href="http://31.216.227.251:5001/swagger/" target="_blank">swagger</a>.

## Front-end
To test the iframe solution copy or download **iframe-example.html** to your local computor and just double click on it.

### Iframe URL configuration:
The front-end implementation can be customized by adding parameters to the URL. Within this section all the details regarding configuration of the iframe is presented.

#### Columns:
It's possible to configure wich columns to be shown i folder and document lists. Any piece of data avaliable within either the Document class or the Folder class is possible to show as columns within an iframe. To add a column to the iframe add it as parameter to the query string part of URL:

&columns=COLUMN_NAME

COLUMN_NAME should correspond to the path of the field within the object and is case sensitive. If not allready present add a localization string for that field in your local IIS site istallation under /wwwroot/assets/i18n/sv.json. This is also where you change display name if you whant a column name than provided by default. 

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
<iframe src="http://example.domain?tags=Policiestags=Protocols" />
```

#### Virtual folder:
In addition to tags, as shown in the tags section, which filters folders and documents from the root folder down, the category parameter can be used to show all documents in a single list that is located in any folder published with a specific category. When the category parameter is used the parameter type must also be included as a parameter to the URL. To filter the result and show documents as a single list add it as parameter to the query string part of url:

&category=SOME_CATEGORY &type=PUBLISH_TYPE (all, approved or public)

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
The url also allows for configuration of how many items are shown on each page. parameter to the query string part of url:

&pageSize=PAGE_SIZE

PAGE_SIZE is corresponding to the number of items to be shown as an integer (default is 10).

Example:
```
<iframe src="http://example.domain?pagesize=5" />
```
#### Hide meta bar and table header:

If you want to hide meta bar (published root folder name) or table head (table column headers), add parameter hideMetaBar=true and/or hideTableHead=true to query string

Example:
```
<iframe src="http://example.domain?hideMetaBar=true&hideTableHead=true" />
```

### Example URL combining multiple parameters:
This is en example showing folders and documents published with the category "Policies". The list has column headers name, createDate and version. The meta bar (root folder name) is hidden and each page will show 5 items. 

Example URL:
```
<iframe src="http://example.domain?columns=createDate&columns=version&&tags=Policies&hideMetaBar=true&pagesize=5" />
```


