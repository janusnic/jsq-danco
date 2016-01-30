# jsq-danco

DOM или объектная модель документа
===================================

Данный html-код:
```
<html>
<head>
    <title>Hello, JavaScript!</title>
</head>
<body>
    <div>
        <span>Раз</span>
        <span>Два</span>
    </div>
</body>
</html>
```
Сформирует следующую структуру DOM:
-----------------------------------
![dom model](dom_model.png)

во главе всего у нас кореневой объект window, который внутри себя содержит объект document, который в свою очередь содержит объект body, а объект body - все остальные объекты, которые тоже могут содежать другие объекты.
1 innerHTML
-----------
```
<html>
<head>
    <title>Hello, JavaScript!</title>
    <script>
    window.onload = function(){
        alert(window.document.body.innerHTML);
    }
    </script>
</head>
<body>
    <div>
        <span>Раз</span>
        <span>Два</span>
    </div>
</body>
</html>
```
innerHTML - свойство, объекта document, которое используеться если нужно вытащить код из HTML-документа или поменять его.

Следующий фрагмент кода затрёт все содержимое объекта body, а вместо него выведет слово пусто.

2.html
------
```
<html>
<head>
    <title>Hello, JavaScript!</title>
    <script>
    window.onload = function(){
        window.document.body.innerHTML = '(пусто)';
    }
    </script>
</head>
<body>
    <div>
        <span>Раз</span>
        <span>Два</span>
    </div>
</body>
</html>
```
3. Модификация DOM
-------------------
```
     <button onclick="document.getElementById('stuff').innerHTML = 'Нажали первую Button';">Первая</button>

     <button onclick="document.getElementById('stuff').innerHTML = 'Нажали сдедующую Button';">Следующая</button>
    
    <p>Это не меняется.</p>
    <p id="stuff">Это меняется.</p>
    <p>Это не меняется.</p>
```

document.body.children
-----------------------
у каждого элемента объектной модели документа есть свойство children - это массив его детей, где мы по индексу можем обращаться к детям. 

4 внутренний HTML код потомка:
------------------------------
```
<html>
<head>
    <title>Hello, JavaScript!</title>
    <script>
    window.onload = function(){
        alert(window.document.body.children[0].innerHTML);
    }
    </script>
</head>
<body>
    <div>
        <span>Раз</span>
        <span>Два</span>
    </div>
</body>
</html>
```
5 Чтобы получить доступ к тегам span:
-------------------------------------
```
<html>
<head>
    <title>Hello, JavaScript!</title>
    <script>
    window.onload = function(){
        var div = window.document.body.children[0];
        var span2 = div.children[1];
        alert(span2.innerHTML);
    }
    </script>
</head>
<body>
    <div>
        <span>Раз</span>
        <span>Два</span>
    </div>
</body>
</html>
```
6 lenght
---------
С помощью свойства lenght можно узнать длинну массива - количество элементов в массиве.
```
<html>
<head>
    <title>Hello, JavaScript!</title>
    <script>
    window.onload = function(){
        var div = window.document.body.children[0];
        alert(div.children.length);
    }
    </script>
</head>
<body>
    <div>
        <span>Раз</span>
        <span>Два</span>
    </div>
</body>
</html>
```
7 innerHTML
-----------
Также мы можем устанавливать innerHTML не только для body, но и для любого другого элемента:
```
<html>
<head>
    <title>Hello, JavaScript!</title>
    <script>
    window.onload = function(){
        var div = window.document.body.children[0];
        var span2 = div.children[1];
        span2.innerHTML = '2';
    }
    </script>
</head>
<body>
    <div>
        <span>Раз</span>
        <span>Два</span>
    </div>
</body>
</html>
```
8 parentNode
-------------
parentNode - выведет ссылку на родительский элемент.
```
<html>
<head>
    <title>Hello, JavaScript!</title>
    <script>
    window.onload = function(){
        var div = window.document.body.children[0];
        var span2 = div.children[1];
        alert(span2.parentNode.innerHTML);
    }
    </script>
</head>
<body>
    <div>
        <span>Раз</span>
        <span>Два</span>
    </div>
</body>
</html>
```
У каждого элемента есть свойство innerHTML, которое позволяет получить содержимое элемента в виде HTML кода - его можно как читать так и записывать в него.
У каждого объекта есть массив потомков, мы можем узнать размер этого массива с помощью свойства length и обращаться к каждого элементу данного массива по индексу с помощью свойства children[].
У каждого элемента есть свойство parentNode, которое указывает на родителя.

