# LDOC-specification
```cs
Convention & Specs :
Name : LDOC
Description : Tags and properties are heavily focused on alignment, margins, and gizmo-like positioning. Horizontal spacing are based on default 1 character width(or space). Vertical spacing based on default newline height(similar to when when press enter key and the before to the after caret position is the space).

wildcards : "*"
types : "int", "byte", "boolean", "string", "int4", "byte4", "byte3", "int3","*numeric", "int2", "byte2", "*non-numeric" 
properties : tag, type, param, embeddable, isstatic, prop, pair, noscope, valueref, load

tag: is the main parent "tag". It has much bigger scopes than "prop"
prop: is embeddable property.

[valuedef:pageNumber, valuetype="int", linkto="tag-page"]
[valuedef:pageNumber, valuetype="int", linkto="tag-page"]
[tag:page, type="int", param="title", type="string", valueref="pageNumber", valuereftype="int", valueto="number",  valueref="pageAuthor", valuereftype="string", valueto="Author", valueref="pageTitle", valuereftype="string", valueto="Title", param="author", type="string", embeddable="false", isstatic="false", pair="false"]
[tag:head, type="string", param="margin", type="int4", param="padding", type="int4", embeddable="false", isstatic="true", pair="true"]
[tag:content, type="string", param="margin", type="int4", param="padding", type="int4", embeddable="false", isstatic="false", pair="true"]
[tag:tail, type="string", param="margin", type="int4", param="padding", type="int4", embeddable="false", isstatic="true", pair="true"]
[tag:table, type="string", param="rows", type="int", param="cols", embeddable="false", isstatic="false", pair="true"]

[prop:h, type="int", param="h*numeric", pair=true, embeddable="false", isstatic="false"]//e.g : h1, h2 h3 h4 headers.
[prop:font-bold, type="boolean", param="b", pair=true, embeddable="true", isstatic="false"]
[prop:font-italic, type="boolean", param="i", pair=true, embeddable="true", isstatic="false"]
[prop:font-strikethrough, type="boolean", param="s", pair=true, embeddable="true", isstatic="false"]
[prop:font-size, type="int", param="size", pair=true, embeddable="true", isstatic="false"]
[prop:halign-center, type="int", param="hcenter", pair=true, embeddable="true", isstatic="false"]
[prop:halign-right, type="int", param="hright", pair=true, embeddable="true", isstatic="false"]
[prop:halign-left, type="int", param="hleft", pair=true, embeddable="true", isstatic="false"]
[prop:valign-top, type="int", param="vtop", pair=true, embeddable="true", isstatic="false"]
[prop:valign-center, type="int", param="vcenter", pair=true, embeddable="true", isstatic="false"]
[prop:valign-bottom, type="int", param="vbottom", pair=true, embeddable="true", isstatic="false"]
[prop:image, type="string", param="img", pair=false, embeddable="true", isstatic="false"]
[prop:row, type="string", param="row", pair="true", embeddable="false", isstatic="false"]
[prop:cell, type="string", param="cell", pair="true", embeddable="true", isstatic="false"]

// NOSCOPEs can appear freely and uncontrained as well as automatically embeddable behavior.
[noscope:charspace, type="int", param="*numeric", pair="false",  embeddable="true", isstatic="false"]
[noscope:caption, type="string", param="*non-numeric", pair="false",  embeddable="true", isstatic="false"]
[noscope:link, type="string", param="*non-numeric", pair="false",  embeddable="true", isstatic="false"]
[noscope:margin, type="int4", param="margin", pair="false",  embeddable="true", isstatic="false"]
[noscope:padding, type="int4", param="pad", pair="false",  embeddable="true", isstatic="false"]
[noscope:autonum, type="int", param="autonumber", pair="false", isincreasing="true", isdecreasing="true", embeddable="true", isstatic="false"]
[noscope:getrefint, type="int", param="pad", pair="false",  embeddable="true", isstatic="false"]
[noscope:getrefstring, type="int", param="pad", pair="false",  embeddable="true", isstatic="false"]

//Below is the full exampleof the specs above.

[page:1, Title="Testing Specs Implementation"]
[head]Head Acts as Static Template, Will be Shown on Any Other Pages[/head]
[content][margin=6,6,6,6][padding=2,2,2,2]
//Page declaration can also includes "content" mbedding like this : [page:1, Title="Testing Specs Implementation", margin="6,6,6,6", pad="2,2,2,2" load=content]
This is regular text, along with other river of texts

[h2, 0, hleft] Tag Pairing Header Example.// the "align-left" will align the header to left. opetions are : left, center, right, default is left. "0" mean no extra space/indent.
Below is the example dot bullets in practice.[/h2, 2] //the "2" at the end tag will give 2 newlines after the tag

[bd, 1] //the "1" is the space after the bullet. in this example it will give 1 character space width
this is inline bullet style indent 1 text.
this is inline bullet style indent 2 text.
this is inline bullet style indent 3 text.
this is inline bullet style indent 4 text.
[/bd, 2] //the "2" at the end tag will give 2 newlines after the end tag

[h4, 1, hright]
Below is the example of custom bullet list.
[/h4, 1]
[-, 1]this is inline dash style indent text right here. //the "1" is the space after the bullet
[+, 1]this is inline plus style indent text right here. //the "1" is the space after the bullet
[>, 2]this is inline arrow style indent text right here. //the "2" is the space after the bullet
[*, 2]this is inline asterisk style indent text right here. //the "2" is the space after the bullet

//Extra spacing example using noscope type
[5] 5 characters worth of empty space
[6] 6 characters worth of empty space
[7] 7 characters worth of empty space
[8] 8 characters worth of empty space

[h2, 0, hcenter] //OR can be written using the param like this [h2, 0, ha-c]
Image Embedding Example 
[/h2, 2]

img[path/to/the/file.someExtension", caption="image test", embedd="click this"]

[b]This is tag pairing usage of text bold.[/b]
[b="Inline style of text bold"]

Table example as shown below :

[h2, 0, hleft]Data Summary Table[/h2, 2]

[table, rows="3", cols="2"]
    [row]
        [cell]Header A[/cell]
        [cell]Header B[/cell]
    [/row]
    [row]
        [cell]Data 1[/cell]
        [cell]Data 2[/cell]
    [/row]
    [row]
        [cell]Data 3[/cell]
        [cell]Data 4[/cell]
    [/row]
[/table, 2]

// You can also use inline style for simple tables if needed:
[table]
[row][cell="Steve"] [cell="Age"]
[row][cell="Hanny"] [cell="30"]
[/table]
[/content]

[tail]Tail Acts as Static Template, Will be Shown on Any Other Pages. PAGENUMBER[getrefint=pageNumber][/tail]

```
