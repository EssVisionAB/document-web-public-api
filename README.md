# document-web-public-api
### Evolution document web solution. Combining front end (Angular 5) and backend (Asp.New.Core) in one project.

To test the iframe solution copy or download **iframe-example.html** to your local computor and just double click on it.

If you whant to develop your own front end, see backend api documentation by ctrl+click on <a href="http://10.3.67.101:5001/swagger/" target="_blank">swagger</a>

## Iframe url configuration:

Within this section all the details regarding configuration of the iframe is presented

### Columns:

Any piece of data avaliable within either the Document class or the Folder class is possible to show within an iframe. To add a column to the iframe add it as parameter to the query string part of url:

&columns=COLUMN_NAME

COLUMN_NAME should correspond to the path of the field within the object and is case sensitive. If not allready present add a localization string for that field in your local IIS site istallation under /wwwroot/assets/i18n/sv.json. This is allso where you change diplay name if you whant a differert representation than provided by default. 

I.e.

&columns=contact.zipCode will return the contacts zipcode

Remember that the string representation of that field will be displayed so if the path references an object you will have json in the table.
 
The name column of any resource (Document, Folder) is allways present and is not needed in query string. The default locale(sv) respresentation of name is 'Resursnamn'

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
### Tags:

&tags=TAG_NAME

Filter published root folders on their publish category (from lookup).

Example url included in next section.

### Page Size:

The url also allows for configuration of how many items are shown on each page. That is done with the following tag:

&pageSize=PAGE_SIZE

Where PAGE_SIZE is an integer (default is 10).

Example:
```
<iframe src="http://example.domain?pagesize=5&columns=createDate&columns=publishCategory&columns=hid&tags=test&tags=publik" />
```
### Hide meta bar and table header:

If you want to hide meta bar or table head, add parameter hideMetaBar=true and/or hideTableHead=true to query string

Example:
```
<iframe src="http://example.domain?category=test&type=all&pagesize=5&hideMetaBar=true&hideTableHead=true" />
```

## Virtual folder:

Display a list of documents in all published folders filtered by their category (which is displayed as root folder name). Query string must be extended with category and type (the publish type by wich documents are filterd), in that case tags and folderId are ignored.

&category=SOME_CATEGORY (from lookup) &type=PUBLISH_TYPE (all, approved or public)

Example:
```
<iframe src="http://example.domain?category=test&type=all&columns=hid&columns=contact.zipCode&pagesize=5" />
```

## Folder published by id:

Display content of folder published by id. query string must contain folderId={guid} NOTE: If category and type is supplied it will be regarded as a virtual and folderId is ignored.

Example:
```
<iframe src="http://example.domain?folderId=59830ECD-5674-4AC6-A48B-F0460AC9413D&ccolumns=contact.zipCode&pagesize=5" />
```