Свойства объектов JavaScript
=============================
9 свойства элемента span2:
--------------------------
```

<html>
<head>
    <title>Hello, JavaScript!</title>
    <script>
    window.onload = function(){           
        var div = document.body.children[0];
        var span2 = div.children[1];
        var_dump(span2);
    }
    
    function var_dump(obj){
        var s = '<h1>' + obj + '</h1>';
        s += '<ol>';

        for (p in obj)
            s += '<li><b>' + p + '</b> : ' + obj[p] + '</li>';
        
        s += '</ol>';
        window.document.body.innerHTML = s;
    }   
    </script>
</head>
<body>
    <div>
        <span>Раз</span>
        <span>Два</span>
    </div>
</body>
</html>
```

[object HTMLSpanElement]
------------------------
```
title :
lang :
translate : true
dir :
dataset : [object DOMStringMap]
hidden : false
tabIndex : -1
accessKey :
draggable : false
spellcheck : true
contentEditable : inherit
isContentEditable : false
offsetParent : [object HTMLBodyElement]
offsetTop : 8
offsetLeft : 34
offsetWidth : 26
offsetHeight : 17
style : [object CSSStyleDeclaration]
innerText : Два
outerText : Два
webkitdropzone :
onabort : null
onblur : null
oncancel : null
oncanplay : null
oncanplaythrough : null
onchange : null
onclick : null
onclose : null
oncontextmenu : null
oncuechange : null
ondblclick : null
ondrag : null
ondragend : null
ondragenter : null
ondragleave : null
ondragover : null
ondragstart : null
ondrop : null
ondurationchange : null
onemptied : null
onended : null
onerror : null
onfocus : null
oninput : null
oninvalid : null
onkeydown : null
onkeypress : null
onkeyup : null
onload : null
onloadeddata : null
onloadedmetadata : null
onloadstart : null
onmousedown : null
onmouseenter : null
onmouseleave : null
onmousemove : null
onmouseout : null
onmouseover : null
onmouseup : null
onmousewheel : null
onpause : null
onplay : null
onplaying : null
onprogress : null
onratechange : null
onreset : null
onresize : null
onscroll : null
onseeked : null
onseeking : null
onselect : null
onshow : null
onstalled : null
onsubmit : null
onsuspend : null
ontimeupdate : null
ontoggle : null
onvolumechange : null
onwaiting : null
click : function click() { [native code] }
focus : function focus() { [native code] }
blur : function blur() { [native code] }
onautocomplete : null
onautocompleteerror : null
namespaceURI : http://www.w3.org/1999/xhtml
prefix : null
localName : span
tagName : SPAN
id :
className :
classList :
attributes : [object NamedNodeMap]
innerHTML : Два
outerHTML : Два
shadowRoot : null
scrollTop : 0
scrollLeft : 0
scrollWidth : 0
scrollHeight : 0
clientTop : 0
clientLeft : 0
clientWidth : 0
clientHeight : 0
onbeforecopy : null
onbeforecut : null
onbeforepaste : null
oncopy : null
oncut : null
onpaste : null
onsearch : null
onselectstart : null
onwheel : null
onwebkitfullscreenchange : null
onwebkitfullscreenerror : null
previousElementSibling : [object HTMLSpanElement]
nextElementSibling : null
children : [object HTMLCollection]
firstElementChild : null
lastElementChild : null
childElementCount : 0
hasAttributes : function hasAttributes() { [native code] }
getAttribute : function getAttribute() { [native code] }
getAttributeNS : function getAttributeNS() { [native code] }
setAttribute : function setAttribute() { [native code] }
setAttributeNS : function setAttributeNS() { [native code] }
removeAttribute : function removeAttribute() { [native code] }
removeAttributeNS : function removeAttributeNS() { [native code] }
hasAttribute : function hasAttribute() { [native code] }
hasAttributeNS : function hasAttributeNS() { [native code] }
getAttributeNode : function getAttributeNode() { [native code] }
getAttributeNodeNS : function getAttributeNodeNS() { [native code] }
setAttributeNode : function setAttributeNode() { [native code] }
setAttributeNodeNS : function setAttributeNodeNS() { [native code] }
removeAttributeNode : function removeAttributeNode() { [native code] }
closest : function closest() { [native code] }
matches : function matches() { [native code] }
getElementsByTagName : function getElementsByTagName() { [native code] }
getElementsByTagNameNS : function getElementsByTagNameNS() { [native code] }
getElementsByClassName : function getElementsByClassName() { [native code] }
insertAdjacentHTML : function insertAdjacentHTML() { [native code] }
createShadowRoot : function createShadowRoot() { [native code] }
getDestinationInsertionPoints : function getDestinationInsertionPoints() { [native code] }
requestPointerLock : function requestPointerLock() { [native code] }
getClientRects : function getClientRects() { [native code] }
getBoundingClientRect : function getBoundingClientRect() { [native code] }
scrollIntoView : function scrollIntoView() { [native code] }
insertAdjacentElement : function insertAdjacentElement() { [native code] }
insertAdjacentText : function insertAdjacentText() { [native code] }
scrollIntoViewIfNeeded : function scrollIntoViewIfNeeded() { [native code] }
webkitMatchesSelector : function webkitMatchesSelector() { [native code] }
animate : function animate() { [native code] }
remove : function remove() { [native code] }
webkitRequestFullScreen : function webkitRequestFullScreen() { [native code] }
webkitRequestFullscreen : function webkitRequestFullscreen() { [native code] }
querySelector : function querySelector() { [native code] }
querySelectorAll : function querySelectorAll() { [native code] }
nodeType : 1
nodeName : SPAN
baseURI : file:///home/janus/github/21v-js/unit_03/dom/2.html
ownerDocument : [object HTMLDocument]
parentNode : [object HTMLDivElement]
parentElement : [object HTMLDivElement]
childNodes : [object NodeList]
firstChild : [object Text]
lastChild : [object Text]
previousSibling : [object Text]
nextSibling : [object Text]
nodeValue : null
textContent : Два
hasChildNodes : function hasChildNodes() { [native code] }
normalize : function normalize() { [native code] }
cloneNode : function cloneNode() { [native code] }
isEqualNode : function isEqualNode() { [native code] }
compareDocumentPosition : function compareDocumentPosition() { [native code] }
contains : function contains() { [native code] }
lookupPrefix : function lookupPrefix() { [native code] }
lookupNamespaceURI : function lookupNamespaceURI() { [native code] }
isDefaultNamespace : function isDefaultNamespace() { [native code] }
insertBefore : function insertBefore() { [native code] }
appendChild : function appendChild() { [native code] }
replaceChild : function replaceChild() { [native code] }
removeChild : function removeChild() { [native code] }
isSameNode : function isSameNode() { [native code] }
ELEMENT_NODE : 1
ATTRIBUTE_NODE : 2
TEXT_NODE : 3
CDATA_SECTION_NODE : 4
ENTITY_REFERENCE_NODE : 5
ENTITY_NODE : 6
PROCESSING_INSTRUCTION_NODE : 7
COMMENT_NODE : 8
DOCUMENT_NODE : 9
DOCUMENT_TYPE_NODE : 10
DOCUMENT_FRAGMENT_NODE : 11
NOTATION_NODE : 12
DOCUMENT_POSITION_DISCONNECTED : 1
DOCUMENT_POSITION_PRECEDING : 2
DOCUMENT_POSITION_FOLLOWING : 4
DOCUMENT_POSITION_CONTAINS : 8
DOCUMENT_POSITION_CONTAINED_BY : 16
DOCUMENT_POSITION_IMPLEMENTATION_SPECIFIC : 32
addEventListener : function addEventListener() { [native code] }
removeEventListener : function removeEventListener() { [native code] }
dispatchEvent : function dispatchEvent() { [native code] }
```
10 Мы можем добавлять новые свойства любым (даже встроенным) объектам:
-----------------------------------------------------------------------
```
<html>
<head>
    <title>Hello, JavaScript!</title>
    <script>
    window.onload = function(){           
        var div = document.body.children[0];
        var span2 = div.children[1];

        span2.myProperty = 1000;

        var_dump(span2);
    }
    
    function var_dump(obj){
        var s = '<h1>' + obj + '</h1>';
        s += '<ol>';

        for (p in obj)
            s += '<li><b>' + p + '</b> : ' + obj[p] + '</li>';
        
        s += '</ol>';
        window.document.body.innerHTML = s;
    }   
    </script>
</head>
<body>
    <div>
        <span>Раз</span>
        <span title='Title for span2' lang='English'>Два</span>
    </div>
</body>
</html>
```

