# jsq-danco

## AngularJS

AngularJS связывает коды в единую систему, и вам не нужно больше обновлять HTML вручную или инспектировать элементы, как в случае, если вы используете JQuery. 

Для использования AngularJS вы должны добавить его в код своей страницы. Для этого в тэг нужно прописать соответствующие параметры. Google’s CDN для более быстрой загрузки рекомендую еще такой код:

<script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.0.7/angular.min.js"></script>
AngularJS включает в себя большое количество директив, которые позволяют связать HTML-элементы моделей. Они представляют из себя атрибуты, начинающиеся с префикса ng-, их можно добавлять к любому элементу. Самым важным атрибутом, который, если вы хотите использовать Angular, нужно включить во все страницы сайта является ng- приложений:
```
body ng-app
```
Атрибут следует добавлять к элементу, который охватывает нужную нам часть страницы: либо все тело страницы, либо ее часть ограниченную тэгами div. Angular ищет его при загрузке страницы и автоматически оценивает все директивы, которые видит, как дочерние элементы.

## Меню навигации

создадим меню навигации, в котором выделяется активный элемент. 

HTML:

```
<!-- Добавляем атрибут ng-app, который инициализирует запуск AngularJS -->
<div id="main" ng-app>
    <!-- Всем переменным классов в меню навигации будет присвоено значение "active". Функция $event.preventDefault() выводит страницу, которая была открыта по ссылке. -->
    <nav class="{{active}}" ng-click="$event.preventDefault()">
        <!-- Когда пункт меню открыт по ссылке, мы устанавливаем активные переменные -->
        <a href="#" class="home" ng-click="active='home'">Home</a>
        <a href="#" class="projects" ng-click="active='projects'">Projects</a>
        <a href="#" class="services" ng-click="active='services'">Services</a>
        <a href="#" class="contact" ng-click="active='contact'">Contact</a>
    </nav>
    <!-- ng-show выводит элемент, если значение переменной в кавычках соответствует истине. ng- hide – скрывает элемент, если наоборот. Так как изначально  активная переменная не установлена, то сперва на экране будет виден следующий текст -->
    <p ng-hide="active">Please click a menu item</p>
    <p ng-show="active">You chose <b>{{active}}</b></p>
</div>
```
CSS:
```
*{
    margin:0;
    padding:0;
}

body{
    font:15px/1.3 'Open Sans', sans-serif;
    color: #5e5b64;
    text-align:center;
}

a, a:visited {
    outline:none;
    color:#389dc1;
}

a:hover{
    text-decoration:none;
}

section, footer, header, aside, nav{
    display: block;
}

/*-------------------------
    Меню
--------------------------*/

nav{
    display:inline-block;
    margin:60px auto 45px;
    background-color:#5597b4;
    box-shadow:0 1px 1px #ccc;
    border-radius:2px;
}

nav a{
    display:inline-block;
    padding: 18px 30px;
    color:#fff !important;
    font-weight:bold;
    font-size:16px;
    text-decoration:none !important;
    line-height:1;
    text-transform: uppercase;
    background-color:transparent;

    -webkit-transition:background-color 0.25s;
    -moz-transition:background-color 0.25s;
    transition:background-color 0.25s;
}

nav a:first-child{
    border-radius:2px 0 0 2px;
}

nav a:last-child{
    border-radius:0 2px 2px 0;
}

nav.home .home,
nav.projects .projects,
nav.services .services,
nav.contact .contact{
    background-color:#e35885;
}

p{
    font-size:22px;
    font-weight:bold;
    color:#7d9098;
}

p b{
    color:#ffffff;
    display:inline-block;
    padding:5px 10px;
    background-color:#c4d7e0;
    border-radius:2px;
    text-transform:uppercase;
    font-size:18px;
}
```
используются директивы Angular для задания и считывания активной переменной. Когда она изменяется, это инициирует изменения HTML-кода элемента. В терминологии Angular эта переменная называется моделью. Она доступна для всех директив текущей области. Ее также могут обрабатывать контроллеры.

