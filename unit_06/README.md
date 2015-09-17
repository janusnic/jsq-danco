# jQuery UI

jQuery UI - это библиотека на основе jQuery, реализующая более 20 плагинов, среди которых плагины организующие различное поведение, восемь видов виджетов и анимационные эффекты. Кроме этого, UI обладает несколькими темами оформления, с помощью которых оформляются виджеты и которые содержат набор полезных иконок. Любая из тем оформления может быть подкорректирована прямо на [сайте jQuery UI](http://jqueryui.com/themeroller/), непосредственно перед загрузкой. 


### Выбор компонентов и загрузка
Зайдите на [страницу загрузки jQuery UI](http://jqueryui.com/download/) и вы увидите, что перед скачиванием можно выбрать необходимые компоненты, тему оформления и версию библиотеки

### Выбрать оформление

Выберите одну из стандартных тем оформления плагинов jQuery UI в поле Theme или создайте свою тему с [помощью themeroller'а](http://jqueryui.com/themeroller/).

Если вы хотите использовать тему оформления, которую вы настроите самостоятельно, то в начале сделайте все необходимые настройки темы на этой странице, затем нажмите кнопку "Download theme" и вы окажетесь на странице загрузки библиотеки, где в поле Theme будет указана отредактированная вами тема.

- css — содержит файлы оформления (CSS-файл и изображения).
- js — содержит файлы с jQuery и jQuery UI.
- Development-bundle — Здесь много различных файлов с демонстрацией работы плагина и другими вспомогательными файлами.
Кроме этих трех папок, в корне архива лежит файл index.html, с демонстрацией скачанных плагинов.

## Подключение UI к вашему сайту
```
<link type="text/css" href="css/themename/jquery-ui-1.11.4.custom.css" rel="Stylesheet"/>      
<script type="text/javascript" src="js/jquery.min.js"></script>
<script type="text/javascript" src="js/jquery-ui-1.11.4.custom.min.js"></script>
```

Все плагины поведения и виджетов обладают схожим принципом работы. Каждый плагин jQuery UI представлен одним основным методом, который вызывается на выбранных элементах. Его имя всегда совпадает с именем плагина. С помощью этого метода можно инстанцировать (устанавливать) плагин на элементы, узнавать и изменять свойства плагина, устанавливать обработчики событий, а так же, запускать функции плагина, которые называют методами.

## Инстанцирование
Для установки любого плагина на элементы страницы, достаточно выбрать нужные элементы средствами jQuery и затем вызвать на них метод работы с плагином (имя которого всегда совпадает с названием плагина):
```
$("#someId").dialog()
```
применит плагин Dialog к элементу с идентификатором someId, превратив его в диалоговое окно.
```
$("div:lt(3)").draggable()
```
применит плагин Draggable к первым трем div'ам на странице, сделав их перетаскиваемыми.
## Методы
Обычно, под методом какого-то объекта в javascript, подразумевается функция, вызываемая на этом объекте следующим образом:
```
obj.A();

// вызов метода A на объекте obj

obj.B();

// вызов метода B на объекте obj
```
Однако в пределах работы с конкретными плагинами jQuery UI, методами называют такую форму записи:
```
$("#someId").plaginName("имя метода", параметры метода);

$("#someId").dialog("close")
```
Метод close закроет диалоговое окно, установленное на элемент с id = someId
```
$("div").draggable("destroy")
```
Destroy удалит функциональность draggable со всех div-элементов на странице

## Свойства

Каждое свойство можно задать в момент инстанцирования плагина. Для этого, при установке плагина на элемент нужно передать объект со свойствами в формате {имя_свойства_1:значение_1, имя_свойства_2:значение_2, ...}:

```
// сделаем из элемента с id=someId диалоговое окно с помощью 
// плагина dialog и укажем при этом заголовок для окна

$("#someId").dialog({title:"Сообщение"});


//сделаем из первого div'а на странице календарь с помощью 
// плагина datepicker, и укажем минимальную и максимальную дату

$("div:first").datepicker({
  minDate:new Date(2007,1-1,1),  maxDate:newDate(2016,1-1,1)
    });

```
Кроме того, значение любого свойства можно узнать или изменить уже после инстанцирования плагина. Для этого необходимо использовать метод "option":
```
// узнаем заголовок у диалогового окна 
var dialogTitle = $("#someId").dialog("option","title");

// изменим заголовок, добавив к нему префикс "#1 
"$("#someId").dialog("option","title","#1 " + dialogTitle)

// изменим минимальную дату в календаре,
// который установлен на первый div на странице

$("div:first").datepicker("option", "minDate", new Date(2008,1 - 1,1));
```
## События

Обработчики событий можно устанавливать средствами основного метода плагина:

```
// обработка события close диалогового окна

$("selector").dialog({
   close: function(event,ui)
{
... }
});
```
или с помощью bind стандартного метода библиотеки jQuery:
```
// обработка события close диалогового окна

$("selector").bind("dialogclose",function(event,ui){ ... });
```

## Оформление
Все плагины jQuery UI обладают общей системой оформления. Ее можно настраивать с помощью визуального редактора ThemeRoller, а так же манипулируя css напрямую.

# Плагин Tabs 

## Tabs1.html
```
<link rel="stylesheet" href="css/smoothness/jquery-ui-1.8.9.custom.css">
Для того, чтобы сделать из элемента систему вкладок, нужно, чтобы он имел подобную структуру:
<div id="myTabs">
<ul>
<li><a href="#a">Tab 1</a></li>
<li><a href="#b">Tab 2</a></li>
</ul>
<div id="a">This is the content panel linked to the first tab, it is shown by default.</div>
<div id="b">This content is linked to the second tab and will be shown when its tab is clicked.</div>
</div>
<script src="development-bundle/jquery-1.4.4.js"></script>
<script src="development-bundle/ui/jquery.ui.core.js"></script>
<script src="development-bundle/ui/jquery.ui.widget.js"></script>
<script src="development-bundle/ui/jquery.ui.tabs.js"></script>
<script>
(function($){
$("#myTabs").tabs();
})(jQuery);
</script>
В одном блоке, часть вкладок может быть готовой, а часть подгружаемой:
  <div id="tabs">
    <ul>
      <li><a href="#tabs-1">Готовая вкладка</a></li>
      <li><a href="/ui/ex1.html">Подгружаемая вкладка 1</a></li>
      <li><a href="/ui/ex3.php">Подгружаемая вкладка 2</a></li>
    </ul>
    <div id="tabs-1">
      <p>Содержимое вкладки 1</p>
    </div>

```
Плагин Tabs использует стандартные стили jQueryUI-css для оформления вкладок. Для редактирования оформления рекомендуется использовать специальную ручную настройку на сайте jQuery UI. 

## tabs2.html
```
<link rel="stylesheet" href="css/tabsTheme.css">

#myTabs { width:400px; padding:5px; border:1px solid #636363; background:#c2c2c2 none; }

.ui-widget-header { border:0; background:#c2c2c2 none; font-family:Georgia; }

#myTabs .ui-widget-content { border:1px solid #aaa; background:#fff none; font-size:80%; }

.ui-state-default, .ui-widget-content .ui-state-default { border:1px solid #636363; background:#a2a2a2 none; }

.ui-state-active, .ui-widget-content .ui-state-active { border:1px solid #aaa; background:#fff none; }
```
#### Свойства

- selected
Определяет номер открытой вкладки (нумерация начиная с 0). Чтобы все вкладки оказались закрыты, необходимо указать значение -1.
```
// ------- Работа со свойством selected ---------
// в момент установки tabs на элемент

(function($){ var tabOpts = { selected: 1}
$("#myTabs").tabs(tabOpts);
})(jQuery);

//получение значения selected

var selected = $("selector").tabs("option","selected" );

//изменение значения selected
$("selector").tabs("option","selected",3 );
```
- Disabling

В этом свойстве можно задавать массив с номерами вкладок, которые должны оказаться недоступны для выбора.
```
// ------- Работа со свойством disabled ---------
// в момент установки tabs на элемент
$("selector").tabs({disabled: [1,2]});


//получение значения disabled 
    var disabled = $("selector").tabs(
    "option",
    "disabled" );

// изменение значения disabled
    $("selector").tabs(
    "option",
    "disabled",
    [1,2]
    );

(function($){ var tabOpts = { disabled: [1] }
$("#myTabs").tabs(tabOpts);
})(jQuery);
```
## Transition effects 6

Это свойство определяет тип анимации, используемой при скрытии и появлении вкладок, а так же продолжительность этой анимации. В поле duration можно задать продолжительность анимации (строковым значением "slow", "normal" или "fast" или целым числом — количеством миллисекунд). По умолчанию, duration равен "normal". Тип анимации задается указанием изменяемого css-свойства и режимом его изменения (насколько я понимаю, подходит только значение toggle):
```
// ------- Работа со свойством fx ---------
// в момент установки tabs на элемент
    $("selector").tabs({
    fx: {opacity:'toggle',
    duration:'fast'
    } });


//получение значения fx
    var fx = $("selector").tabs(
    "option",
    "fx" );

//изменение значения fx
    $("selector").tabs(
    "option",
    "fx",
    {opacity:'toggle',
    duration:'fast'
    } );

    (function($){ var tabOpts = {
    fx: {
    opacity: "toggle",
    duration: "slow" }
    }
    $("#myTabs").tabs(tabOpts);
    })(jQuery);

```
## Collapsible tabs 7

Если установить это свойство в true, то появится возможность сворачивать все вкладки. Для этого достаточно нажать на заголовок открытой в данный момент вкладки.
```
//------- Работа со свойством collapsible ---------
// в момент установки tabs на элемент
$("selector").tabs({
collapsible: false
});


//получение значения closeOnEscape
var collapsible = $("selector").tabs(
"option",
"collapsible" );
//изменение значения collapsible
$("selector").tabs(
"option",
"collapsible",
false );

(function($){
var tabOpts = {
collapsible: true
}
$("#myTabs").tabs(tabOpts);
})(jQuery);
```
### spinner 8
В этом свойстве можно задать текст HTML, который будет использован в качестве заголовка вкладки, пока загружается ее содержимое. Если задать в этом свойстве пустую строку, то на время загрузки содержимого, заголовок вкладки меняться не будет.
```
// ------- Работа со свойством spinner ---------
// в момент установки tabs на элемент
$("selector").tabs({
spinner: 'Загрузка...'
});
 
//получение значения spinner
var spinner = $("selector").tabs(
"option",
"spinner" );
//изменение значения spinner
$("selector").tabs(
"option",
"spinner",
'Загрузка...' );
```
### Tab events 9

В event можно указать, событие какого типа должно произойти на элементе заголовка вкладки, чтобы она открылась.
```
//------- Работа со свойством event ---------
//в момент установкиtabs на элемент
$("selector").tabs({
event: 'mouseover'
});
//получение значения event
var event = $("selector").tabs(
"option",
"event" );
//изменение значения event
$("selector").tabs(
"option",
"event",
'mouseover' );

(function($){
var handleSelect = function(e, tab) {
$("<p></p>", {
text: "Tab at index " + tab.index + " selected",
"class": "status-message ui-corner-all"
}).appendTo(".ui-tabs-nav", "#myTabs").fadeOut(5000, function() {
$(this).remove();
});
},
tabOpts = {
select: handleSelect
}
$("#myTabs").tabs(tabOpts);
})(jQuery);

```
### Tabs9.html
Это событие происходит, когда вкладка становится видимой.
```
// обработка события show
$("selector").tabs({
   show:
function(event,
ui)
{
... }
});
 
// еще один способ (используя метод bind)
$("selector").bind("tabsshow",
function(event,ui){ ... });

(function($){
$("#myTabs").tabs();
$("#myTabs").bind("tabsselect", function(e, tab) {
alert("The tab at index " + tab.index + " was selected");
});
})(jQuery);

```

### create
Событие create происходит в момент инициализации tabs на элементе.
```
// обработка события create
$("selector").tabs({
   create:
function(event,ui)
{
... }
});
 
// еще один способ (используя метод bind)
$("selector").bind(
"tabscreate",
function(event,
ui){ ... });
```
### add 11
Это событие происходит при добавлении новой вкладки.
```
// обработка события add
$("selector").tabs({
   add:
function(event,ui)
{
... }
});
 
// еще один способ (используя метод bind)
$("selector").bind(
"tabsadd",
function(event,ui){ ... });
```

### disable 10
Это событие происходит, когда одна из вкладок становиться активной (доступной для выбора).
```
// обработка события disable
$("selector").tabs({
   tabsdisable:
function(event,ui)
{
... }
});
 
// еще один способ (используя метод bind)
$("selector").bind(
"disable",
function(event,ui){ ... });

```
### enable 10

Это событие происходит, когда одна из вкладок становиться неактивной (недоступной для выбора).
```
// обработка события enable
$("selector").tabs({
   enable:
function(event,ui)
{
... }
});
 
// еще один способ (используя метод bind)
$("selector").bind(
"tabsenable",
function(event,
ui){ ... });

```


### load

Это событие происходит в момент окончания ajax-загрузки удаленной вкладки.
```
// обработка события load
$("selector").tabs({
   load:function(event,ui)
{
... }
});
 
// еще один способ (используя метод bind)
$("selector").bind(
"tabsload",function(event,ui){ ... });
```
### remove

Это событие происходит при удалении вкладки.
```
// обработка события remove
$("selector").tabs({
   remove:function(event,ui)
{
... }
});
 
// еще один способ (используя метод bind)
$("selector").bind(
"tabsremove",function(event,ui){ ... });

```
### select

Это событие происходит, при клике по заголовку вкладки. Если обработчик этого события вернет значение false, то переключения между вкладками не произойдет.
```
// обработка события select
$("selector").tabs({
   select:function(event,ui)
{
... }
});
 
// еще один способ (используя метод bind)
$("selector").bind(
"tabsselect",function(event,ui){ ... });

```

## Tabs10.html

```

(function($){
$("#myTabs").tabs({
disabled: [1]
});

$("#enable").click(function() {
$("#myTabs").tabs("enable", 1);
});

$("#disable").click(function() {
$("#myTabs").tabs("disable", 1);
});
})(jQuery);

```

### Adding and removing tabs tabs11.html

```

(function($){
$("#myTabs").tabs();
$("#remove").click(function() {
$("#myTabs").tabs("remove", parseInt($("#indexNum").val(), 10));
});

$("#add").click(function() {
$("#myTabs").tabs("add", "remoteTab.txt", "A New Tab!");
});
})(jQuery);

```

## Simulating clicks tabs12.html

```

(function($){
$("#myTabs").tabs();
$("#remove").click(function() {
$("#myTabs").tabs("remove", parseInt($("#indexNum").val(), 10));
});

$("#add").click(function() {
$("#myTabs").tabs("add", "remoteTab.txt", "A New Tab!").tabs("select", $("#myTabs").tabs("length") - 1);
});
})(jQuery);

```
## Creating a tab carousel yabs13.html

```

(function($){
$("#myTabs").tabs().tabs("rotate", 1000, true);
})(jQuery);

```
## tabs14.html

```

(function($){
$("#myTabs").tabs();
$("#destroy").click(function() {
$("#myTabs").tabs("destroy");
});
})(jQuery);

```

## Getting and setting options tabs15

```
<button type="button" id="show">Show Selected</button>


(function($){
$("#myTabs").tabs();
$("#show").click(function() {
$("<p></p>", {
text: "Tab at index " + $("#myTabs").tabs("option", "selected") + " is active"
}).appendTo(".ui-tabs-nav").fadeOut(5000);
});
})(jQuery);
```
## tabs16.html

```
<label for="newIndex">Enter a tab index to select</label>
<input id="newIndex" type="text">
<button type="button" id="set">Change Selected</button>

(function($){
$("#myTabs").tabs();
$("#set").click(function() {
$("#myTabs").tabs("option", "selected", parseInt($("#newIndex").val()));
});
})(jQuery);

```

## AJAX tabs tabs17

```
<div id="myTabs">
<ul>
<li><a href="#a">Tab 1</a></li>
<li><a href="#b">Tab 2</a></li>
<li><a href="remoteTab.txt">AJAX Tab</a></li>
</ul>


(function($){
$("#myTabs").tabs();
})(jQuery);

```
## Changing the URL of a remote tab's content tabs18

```
<div id="myTabs">
<ul>
<li><a href="#a">Tab 1</a></li>
<li><a href="#b">Tab 2</a></li>
<li><a href="remoteTab.txt">AJAX Tab</a></li>
</ul>
<select id="fileChooser">
<option value="remoteTab1">remoteTab.txt</option>
<option value="remoteTab2">remoteTab2.txt</option>
</select>

(function($){
$("#myTabs").tabs();
$("#fileChooser").change(function() {
$("#myTabs").tabs("url", 2, $(this).val());
});
})(jQuery);

```
## Reloading a remote tab tabs19

```

(function($){
$("#myTabs").tabs();
$("#fileChooser").change(function() {

$("#myTabs").tabs("url", 2, $(this).val()).tabs("load", 2);
});
})(jQuery);

```

## Displaying data obtained via JSONP 20
```
<div id="myTabs">
<ul>
<li><a href="#a"><span>Nebula Information</span></a>
</li>
<li><a href="#flickr"><span>Images</span></a></li>
</ul>
<div id="flickr"></div>
</div>

(function($){
var img = $("<img/>", {
height: 100,
width: 100
}),
tabOpts = {
select: function(event, ui) {
if (ui.tab.toString().indexOf("flickr") != -1 ) {
$("#flickr").empty();

$.getJSON("http://api.flickr.com/services/feeds/photos_public.gne?tags=nebula&format=json&jsoncallback=?", function(data) {
$.each(data.items, function(i,item){
img.clone().attr("src", item.media.m).appendTo("#flickr");
if (i == 5) { return false; }
        });
    });
 }}
};

$("#myTabs").tabs(tabOpts);
})(jQuery);

```

## Как узнать номер открытой вкладки?

```
// Если вкладки установлены на элемент с
id = example:
var $tabs = $('#example').tabs();
// то получить номер открытой вкладки можно так:
var selected = $tabs.tabs('option', 'selected');

```

## Как открыть ссылку прямо во вкладке, не покидая страницу?

Если необходимо, чтобы при нажатии по ссылке, которая находится внутри вкладки, содержимое страницы по ссылке загрузилось в эту вкладку, вместо того, чтобы пользователь перешел на эту страницу

```
// "перехватим" нажатие по ссылке и загрузим средствами jQuery
// содержимое находящееся по ссылке прямо во вкладку:
$('#example').tabs({
  load:
function(event,
ui)
{
    $('a',
ui.panel).click(function()
{
      $(ui.panel).load(this.href);
      return false;
    });
  }
});
```
Как открыть вкладку по нажатию на ссылку, а не заголовок вкладки?

Если необходимо, чтобы при нажатии по ссылке, которая находится внутри вкладки, содержимое страницы по ссылке загрузилось в эту вкладку, вместо того, чтобы пользователь перешел на эту страницу

```
// инициализация вкладок
// (будет открыта первая вкладка)
var $tabs = $('#example').tabs();

// при нажатии на ссылку, сымитируем нажатие по нужной вкладке
$('#my-text-link').click(function()
{
    $tabs.tabs('select',
2);
    return
false;
});
```
Как предотвратить выбор другой вкладки, пока не будет пройдена валидация формы в текущей вкладке?

Воспользуемся тем, что когда обработчик события tabsselect возвращает false, переключение вкладки не происходит:

```
$('#example').tabs({
    select:
function(event,ui)
{
        var isValid =
... // выполним валидацию, присвоив переменной true или false
        return isValid;
    }
});
```
Как незамедлительно открыть добавленную вкладку?

Воспользуемся тем, что при добавлении новой вкладки происходит событие tabsadd
```
var $tabs = $('#example').tabs({
    add:function(event,ui)
{
        $tabs.tabs('select','#'+ui.panel.id);
    }
});
```
Как избавиться от эффекта FOUC (Flash of Unstyled Content) пока идет инициализация вкладок?

Эффектом FOUC называют тот случай, когда браузер собирает (инициализирует) тяжелую страницу не мгновенно, а за несколько секунд, во время которых в окне браузера постоянно мельтешат элементы страницы.

Наиболее простым способом является скрыть вкладки, которые должны оказаться закрытыми, добавив их элементам специальный класс.
```
<div id="example" class="ui-tabs">
  ...
  <div id="a-tab-panel" class="ui-tabs-hide">
</div>
  ...
</div>
```
Почему мой слайдер (или Google Map, или sIFR и т.д.) не работает, если он был в первоначально закрытой вкладке?

Многие виджеты в момент инициализации пытаются узнать свой размер, но если они находятся в закрытой вкладке, то они не смогут это сделать: элемент вкладки скрыт с помощью css-правила display:none, а значит размеры всех содержащихся в нем элементов равны 0.

Эту проблему можно исправить, изменив способ скрытия вкладок на "смещение влево". Для этого нужно переписать следующие правила:
```
.ui-tabs
.ui-tabs-hide
{
    position:absolute;
    left:-10000px;
}
```
Для Google Map подойдет и другой способ. Можно вызвать метод пересчета размеров карты, когда вкладка с ней будет открыта:
```
$('#example').bind('tabsshow',
function(event,ui) {
    if(ui.panel.id=="map-tab")
{
        resizeMap();
    }
});

```
## Accordion Widget
### Accordion's structure 1
```
<title>Accordion</title>
<link rel="stylesheet" href="css/smoothness/jquery-ui.css">
<div id="myAccordion">
</div>
<script src="development-bundle/jquery-1.4.4.js"></script>
<script src="development-bundle/ui/jquery.ui.core.js"></script>
<script src="development-bundle/ui/jquery.ui.widget.js"></script>
<script src="development-bundle/ui/jquery.ui.accordion.js">
</script>

(function($){
$("#myAccordion").accordion();
})(jQuery);
```
### Styling accordion 2
```
<link rel="stylesheet" href="css/accordionTheme.css">
```
## Configuring accordion 3
```



(function($){

var accOpts = {

event: "mouseover"

};

$("#myAccordion").accordion(accOpts);

})(jQuery);


```
### Changing the default active header 4

Это свойство отвечает за то, какая вкладка окажется открыта. Если указать в нем false, то все вкладки будут закрыты.
```
//------- Работа со свойством active ---------
// в момент установки accordion на элемент
$("selector").accordion({
active:false
});


//получение значения active
var active = $(".selector").accordion("option","active" );
//изменение значения addClasses
$("selector").accordion( "option", "active", false );


(function($){

var accOpts = {

active: 2

};

$("#myAccordion").accordion(accOpts);

})(jQuery);


```
Change the configuration object once again 5
```
(function($){

var accOpts = {

active: false

};

$("#myAccordion").accordion(accOpts);

})(jQuery);
```
collapsible option 6

По умолчанию, пользователь не может закрывать вкладки, а только переключать. Однако если свойство collapsible установлено в true, то нажатие на заголовок открытой вкладки приведет к ее закрытию (если вкладки переключаются при наведении курсора на заголовок, то и закрытие будет происходить при наведении, а не при нажатии).
```
// ------- Работа со свойством collapsible ---------
// в момент установки accordion на элемент
$("selector").accordion({
collapsible:true
});
 
//получение значения collapsible
var collapsible = $("selector").accordion(
"option",
"collapsible" );
//изменение значения collapsible
$("selector").accordion(
"option",
"collapsible",
true );


(function($){

var accOpts = {

active: false,

collapsible: true

};

$("#myAccordion").accordion(accOpts);

})(jQuery);


```

Filling 7

Аккордеон занимает все возможное горизонтальное пространство внутри своего родителя. Если необходимо, чтобы он занимал также и все свободное пространство по вертикали, необходимо установить свойство fillSpace в true. Однако, это не означает, что если родитель изменит свою высоту, то аккордеон изменит свою вслед за ним. Такое поведение необходимо организовывать самостоятельно.
```
// ------- Работа со свойством fillSpace ---------
// в момент установки accordion на элемент
$("selector").accordion({
fillSpace:true
});
 
//получение значения fillSpace
var fillSpace = $("selector").accordion(
"option",
"fillSpace" );
//изменение значения fillSpace
$("selector").accordion(
"option",
"fillSpace",
true );


#container { height:600px; width:400px; }

</style>

<div id="container">

<div id="myAccordion">


(function($){
var accOpts = {
fillSpace: true
};
$("#myAccordion").accordion(accOpts);
})(jQuery);

```
Accordion animation 8

Этот параметр определяет тип анимации. Задав false, вы отключите анимационную смену вкладок аккордеона.
```
// ------- Работа со свойством animated ---------
// в момент установки accordion на элемент
$("selector").accordion({
animated:"bounceslide"
});
 
//получение значения animated
var animated = $("selector").accordion(
"option",
"animated" );
//изменение значения animated
$("selector").accordion(
"option",
"animated",
"bounceslide" );
Тип "bounceslide" доступен только при подключенном UI Effects Core.

(function($){

var accOpts = {

animated: false

};

$("#myAccordion").accordion(accOpts);

})(jQuery);
```
## jquery.effects.core.js 9
```
<script src="development-bundle/ui/jquery.effects.core.js">

</script>



(function($){

var accOpts = {

animated: "bounceslide"

};

$("#myAccordion").accordion(accOpts);

})(jQuery);


```
jquery.effects.core.js 10 - 11
```
(function($){

var accOpts = {

animated: "easeOutBounce"

};

$("#myAccordion").accordion(accOpts);

})(jQuery);



(function($){

var accOpts = {

clearStyle: true,

animated: "easeOutBounce"

};
```
Accordion events Using the change event 12
```


(function($){

var accOpts = {

change: function(e, ui) {

$(".notify").remove();

$("<div />", {

"class": "notify",

text: ([

ui.newHeader.find("a").text(),

"was activated,",

ui.oldHeader.find("a").text(),

"was closed"].join(" "))

}).insertAfter("#myAccordion").fadeOut(2000, function(){

$(this).remove();

});

}};

$("#myAccordion").accordion(accOpts);

})(jQuery);


```
The changestart event 13
```


(function($){

var accOpts = {

changestart: function(e, ui) {

$(".notify").remove();

$("<div />", {

"class": "notify",

text: ([ui.newHeader.find("a").text(), "was activated,", ui.oldHeader.find("a").text(), "was closed"].join(" "))

}).insertAfter("#myAccordion").fadeOut(2000, function(){

$(this).remove();

});

}};

$("#myAccordion").accordion(accOpts);

})(jQuery);


```
Accordion navigation 14

Если этот параметр включен, то вкладки аккордеона можно будет открывать по принципу якорей. Если вы хотите самостоятельно обрабатывать ситуацию и принимать решение, о том, какая вкладка должна быть открыта, используйте параметр navigationFilter.
```
// ------- Работа со свойством navigation ---------
// в момент установки accordion на элемент
$(".selector").accordion({
navigation:15
});
 
//получение значения navigation
var navigation = $(".selector").accordion(
"option",
"navigation" );
//изменение значения navigation
$(".selector").accordion(
"option",
"navigation",
15 );


<link rel="stylesheet" href="css/accordionTheme2.css">



(function($){

var accOpts = {

navigation: true

};

$("#myAccordion").accordion(accOpts);

})(jQuery);


```
## Accordion methods

Header activation 15

С помощью этого свойства можно задать элементы, которые будут использоваться в качестве заголовков.
```
// ------- Работа со свойством header ---------
// в момент установки accordion на элемент
$("selector").accordion({
header:'h3'
});


//получение значения header
var header = $("selector").accordion(
"option",
"header" );
//изменение значения cursorAt
$("selector").accordion(
"option",
"header",
'h3' );


<label for="activateChoice">Enter a header index to activate</label>

<input id="activateChoice">

<button type="button" id="activate">Activate</button>


(function($){

$("#myAccordion").accordion();

$("#activate").click(function() {

$("#myAccordion").accordion("activate", parseInt($("#activateChoice").val(), 10));

});

})(jQuery);


```
Resizing an accordion panel 16

Событие change происходит при переключении вкладок аккордеона. Если переключение анимировано, то это событие будет происходить в течении выполнения анимации (неоднократно). Если вам нужно среагировать на переключение лишь один раз, используйте событие changestart.
```
// второй параметр передаваемый в обработчик будет обладать специфическими полями:
$('.ui-accordion').bind('accordionchange',
function(event,
ui) {
  ui.newHeader
// объект jQuery с элементом, являющимся заголовком ОТКРЫВАЮЩЕЙСЯ вкладки
  ui.oldHeader
// -||-||- ЗАКРЫВАЮЩЕЙСЯ вкладки  
 ui.newContent
// объект jQuery с элементом, являющимся содержимым ОТКРЫВАЮЩЕЙСЯ вкладки
  ui.oldContent
//-||-||- ЗАКРЫВАЮЩЕЙСЯ вкладки
});
 
//обработка события change
$("selector").accordion({
   change:function(event,ui)
{
... }
});
 
//еще один способ (используя метод bind)
$("selector").bind(
"accordionchange",
function(event,
ui){ ... });

```
Событие changestart происходит в момент начала переключения вкладок аккордеона.
```
// второй параметр передаваемый в обработчикбудет обладать специфическими полями:
$('.ui-accordion').bind('accordionchange',
function(event,ui) {
  ui.newHeader
//объект jQuery с элементом, являющимся заголовком ОТКРЫВАЮЩЕЙСЯ вкладки
  ui.oldHeader
//-||-||- ЗАКРЫВАЮЩЕЙСЯ вкладки
  ui.newContent
//объект jQuery с элементом, являющимся содержимым ОТКРЫВАЮЩЕЙСЯ вкладки
  ui.oldContent
//-||-||- ЗАКРЫВАЮЩЕЙСЯ вкладки
});
 
//обработка события changestart
$("selector").accordion({
   changestart:
function(event,ui)
{
... }
});
 
//еще один способ (используя метод bind)
$("selector").bind(
"accordionchangestart",
function(event,
ui){ ... });
<h2 id="remote"><a href="remoteAccordion.txt">Remote</a></h2>

<div></div>


(function($){

var accOpts = {

changestart: function(e, ui) {

if (ui.newHeader.attr("id") === "remote") {

$.get(ui.newHeader.find("a").attr("href"), function(data) {

ui.newHeader.next().text(data);

});

}

},

change: function(e, ui) {

ui.newHeader.closest("#myAccordion").accordion("resize");

}

};

$("#myAccordion").accordion(accOpts);

})(jQuery);



```

Accordion interoperability 17
```
<div id="myAccordion">

<h2><a href="#">Header 1</a></h2>

<h2><a href="#">Header 2</a></h2>

<h2><a href="#">Header 3</a></h2>

<div>

<div id="myTabs">

<ul>

<li><a href="#0"><span>Tab 1</span></a></li>

<li><a href="#1"><span>Tab 2</span></a></li>

</ul>

<div id="0">This is the content panel linked to the first tab, it is shown by default.</div>

<div id="1">This content is linked to the second tab and will be shown when its tab is clicked.</div>

</div>

</div>

</div>


(function($){

$("#myAccordion").accordion();

$("#myTabs").tabs();

})(jQuery);


```
19 fillSpace
```
<div id="container" class="ui-helper-clearfix">

<div id="myAccordion">

<h2><a href="#me" title="About Me">About Me</a></h2>

<div>

<a href="accordionMe.html#me" title="Bio">My Bio</a>

<a href="accordionMe.html#me" title="Contact Me">Contact Me</a>

<a href="accordionMe.html#me" title="Resume">My Resume</a>

</div>

<h2><a href="#js" title="JavaScript">JavaScript</a></h2>

<div>

<a href="accordionJS.html#js" title="Tutorials">Tutorials</a>

<a href="accordionJS.html#js" title="AJAX">AJAX</a>

<a href="accordionJS.html#js" title="Apps">Apps</a>

</div>

</div>

<div id="contentCol">

<h1>JavaScript</h1>

</div>

</div>


(function($){

var accOpts = {

fillSpace: true,

navigation: true

};

$("#myAccordion").accordion(accOpts);

})(jQuery);


```
20 navigation
```
<link rel="stylesheet" href="css/accordionTheme2.css">

<div id="container" class="ui-helper-clearfix">

<div id="myAccordion">

<h2><a href="#me" title="About Me">About Me</a></h2>

<div>

<a href="accordionMe.html#me" title="Bio">My Bio</a>

<a href="accordionMe.html#me" title="Contact Me">Contact Me</a>

<a href="accordionMe.html#me" title="Resume">My Resume</a>

</div>

<h2><a href="#js" title="JavaScript">JavaScript</a></h2>

<div>

<a href="accordionJS.html#js" title="Tutorials">Tutorials</a>

<a href="accordionJS.html#js" title="AJAX">AJAX</a>

<a href="accordionJS.html#js" title="Apps">Apps</a>

</div>

</div>

<div id="contentCol">

<h1>About Me</h1>

</div>

</div>


(function($){

var accOpts = {

fillSpace: true,

navigation: true

};

$("#myAccordion").accordion(accOpts);

})(jQuery);


```