[object HTMLSpanElement]
-------------------------
```
myProperty : 1000
title : Title for span2
lang : English

```
Функция getElementById 
=======================
позволяет быстро получать доступ к элементам - принимает строкое значение идентификатора и возвращает DOM-объект, а если такого элемента не найдено, то возвращает NULL.

Для того чтобы изменить стилевое свойство элемента нужно воспользоваться фукнцией style:
----------------------------------------------------------------------------------------
11.html
```
<html>
<head>
    <title>Hello, JavaScript!</title>
    <script>
    window.onload = function(){           
        var span1 = document.getElementById('one');
        span1.style.color = 'red';
        span1.style.fontWeight = 'bold';
    }  
    </script>
</head>
<body>
    <div>
        <span id="one">Раз</span>
        <span>Два</span>
    </div>
</body>
</html>
```

CSS свойства
=============
CSS свойства, название которых указываються через дефис нужно удалять, а второе слово указывать с большого регистра.

12 проверить сколько есть возможных CSS свойст для элемента:
------------------------------------------------------------
```
<html>
<head>
    <title>Hello, JavaScript!</title>
    <script>
    window.onload = function(){           
        var span1 = document.getElementById('one');

        var_dump(span1.style);  
    }

    function var_dump(obj){
        var s = '<h1>' + obj + '</h1>';
        s += '<ol>';

        for (p in obj)
            s += '<li><b>' + p + '</b> : ' + obj[p] + '</li>';
        
        s += '</ol>';
        window.document.body.innerHTML = s;
    }   
    </script>
</head>
<body>
    <div>
        <span id="one">Раз</span>
        <span>Два</span>
    </div>
</body>
</html>
```
13 create table
---------------
```
        <script>
            function create() {
                var row = 5, col = 5;
                var tablestart="<table id=myTable border=1>";
                var tableend = "</table>";
                var trstart = "<tr bgcolor=#ff9966>";
                var trend = "</tr>";
                var tdstart = "<td>";
                var tdend = "</td>";
                
                document.write(tablestart);

                for (var r=0;r<row;r++) {
                    document.write(trstart);
                    for(var c=0; c<col; c++) {
                        document.write(tdstart+"Row."+r+" Col."+c+tdend);
                    }
                }
                document.write(tableend);
                document.write("<br/>");
             }
        </script>
        <br/>
            <button id="create" onclick="create()">create table</button>

```
14 document.createElement
-------------------------
```
    <script type="text/javascript">
        function tableCreate(){
            var body = document.body,
                tbl  = document.createElement('table');
            
            body.appendChild(tbl);
        }
        tableCreate();
   </script>
```
Elements
---------
```
<table></table>

table {
    display: table;
    border-collapse: separate;
    border-spacing: 2px;
    border-color: grey;
}
```
15 insertRow insertCell
------------------------
```
<script type="text/javascript">
  function tableCreate(){
    var body = document.body,
        tbl  = document.createElement('table');

    for(var i = 0; i < 5; i++){
        var tr = tbl.insertRow();
        for(var j = 0; j < 5; j++){
            var td = tr.insertCell();
        }
    }
    body.appendChild(tbl);
}
tableCreate();
```
Elements
---------
```
    <table><tbody>
        <tr>
            <td></td><td></td><td></td><td></td><td></td>
        </tr>
        <tr>
            <td></td><td></td><td></td><td></td><td></td>
        </tr>
        <tr>
            <td></td><td></td><td></td><td></td><td></td>
        </tr>
        <tr>
            <td></td><td></td><td></td><td></td><td></td>
        </tr>
        <tr>
            <td></td><td></td><td></td><td></td><td></td>
        </tr>
    </tbody></table>
```
16 createTextNode
------------------
```
<script type="text/javascript">
 function tableCreate(){
    var body = document.body,
        tbl  = document.createElement('table');
    
    for(var i = 0; i < 5; i++){
        var tr = tbl.insertRow();
        for(var j = 0; j < 5; j++){
            var td = tr.insertCell();
            td.appendChild(document.createTextNode('Cell'));
        }
    }
    body.appendChild(tbl);
 }
tableCreate();
</script>
```
17 style
---------
```
<script type="text/javascript">
 function tableCreate(){
    var body = document.body,
        tbl  = document.createElement('table');
    tbl.style.width  = '500px';
    tbl.style.border = '3px solid red';
    
    for(var i = 0; i < 5; i++){
        var tr = tbl.insertRow();
        for(var j = 0; j < 5; j++){
            var td = tr.insertCell();
            td.appendChild(document.createTextNode('Cell'));
            td.style.border = '2px solid green';
        }
    }
    body.appendChild(tbl);
 }
tableCreate();
</script>
```
18 setAttribute
---------------
```
<script type="text/javascript">
 function tableCreate(){
    var body = document.body,
        tbl  = document.createElement('table');
    tbl.style.width  = '500px';
    tbl.style.border = '3px solid red';
    
    for(var i = 0; i < 5; i++){
        var tr = tbl.insertRow();
        for(var j = 0; j < 5; j++){
            if(i == 4 && j == 4) continue;
            var td = tr.insertCell();
            td.appendChild(document.createTextNode('Cell'));
            td.style.border = '2px solid green';
            if(i == 3 && j == 4){
                    td.setAttribute('rowSpan', '2');
                }
        }
    }
    body.appendChild(tbl);
 }
tableCreate();
</script>
```
19.html - setAttribute('id', 'myTable')
---------------------------------------
```
<script type="text/javascript">
 function tableCreate(){
    var body = document.body,
        tbl  = document.createElement('table');
        tbl.setAttribute('id', 'myTable');
    tbl.style.width  = '500px';
    tbl.style.border = '3px solid red';
    
    for(var i = 0; i < 5; i++){
        var tr = tbl.insertRow();
        for(var j = 0; j < 5; j++){
            
            var td = tr.insertCell();

            td.appendChild(document.createTextNode('Cell'));
            td.style.border = '2px solid green';
            
        }
    }
    body.appendChild(tbl);
 }
tableCreate();
</script>
```