## {{VAR}}. 
Когда фреймворк видит такую строку, он заменяет содержимое переменной. Эта операция повторяется каждый раз, когда изменяется переменная.

## Встроенный редактор

создадим простой встроенный редактор – при нажатии пункта меню всплывает небольшое текстовое поле с подсказкой. Мы используем контроллер, который будет инициализировать модели и задавать два разных метода отображения подсказки. Контроллеры являются стандартными функциями JavaScript, которые автоматически выполняются фреймворком Angular. Они связаны с кодом отображения страницы вашего сайта через директивы ng-controller .

HTML:
```
<!-- Когда элемент выбран, всплывающая подсказка скрывается-->
<div id="main" ng-app ng-controller="InlineEditorController" ng-click="hideTooltip()">
    <!-- Это всплывающая подсказка. Она показывается только, когда значение переменной "showtooltip" – «истина» -->
    <div class="tooltip" ng-click="$event.stopPropagation()" ng-show="showtooltip">
        <!-- ng-модель связывает содержание текстового поля с моделью "value".
         Любые изменения текстового поля будут автоматически задаваться, как значение этой модели, а также вызывать изменения других элементов страницы, связанных с ней.  -->
        <input type="text" ng-model="value" />
    </div>
    <!-- Выбор метода отображения подсказки из вариантов заданных в InlineEditorController (контроллере встроенного редактора), он зависит от значения переменной "showtooltip". -->
    <p ng-click="toggleTooltip($event)">{{value}}</p>
</div>
```
JS:
```
// Контроллер – стандартная функция. Она инициируется, когда 
AngularJS при обработке кода находит атрибут ng-controller.

function InlineEditorController($scope){

    // $scope – специальный объект, который задает параметры отображения 
    // переменной. Здесь вы можете задать некоторые значения по умолчанию   
   
    $scope.showtooltip = false;
    $scope.value = 'Edit me.';

    // Некоторые вспомогательные функции, которые доступны после инициации  // Аngular.

    $scope.hideTooltip = function(){

    // Когда значение модели меняется, AngularJS автоматически вносит       // изменения в формат вывода. И всплывающее меню скрывается с экрана.


        $scope.showtooltip = false;
    }

    $scope.toggleTooltip = function(e){
        e.stopPropagation();
        $scope.showtooltip = !$scope.showtooltip;
    }
}
```
CSS:
```
*{
    margin:0;
    padding:0;
}

body{
    font:15px/1.3 'Open Sans', sans-serif;
    color: #5e5b64;
    text-align:center;
}

a, a:visited {
    outline:none;
    color:#389dc1;
}

a:hover{
    text-decoration:none;
}

section, footer, header, aside, nav{
    display: block;
}

/*-------------------------
    Всплывающее меню редактора.
--------------------------*/

.tooltip{
    background-color:#5c9bb7;

    background-image:-webkit-linear-gradient(top, #5c9bb7, #5392ad);
    background-image:-moz-linear-gradient(top, #5c9bb7, #5392ad);
    background-image:linear-gradient(top, #5c9bb7, #5392ad);

    box-shadow: 0 1px 1px #ccc;
    border-radius:3px;
    width: 290px;
    padding: 10px;

    position: absolute;
    left:50%;
    margin-left:-150px;
    top: 80px;
}

.tooltip:after{
    /* The tip of the tooltip */
    content:'';
    position:absolute;
    border:6px solid #5190ac;
    border-color:#5190ac transparent transparent;
    width:0;
    height:0;
    bottom:-12px;
    left:50%;
    margin-left:-6px;
}

.tooltip input{
    border: none;
    width: 100%;
    line-height: 34px;
    border-radius: 3px;
    box-shadow: 0 2px 6px #bbb inset;
    text-align: center;
    font-size: 16px;
    font-family: inherit;
    color: #8d9395;
    font-weight: bold;
    outline: none;
}

p{
    font-size:22px;
    font-weight:bold;
    color:#6d8088;
    height: 30px;
    cursor:default;
}

p b{
    color:#ffffff;
    display:inline-block;
    padding:5px 10px;
    background-color:#c4d7e0;
    border-radius:2px;
    text-transform:uppercase;
    font-size:18px;
}

p:before{
    content:'&#9998;';
    display:inline-block;
    margin-right:5px;
    font-weight:normal;
    vertical-align: text-bottom;
}

#main{
    height:300px;
    position:relative;
    padding-top: 150px;
}
```
Когда функция контроллера запускается на исполнение, для нее в качестве параметра задается специальный объект $scope. Он отвечает за ввод текста в текстовый редактор. Для того, чтобы вывести его на экран, нужно прописать дополнительные свойства и функции, которые описывают отображение его элементов. С помощью NG-моделей осуществляется связь кода сайта с текстом, который вводится в рабочее поле редактора. При вводе текста Angular задает соответствующие изменения переменных.

