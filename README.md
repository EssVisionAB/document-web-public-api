# document-web-public-api
### New evolution document web solution. Combining front end (Angular 5) and backend (Asp.New.Core) in one project.

To test iframe solution copy or download **iframe-example.html**

For backend api documentation ctrl+click on <a href="http://10.3.67.101:5001/swagger/" target="_blank">swagger</a>


## Iframe url configuration:

Within this section all the details regarding configuration of the iframe is presented

Columns:

Any piece of data avaliable within either the Document class or the Folder class is possible to show within an iframe. To add a column to the iframe within the url add:

&columns=COLUMN_NAME

COLUMN_NAME should correspond to the path to the field within the object and it is case sensitive. Also add a localization string for that field within /assets/locale/sv_SE.json in your local IIS site.

I.e.

&columns=contact.zipCode will return the contacts zipcode

Remember that the string representation of that field will be displayed so if the path references an object you will have json in the table.

Tags:

&tags=TAG_NAME

Filter published root folders on their category.

Page Size:

The url also allows for configuration of how many items are shown on each page. That is done with the following tag:

&pagesize=PAGE_SIZE

Where PAGE_SIZE is an integer.

Example url:

http://localhost:63285/?url=localhost:8090&tags=internal&tags=external&columns=Name&columns=published&columns=Contact.ZipCode&pagesize=5

Hide meta bar and table header:

add parameter &hideMetaBar=true and/or &hideTableHead=true to src string

Example url:

http://localhost:63285/?url=localhost:8090&category=test&type=all&pagesize=5&hideMetaBar=true&hideTableHead=true


## Virtual folder:

Display list of documents in published folders with category as root folder name. Url must be extended with category and type, in that case tags are ignored.

&category=SOME_CATEGORY (from lookup) &type=PUBLISH_TYPE (all, approved or public)

Example url:

http://localhost:63285/?url=localhost:8090&category=test&type=all&columns=hid&columns=contact.zipCode&pagesize=5


## Folder published by id:

Display content of folder published by id. Url must contain &folderId={guid} NOTE: If category and type is supplied in url it will be regarded as Virtual and folderId is ignored.

Example url:

http://localhost:63285/?url=localhost:8090&folderId=59830ECD-5674-4AC6-A48B-F0460AC9413D&columns=Name&columns=Contact.ZipCode&pagesize=5