20  createTHead 
----------------
```
<script type="text/javascript">
 function tableCreate(){
    var body = document.body,
        tbl  = document.createElement('table');
        tbl.setAttribute('id', 'myTable');
    tbl.style.width  = '500px';
    tbl.style.border = '3px solid red';

    var header = tbl.createTHead();
    var row = header.insertRow(0);
    var cell = row.insertCell(0);
    cell.innerHTML = "<b>This is a table header</b>";
    
    for(var i = 0; i < 5; i++){
        var tr = tbl.insertRow();
        for(var j = 0; j < 5; j++){
            
            var td = tr.insertCell();

            td.appendChild(document.createTextNode('Cell'));
            td.style.border = '2px solid green';
            
        }
    }
    body.appendChild(tbl);
 }
tableCreate();
</script>
```

21  createTHead
----------------
```
<script type="text/javascript">
 function tableCreate(){
    var body = document.body,
        tbl  = document.createElement('table');
        tbl.setAttribute('id', 'myTable');
    tbl.style.width  = '500px';
    tbl.style.border = '3px solid red';

    var header = tbl.createTHead();
    var tr = header.insertRow(0);
    for(var j = 0; j < 5; j++){
            var th = tr.insertCell();
            th.appendChild(document.createTextNode('Head Cell'));
            th.style.border = '5px solid blue';
            
        }
    
    for(var i = 0; i < 5; i++){
        var tr = tbl.insertRow();
        for(var j = 0; j < 5; j++){
            
            var td = tr.insertCell();

            td.appendChild(document.createTextNode('Cell'));
            td.style.border = '2px solid green';
            
        }
    }
    body.appendChild(tbl);
    return false;
 }
 function DeleteFunction() {
    document.getElementById("myTable").remove();
    return false;
}
function DeleteThead() {
    document.getElementById("myTable").deleteTHead();
    return false;
}

</script>
```
22 Add Caption
--------------
```
<button onclick="tableCreate()">Create thead</button>
<button onclick="DeleteFunction()">Delete table</button>  
<button onclick="DeleteThead()">Delete thead</button>  
<button onclick="AddCaption()">Add Caption</button>  
<script type="text/javascript">
 function tableCreate(){
    var body = document.body,
        tbl  = document.createElement('table');
        tbl.setAttribute('id', 'myTable');
    tbl.style.width  = '500px';
    tbl.style.border = '3px solid red';

    var header = tbl.createTHead();
    var tr = header.insertRow(0);
    for(var j = 0; j < 5; j++){
           
            var th = tr.insertCell();

            th.appendChild(document.createTextNode('Head Cell'));
            th.style.border = '5px solid blue';
            
        }
    
    for(var i = 0; i < 5; i++){
        var tr = tbl.insertRow();
        for(var j = 0; j < 5; j++){
            
            var td = tr.insertCell();

            td.appendChild(document.createTextNode('Cell'));
            td.style.border = '2px solid green';
            
        }
    }
    body.appendChild(tbl);
    return false;
 }
 function DeleteFunction() {
    document.getElementById("myTable").remove();
    return false;
}
function DeleteThead() {
    document.getElementById("myTable").deleteTHead();
    return false;
}
function AddCaption() {
    var table = document.getElementById("myTable").createCaption();
    table.innerHTML = "<b>My table caption</b>";
    return false;
}
```