## Форма заказа

рассмотрим код формы заказы, в которой автоматически выводится общая сумма. Здесь использована еще одна полезная функция AngularJS - фильтры. Фильтры позволяют вносить изменения в модели, а также объединять их с помощью символа «|». В примере, используется фильтр валюты, чтобы перевести числовое значение в корректный формат цены - с разделением долларов и центов. 

HTML:
```

<!-- Объявление нового приложения AngularJS и связанного с ним контроллера -->
<form ng-app ng-controller="OrderFormController">
    <h1>Services</h1>
    <ul>
        <!-- Запуск цикла обработки массива с перечнем услуг, назначается при нажатии элемента. При этом если нужно устанавливается активный css-класс. -->
        <li ng-repeat="service in services" ng-click="toggleActive(service)" ng-class="{active:service.active}">
            <!-- Обратите внимание на использование фильтра валюты, он задает формат вывода цены. -->
            {{service.name}} <span>{{service.price | currency}}</span>
        </li>
    </ul>
    <div class="total">
        <!-- Подсчет общей стоимости всех выбранных услуг. Выводится по заданному формату валюты. -->
        Total: <span>{{total() | currency}}</span>
    </div>
```
JS:
```
function OrderFormController($scope){

// Определение параметров модели. Вид отображения будет зависеть от
// обработки циклом массива перечня услуг, для которых автоматически будет  // сгенерирован формат вывода списком через тэг li.

    $scope.services = [
        {
            name: 'Web Development',
            price: 300,
            active:true
        },{
            name: 'Design',
            price: 400,
            active:false
        },{
            name: 'Integration',
            price: 250,
            active:false
        },{
            name: 'Training',
            price: 220,
            active:false
        }
    ];

    $scope.toggleActive = function(s){
        s.active = !s.active;
    };

    // Вспомогательный метод подсчета общей суммы по всем выбранным
    // позициям.

    $scope.total = function(){

        var total = 0;

        // Use the angular forEach helper method to
        // loop through the services array:

        angular.forEach($scope.services, function(s){
            if (s.active){
                total+= s.price;
            }
        });

        return total;
    };
}
```
CSS:
```
*{
    margin:0;
    padding:0;
}

body{
    font:15px/1.3 'Open Sans', sans-serif;
    color: #5e5b64;
    text-align:center;
}

a, a:visited {
    outline:none;
    color:#389dc1;
}

a:hover{
    text-decoration:none;
}

section, footer, header, aside, nav{
    display: block;
}

/*-------------------------
    Форма заказа
--------------------------*/

form{
    background-color: #61a1bc;
    border-radius: 2px;
    box-shadow: 0 1px 1px #ccc;
    width: 400px;
    padding: 35px 60px;
    margin: 50px auto;
}

form h1{
    color:#fff;
    font-size:64px;
    font-family:'Cookie', cursive;
    font-weight: normal;
    line-height:1;
    text-shadow:0 3px 0 rgba(0,0,0,0.1);
}

form ul{
    list-style:none;
    color:#fff;
    font-size:20px;
    font-weight:bold;
    text-align: left;
    margin:20px 0 15px;
}

form ul li{
    padding:20px 30px;
    background-color:#e35885;
    margin-bottom:8px;
    box-shadow:0 1px 1px rgba(0,0,0,0.1);
    cursor:pointer;
}

form ul li span{
    float:right;
}

form ul li.active{
    background-color:#8ec16d;
}

div.total{
    border-top:1px solid rgba(255,255,255,0.5);
    padding:15px 30px;
    font-size:20px;
    font-weight:bold;
    text-align: left;
    color:#fff;
}

div.total span{
    float:right;
}
```
Связка ng-repeat – это еще один полезный элемент Angular. Она позволяет запустить цикл обработки массива элементов, а также задать разметку для каждого из них. Она автоматически обновляет код, если один из элементов был изменен или удален.