23 createTFoot
---------------
```
function AddFoot() {
    var table = document.getElementById("myTable");
    var footer = table.createTFoot();
    var row = footer.insertRow(0);
    var cell = row.insertCell(0);
    cell.innerHTML = "<b>This is a table footer</b>";
    return false;
}

```
24 deleteRow() Method
----------------------
```
function deleteTableRow() {
            var dr=0;
            if(confirm("It will be deleted..!!")) {
               document.getElementById("myTable").deleteRow(dr);
                }
            }

```

25 location.reload
--------------------
```
function reloadPage(){
                location.reload();
            }
```

createElement
--------------
```
function addTable() {
    var myTableDiv = document.getElementById("myDynamicTable");

    var table = document.createElement('TABLE');
    table.border = '1';

    var tableBody = document.createElement('TBODY');
    table.appendChild(tableBody);

    for (var i = 0; i < 3; i++) {
        var tr = document.createElement('TR');
        tableBody.appendChild(tr);

        for (var j = 0; j < 4; j++) {
            var td = document.createElement('TD');
            td.width = '75';
            td.appendChild(document.createTextNode("Cell " + i + "," + j));
            tr.appendChild(td);
        }
    }
    myTableDiv.appendChild(table);
}
```

documentFragment
================
documentFragment - "фрагмент документа" наиболее близок по смыслу к обычному DOM-элементу.

То есть, его можно создать:
```
var fragment = document.createDocumentFragment()
```
в него можно добавлять другие узлы.
```
fragment.appendChild(node)
```
когда documentFragment вставляется в DOM - то он исчезает, а вместо него вставляются его дети. Это единственное и основное свойство documentFragment по сравнению со всеми остальными сущностями DOM.

Возврат множества узлов из функции
-----------------------------------
```

function makeRow() {

  var fragment = document.createDocumentFragment()

  var td_1 = document.createElement('TD')

  fragment.appendChild(td_1)

  fragment.appendChild(td_n)

  return fragment

}
```
Затем внешняя функция может вставить его в DOM или использовать далее без промежуточных массивов.

Быстрая вставка в DOM
----------------------
Допустим, нам нужно создать пачку элементов TR и вставить их в DOM.

Первый способ - создавать их и вставлять. И так n раз.

Но операция вставки в "живой" DOM дорогая. И тут на помощь приходит как раз documentFragment. Можно вставлять в него, а уже потом его добавить в DOM.


Document.querySelector()
========================
Возвращает первый элемент внутри документа, который совпадает с определенной группой селекторов.

вернется первый элемент в документе с классом "myclass":
--------------------------------------------------------
```
var el = document.querySelector(".myclass");
```
Возвращается null, если нет найденых совпадений; в ином случае, нам вернется первый найденный элемент.