## Функция поиска

функция, позволяющая фильтровать список элементов по определенному критерию. 

Модули представляют собой форму организации приложений JavaScript в автономные компоненты, которые можно связывать между собою в разных вариантах и последовательностях. Angular также использует этот метод группировки кодов. Потому прежде, чем создавать фильтр, нужно сначала создать модули для разных приложений.

Для того, чтобы создать модуль приложения, нужно выполнить два действия:

1. Использовать функцию angular.module("name",[]) при вызове JS. Это установит границы нового модуля;
2. Задать имя модуля в качестве значения директивы ng-app.
После этого фильтр создается функцией filter(). 
потом вызвать его через обращение к соответствующему модулю angular.module("name", []).

HTML:
```
—Инициализация нового приложения AngularJS и увязка его с модулем "instantSearch"
<div ng-app="instantSearch" ng-controller="InstantSearchController">

    <div class="bar">
        <!—Создание взаимосвязи между моделью searchString и текстовым полем -->
        <input type="text" ng-model="searchString" placeholder="Enter your search terms" />
    </div>

    <ul>
        <!-- Назначение формата вывода списком через разметку тэга li для всех элементов массива. Примечание: фильтр пользовательского поиска задается через переменную "searchFor". В качестве аргумента она принимает значение модели searchString
         -->
        <li ng-repeat="i in items | searchFor:searchString">
            <a href="{{i.url}}"><img ng-src="{{i.image}}" /></a>
            <p>{{i.title}}</p>
        </li>
    </ul>
</div>
```
JS:
```
// Задается новый модуль для нашего приложения. Массив содержит имена всех 
// зависимых элементов, если таковые имеются.

 var app = angular.module("instantSearch", []);

// Создается новый фильтр для поиска

app.filter('searchFor', function(){

    // Все фильтры должны вызываться через функцию. Первым параметром
    // выступает массив данных, которые нужно обработать. В качестве второго
    // параметра задается аргумент, по которому мы будем отфильтровывать всю    
    // последовательность данных (searchFor:searchString)

    return function(arr, searchString){

        if(!searchString){
            return arr;
        }

        var result = [];

        searchString = searchString.toLowerCase();

        // С помощью функции forEach производится обработка всего массива       
        // данных циклом. 
        angular.forEach(arr, function(item){

            if(item.title.toLowerCase().indexOf(searchString) !== -1){
                result.push(item);
            }

        });

        return result;
    };

});

// Контроллер

function InstantSearchController($scope){

    // Модель данных. Как правило, элементы вызываются через AJAX

    $scope.items = [
        {
            url: 'http://tutorialzine.com/2013/07/50-must-have-plugins-for-extending-twitter-bootstrap/',
            title: '50 Must-have plugins for extending Twitter Bootstrap',
            image: 'http://cdn.tutorialzine.com/wp-content/uploads/2013/07/featured_4-100x100.jpg'
        },
        {
            url: 'http://tutorialzine.com/2013/08/simple-registration-system-php-mysql/',
            title: 'Making a Super Simple Registration System With PHP and MySQL',
            image: 'http://cdn.tutorialzine.com/wp-content/uploads/2013/08/simple_registration_system-100x100.jpg'
        },
        {
            url: 'http://tutorialzine.com/2013/08/slideout-footer-css/',
            title: 'Create a slide-out footer with this neat z-index trick',
            image: 'http://cdn.tutorialzine.com/wp-content/uploads/2013/08/slide-out-footer-100x100.jpg'
        },
        {
            url: 'http://tutorialzine.com/2013/06/digital-clock/',
            title: 'How to Make a Digital Clock with jQuery and CSS3',
            image: 'http://cdn.tutorialzine.com/wp-content/uploads/2013/06/digital_clock-100x100.jpg'
        },
        {
            url: 'http://tutorialzine.com/2013/05/diagonal-fade-gallery/',
            title: 'Smooth Diagonal Fade Gallery with CSS3 Transitions',
            image: 'http://cdn.tutorialzine.com/wp-content/uploads/2013/05/featured-100x100.jpg'
        },
        {
            url: 'http://tutorialzine.com/2013/05/mini-ajax-file-upload-form/',
            title: 'Mini AJAX File Upload Form',
            image: 'http://cdn.tutorialzine.com/wp-content/uploads/2013/05/ajax-file-upload-form-100x100.jpg'
        },
        {
            url: 'http://tutorialzine.com/2013/04/services-chooser-backbone-js/',
            title: 'Your First Backbone.js App – Service Chooser',
            image: 'http://cdn.tutorialzine.com/wp-content/uploads/2013/04/service_chooser_form-100x100.jpg'
        }
    ];

}
```
CSS:
```
*{
    margin:0;
    padding:0;
}

body{
    font:15px/1.3 'Open Sans', sans-serif;
    color: #5e5b64;
    text-align:center;
}

a, a:visited {
    outline:none;
    color:#389dc1;
}

a:hover{
    text-decoration:none;
}

section, footer, header, aside, nav{
    display: block;
}

/*-------------------------
    Форма заказа
--------------------------*/

form{
    background-color: #61a1bc;
    border-radius: 2px;
    box-shadow: 0 1px 1px #ccc;
    width: 400px;
    padding: 35px 60px;
    margin: 50px auto;
}

form h1{
    color:#fff;
    font-size:64px;
    font-family:'Cookie', cursive;
    font-weight: normal;
    line-height:1;
    text-shadow:0 3px 0 rgba(0,0,0,0.1);
}

form ul{
    list-style:none;
    color:#fff;
    font-size:20px;
    font-weight:bold;
    text-align: left;
    margin:20px 0 15px;
}

form ul li{
    padding:20px 30px;
    background-color:#e35885;
    margin-bottom:8px;
    box-shadow:0 1px 1px rgba(0,0,0,0.1);
    cursor:pointer;
}

form ul li span{
    float:right;
}

form ul li.active{
    background-color:#8ec16d;
}

div.total{
    border-top:1px solid rgba(255,255,255,0.5);
    padding:15px 30px;
    font-size:20px;
    font-weight:bold;
    text-align: left;
    color:#fff;
}

div.total span{
    float:right;
}
```
В создании различных фильтров используется подход, базирующийся на общей философии AngularJS. В соответствии с ней каждая часть кода, который вы пишете, должна быть автономной, легко тестируемой, а также иметь возможность использоваться разными элементами фреймворка. Вы можете применять созданный однажды фильтр для обработки данных в рамках других приложений. И даже объединять его в последовательности с другими фильтрами.