Если селектор найден по ID и этот ID ошибочно используется несколько раз в документе, нам вернется первый совпавший элемент.

Если селекторы не корректны, выбрасывается исключение SYNTAX_ERR.

Строка передаваемых аргументов в querySelector должна соответствовать синтаксу CSS.

```
<div id="foo\bar"></div>
<div id="foo:bar"></div>

<script>
  console.log('#foo\bar')               // "#fooar"
  document.querySelector('#foo\bar')    // Ничего не найдено


  console.log('#foo\\bar')              // "#foo\bar"
  console.log('#foo\\\\bar')            // "#foo\\bar"
  document.querySelector('#foo\\\\bar') // Найден в первом div'e

  document.querySelector('#foo:bar') // Ничего не найдено
  document.querySelector('#foo\\:bar') // Найдено во втором div'е
</script>
```
26.html
--------
```
<table>
  <thead>
    <tr>
      <th class='prop__name' data-prop-name='firstName'>First Name</th>
      <th class='prop__name' data-prop-name='lastName'>Last Name</th>
      <th class='prop__name' data-prop-name='birth'>Birth</th>
    </tr>
  </thead>
  <tbody></tbody>
</table>

<script>
var table = document.querySelector('table'), 
    data_container = table.querySelector('tbody');

var createTable = function () {
    var fragment = document.createDocumentFragment(), curr_item, curr_p;
    for (var i = 0; i < 5; i++) {
        curr_item = document.createElement('tr');
        curr_item.classList.add(i % 2 === 0 ? 'odd' : 'even');
        for(var j = 0; j < 5; j++){
            curr_p = document.createElement('td');
            curr_p.classList.add('prop__value');
            curr_p.appendChild(document.createTextNode('Cell'));
            curr_item.appendChild(curr_p);
         }
        fragment.appendChild(curr_item);
    }
    data_container.appendChild(fragment);
};
createTable();
</script>
```
27.html
-------
```
<script>
var table = document.querySelector('table'), 
    data_container = table.querySelector('tbody'), 
    data = [
        {
            'firstName': 'Scooby',
            'lastName': 'Doo',
            'birth': 1969
        },
        {
            'firstName': 'Yogi',
            'lastName': 'Bear',
            'birth': 1958
        },
        {
            'firstName': 'Tom',
            'lastName': 'Cat',
            'birth': 1940
        },
        {
            'firstName': 'Jerry',
            'lastName': 'Mouse',
            'birth': 1940
        },
        {
            'firstName': 'Fred',
            'lastName': 'Flintstone',
            'birth': 1960
        }
    ], 
    n = data.length;
    
var createTable = function (src) {
    var fragment = document.createDocumentFragment(), curr_item, curr_p;
    for (var i = 0; i < n; i++) {
        curr_item = document.createElement('tr');
        curr_item.classList.add(i % 2 === 0 ? 'odd' : 'even');
        data[i].el = curr_item;
        for (var p in data[i]) {
            if (p !== 'el') {
                curr_p = document.createElement('td');
                curr_p.classList.add('prop__value');
                curr_p.dataset.propName = p;
                curr_p.textContent = data[i][p];
                curr_item.appendChild(curr_p);
            }
        }
        fragment.appendChild(curr_item);
    }
    data_container.appendChild(fragment);
};
createTable(data);
</script>
```