## Функция переключения режима вывода элементов на странице

переключение по выбору пользователя различных режимов вывода элементов на странице (список или плитка).

## сервисы. 

Это объекты, которые могут быть использованы приложениями для взаимодействия с сервером, API или другими источниками данных. В нашем случае, мы напишем сервис, который взаимодействует с Instagram’s API и выводит массив с самыми популярными на текущий момент фотографиями.

Обратите внимание, что для работы этого кода, нам потребуется использовать на странице дополнительный файл Angular.js:
```
<script src="http://ajax.googleapis.com/ajax/libs/angularjs/1.0.7/angular-resource.min.js"></script>
```
Для оптимизации работы с AJAX API здесь используется модуль ngResource (в коде модуля задействована переменная $resource).

HTML:
```
<div ng-app="switchableGrid" ng-controller="SwitchableGridController">

    <div class="bar">

        <!—Это две кнопки переключения между режимами вывода элементов. С их помощью задается корректный формат вывода элементов списка UL. 
-->

        <a class="list-icon" ng-class="{active: layout == 'list'}" ng-click="layout = 'list'"></a>
        <a class="grid-icon" ng-class="{active: layout == 'grid'}" ng-click="layout = 'grid'"></a>
    </div>

    <!—У нас есть два варианта раскладки. Мы выбираем, какой из них нам нужен в зависимости от параметров переменной "layout" -->

    <ul ng-show="layout == 'grid'" class="grid">
        <!-- A view with big photos and no text -->
        <li ng-repeat="p in pics">
            <a href="{{p.link}}" target="_blank"><img ng-src="{{p.images.low_resolution.url}}" /></a>
        </li>
    </ul>

    <ul ng-show="layout == 'list'" class="list">
        <!-- A compact view smaller photos and titles -->
        <li ng-repeat="p in pics">
            <a href="{{p.link}}" target="_blank"><img ng-src="{{p.images.thumbnail.url}}" /></a>
            <p>{{p.caption.text}}</p>
        </li>
    </ul>
</div>
```
JS:
```

// Задаем новый модуль. в нем мы прописываем связь с модулем
 // ngResource, который предназначен для поддержки работы с Instagram API.

var app = angular.module("switchableGrid", ['ngResource']);

// Создаем и регистрируем новый сервис "instagram"

app.factory('instagram', function($resource){

    return {
        fetchPopular: function(callback){

// В модуле ngResource уже прописан сервис $resource service.           
// Он предназначен для оптимизации работы с AJAX. Здесь мы          
// используем приложения client_id. Если необходимо, вы можете          
// удалить или переместить его по своему усмотрению.

            var api = $resource('https://api.instagram.com/v1/media/popular?client_id=:client_id&callback=JSON_CALLBACK',{
                client_id: '642176ece1e7445e99244cec26f4de1f'
            },{
// Этот код запускает функцию, которую мы назвали "fetch".              
// Она отправляет JSONP-запрос к URL источника. При отклике на
// JSONP-запрос к URL-адресам добавляется запись
// =JSON_CALLBACK
                
                fetch:{method:'JSONP'}
            });

            api.fetch(function(response){

            // Вызов функции, которая задает вывод результатов                  // обработки данных
                callback(response.data);

            });
        }
    }

});

// Контроллер. в него включен новый сервис instagram, 
// который мы задали ранее. Он будет доступен внутри функции автоматически.

function SwitchableGridController($scope, instagram){

    // Режим вывода по умолчанию. Кликнув на соответствующую кнопку, мы
    // можем выбрать тот вариант вывода, который нам нужен.
    
    $scope.layout = 'grid';

    $scope.pics = [];

    // Запускаем сервис instagram и выводим список популярных фото.

    instagram.fetchPopular(function(data){

        // Задаем массив данных (фото), которые будут обработаны Angular 
        // автоматически.
        $scope.pics = data;
    });
```
CSS:
```
*{
    margin:0;
    padding:0;
}

body{
    font:15px/1.3 'Open Sans', sans-serif;
    color: #5e5b64;
    text-align:center;
}

a, a:visited {
    outline:none;
    color:#389dc1;
}

a:hover{
    text-decoration:none;
}

section, footer, header, aside, nav{
    display: block;
}

/*-------------------------
    Форма для задания аргумента поиска
--------------------------*/

.bar{
    background-color:#5c9bb7;

    background-image:-webkit-linear-gradient(top, #5c9bb7, #5392ad);
    background-image:-moz-linear-gradient(top, #5c9bb7, #5392ad);
    background-image:linear-gradient(top, #5c9bb7, #5392ad);

    box-shadow: 0 1px 1px #ccc;
    border-radius: 2px;
    width: 580px;
    padding: 10px;
    margin: 45px auto 25px;
    position:relative;
    text-align:right;
    line-height: 1;
}

.bar a{
    background:#4987a1 center center no-repeat;
    width:32px;
    height:32px;
    display:inline-block;
    text-decoration:none !important;
    margin-right:5px;
    border-radius:2px;
    cursor:pointer;
}

.bar a.active{
    background-color:#c14694;
}

.bar a.list-icon{
    background-image:url(data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABAAAAAQCAYAAAAf8/9hAAAAGXRFWHRTb2Z0d2FyZQBBZG9iZSBJbWFnZVJlYWR5ccllPAAAAyBpVFh0WE1MOmNvbS5hZG9iZS54bXAAAAAAADw/eHBhY2tldCBiZWdpbj0i77u/IiBpZD0iVzVNME1wQ2VoaUh6cmVTek5UY3prYzlkIj8+IDx4OnhtcG1ldGEgeG1sbnM6eD0iYWRvYmU6bnM6bWV0YS8iIHg6eG1wdGs9IkFkb2JlIFhNUCBDb3JlIDUuMC1jMDYwIDYxLjEzNDc3NywgMjAxMC8wMi8xMi0xNzozMjowMCAgICAgICAgIj4gPHJkZjpSREYgeG1sbnM6cmRmPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5LzAyLzIyLXJkZi1zeW50YXgtbnMjIj4gPHJkZjpEZXNjcmlwdGlvbiByZGY6YWJvdXQ9IiIgeG1sbnM6eG1wPSJodHRwOi8vbnMuYWRvYmUuY29tL3hhcC8xLjAvIiB4bWxuczp4bXBNTT0iaHR0cDovL25zLmFkb2JlLmNvbS94YXAvMS4wL21tLyIgeG1sbnM6c3RSZWY9Imh0dHA6Ly9ucy5hZG9iZS5jb20veGFwLzEuMC9zVHlwZS9SZXNvdXJjZVJlZiMiIHhtcDpDcmVhdG9yVG9vbD0iQWRvYmUgUGhvdG9zaG9wIENTNSBXaW5kb3dzIiB4bXBNTTpJbnN0YW5jZUlEPSJ4bXAuaWlkOkYzNkFCQ0ZBMTBCRTExRTM5NDk4RDFEM0E5RkQ1NEZCIiB4bXBNTTpEb2N1bWVudElEPSJ4bXAuZGlkOkYzNkFCQ0ZCMTBCRTExRTM5NDk4RDFEM0E5RkQ1NEZCIj4gPHhtcE1NOkRlcml2ZWRGcm9tIHN0UmVmOmluc3RhbmNlSUQ9InhtcC5paWQ6RjM2QUJDRjgxMEJFMTFFMzk0OThEMUQzQTlGRDU0RkIiIHN0UmVmOmRvY3VtZW50SUQ9InhtcC5kaWQ6RjM2QUJDRjkxMEJFMTFFMzk0OThEMUQzQTlGRDU0RkIiLz4gPC9yZGY6RGVzY3JpcHRpb24+IDwvcmRmOlJERj4gPC94OnhtcG1ldGE+IDw/eHBhY2tldCBlbmQ9InIiPz7h1bLqAAAAWUlEQVR42mL8////BwYGBn4GCACxBRlIAIxAA/4jaXoPEkMyjJ+A/g9MDJQBRhYg8RFqMwg8RJIUINYLFDmBUi+ADQAF1n8ofk9yIAy6WPg4GgtDMRYAAgwAdLYwLAoIwPgAAAAASUVORK5CYII=);
}

.bar a.grid-icon{
    background-image:url(data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABAAAAAQCAYAAAAf8/9hAAAAGXRFWHRTb2Z0d2FyZQBBZG9iZSBJbWFnZVJlYWR5ccllPAAAAyBpVFh0WE1MOmNvbS5hZG9iZS54bXAAAAAAADw/eHBhY2tldCBiZWdpbj0i77u/IiBpZD0iVzVNME1wQ2VoaUh6cmVTek5UY3prYzlkIj8+IDx4OnhtcG1ldGEgeG1sbnM6eD0iYWRvYmU6bnM6bWV0YS8iIHg6eG1wdGs9IkFkb2JlIFhNUCBDb3JlIDUuMC1jMDYwIDYxLjEzNDc3NywgMjAxMC8wMi8xMi0xNzozMjowMCAgICAgICAgIj4gPHJkZjpSREYgeG1sbnM6cmRmPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5LzAyLzIyLXJkZi1zeW50YXgtbnMjIj4gPHJkZjpEZXNjcmlwdGlvbiByZGY6YWJvdXQ9IiIgeG1sbnM6eG1wPSJodHRwOi8vbnMuYWRvYmUuY29tL3hhcC8xLjAvIiB4bWxuczp4bXBNTT0iaHR0cDovL25zLmFkb2JlLmNvbS94YXAvMS4wL21tLyIgeG1sbnM6c3RSZWY9Imh0dHA6Ly9ucy5hZG9iZS5jb20veGFwLzEuMC9zVHlwZS9SZXNvdXJjZVJlZiMiIHhtcDpDcmVhdG9yVG9vbD0iQWRvYmUgUGhvdG9zaG9wIENTNSBXaW5kb3dzIiB4bXBNTTpJbnN0YW5jZUlEPSJ4bXAuaWlkOjBEQkMyQzE0MTBCRjExRTNBMDlGRTYyOTlBNDdCN0I4IiB4bXBNTTpEb2N1bWVudElEPSJ4bXAuZGlkOjBEQkMyQzE1MTBCRjExRTNBMDlGRTYyOTlBNDdCN0I4Ij4gPHhtcE1NOkRlcml2ZWRGcm9tIHN0UmVmOmluc3RhbmNlSUQ9InhtcC5paWQ6MERCQzJDMTIxMEJGMTFFM0EwOUZFNjI5OUE0N0I3QjgiIHN0UmVmOmRvY3VtZW50SUQ9InhtcC5kaWQ6MERCQzJDMTMxMEJGMTFFM0EwOUZFNjI5OUE0N0I3QjgiLz4gPC9yZGY6RGVzY3JpcHRpb24+IDwvcmRmOlJERj4gPC94OnhtcG1ldGE+IDw/eHBhY2tldCBlbmQ9InIiPz4MjPshAAAAXklEQVR42mL4////h/8I8B6IGaCYKHFGEMnAwCDIAAHvgZgRyiZKnImBQsACxB+hNoDAQyQ5osQZIT4gH1DsBZABH6AB8x/JaQzEig++WPiII7Rxio/GwmCIBYAAAwAwVIzMp1R0aQAAAABJRU5ErkJggg==);
}

.bar input{
    background:#fff no-repeat 13px 13px;

    border: none;
    width: 100%;
    line-height: 19px;
    padding: 11px 0;

    border-radius: 2px;
    box-shadow: 0 2px 8px #c4c4c4 inset;
    text-align: left;
    font-size: 14px;
    font-family: inherit;
    color: #738289;
    font-weight: bold;
    outline: none;
    text-indent: 40px;
}

/*-------------------------
    Режим вывода «список»
--------------------------*/

ul.list{
    list-style: none;
    width: 500px;
    margin: 0 auto;
    text-align: left;
}

ul.list li{
    border-bottom: 1px solid #ddd;
    padding: 10px;
    overflow: hidden;
}

ul.list li img{
    width:120px;
    height:120px;
    float:left;
    border:none;
}

ul.list li p{
    margin-left: 135px;
    font-weight: bold;
    color:#6e7a7f;
}

/*-------------------------
    Режим вывода «плитка»
--------------------------*/

ul.grid{
    list-style: none;
    width: 570px;
    margin: 0 auto;
    text-align: left;
}

ul.grid li{
    padding: 2px;
    float:left;
}

ul.grid li img{
    width:280px;
    height:280px;
    display:block;
    border:none;
}
```
Сервисы – это полностью автономные элементы, что делает возможным написание различных вариантов модулей для реализации процесса, при этом не затрагивая остальную часть кода.

Например, во время тестирования, вы можете предпочесть выводить данные из четко заданного массива фотографий (без фильтров и обработки), что ускорит отладку всей системы.

