# jsq-danco

Web разработка на node.js и express
===================================
node.js - http://nodejs.org/
----------------------------
это серверная платформа, для выполнения javascript. 
express - web-фреймворк построеный на концепции middleware

Рабочее окружение
------------------
Установка git
-------------
```
$ sudo apt-get install git-core
```

http://git-scm.com/book/ch1-4.html

Установка node.js и npm
------------------------
```
$ sudo apt-get install python-software-properties
$ sudo add-apt-repository ppa:chris-lea/node.js
$ sudo apt-get update
$ sudo apt-get install nodejs npm
```

Среда разработки
----------------

Express и первое приложение
-----------------------------

Устанавливаем express глобально:
--------------------------------
```
$ sudo npm install -g express
```
Создаем директорию для наших учебных проектов:
----------------------------------------------
```
$ mkdir -p ~/projects/shop
$ cd ~/projects/nshop
```
Создаем проект и устанавливаем зависимости:
-------------------------------------------
```
$ express app
$ cd app && npm install
```
Теперь приложение можно запустить:
-----------------------------------
```
$ node app

```
И увидеть результат работы http://localhost:3000/


Использование шаблонизаторов в Express
======================================
Для того чтобы отображать в Express файлы шаблонов, необходимо задать следующие параметры приложения:

- views, каталог, в котором находятся файлы шаблонов. Например: app.set('views', './views')
- view engine, используемый шаблонизатор. Например: app.set('view engine', 'jade')

Затем установите соответствующий пакет npm шаблонизатора:
```
$ npm install jade --save
```
Шаблонизаторы, совместимые с Express, например, Jade, экспортируют функцию __express(filePath, options, callback), вызываемую с помощью функции res.render() для вывода кода шаблона.

Это правило действует не для всех шаблонизаторов. Библиотека Consolidate.js соблюдает его путем преобразования всех популярных шаблонизаторов Node.js, благодаря чему работает в Express без проблем.
Express загружает модуль внутренними средствами.

```
app.set('view engine', 'jade');
```
Создайте файл шаблона Jade с именем index.jade в каталоге views со следующим содержанием:
```

html
  head
    title!= title
  body
    h1!= message
```
Затем создайте маршрут для вывода файла index.jade. Если свойство view engine не задано, необходимо указать расширение файла view. В противном случае, можно не указывать расширение.
```

app.get('/', function (req, res) {
  res.render('index', { title: 'Hey', message: 'Hello there!'});
});
```
При выполнении запроса к домашней странице файл index.jade будет отображаться как HTML.

layout.jade
-----------
```
doctype html
html
  head
    title= title
    meta(charset='UTF-8')
    meta(name='viewport' content='width=device-width, initial-scale=1.0')
    script(src='/javascripts/modernizr.js' type='text/javascript')
    
    link(rel='stylesheet', href='/stylesheets/main.css')
    link(rel='stylesheet prefetch' href='/stylesheets/normalize.css')
    script(src='/javascripts/prefixfree.min.js')
    script(src='/javascripts/jquery.min.js')
    script(src='/javascripts/cart.js')
  body
    block content
```
index.jade
----------
```
extends layout

block content
  #cart
      h2 Your Shopping Cart
      |   
      ul.cart-items
      |   
      .total
        .subtotalTotal
          | Subtotal
          span $0.00
        |     
        .taxes
          | Tax
          span $0.00
        |     
        .shipping
          | Shipping
          span $0.00
        |     
        .finalTotal
          | Total
          span $0.00
        |     
        a.checkout
          | Check Out
        |     
        p.error
        |         
        #payment_wrapper(style='display:none')
          #payment
            p.headings Pay for your products
            |                                           
            p Enter your credit / debit details:
            |       
            |                               
            ul
              li
                label.card Card type
                |    
                |                                                 
                select#cardType(name='cardtype')
                  option(selected='selected' value='Visa Debit') Visa Debit
                  |                                                 
                  option(value='Mastercard') Mastercard
                  |                                                 
                  option(value='Visa Credit') Visa Credit
                  |                                                 
                  option(value='Electron') Electron
                  |                                                 
                  option(value='Solo') Solo
            |                                                   
            ul
              li
                label.card Card number
                |                                                 
                input#cardNumber(type='text')
            |                                                 
            ul
              li
                label.card Name on card
                |                                                 
                input#cardholderName(type='text')
            |                             
            ul
              li
                label.card Expiration Date 
                |                                                 
                select#expirationMonth
                  option(selected='selected' value='0') month
                  |                                                 
                  option(value='01') 01
                  |                                                 
                  option(value='02') 02
                  |                                                 
                  option(value='03') 03
                  |                                                 
                  option(value='04') 04
                  |                                                 
                  option(value='05') 05
                  |                                                 
                  option(value='06') 06
                  |                                                 
                  option(value='07') 07
                  |                                                 
                  option(value='08') 08
                  |                                                 
                  option(value='09') 09
                  |                                                 
                  option(value='10') 10
                  |                                                 
                  option(value='11') 11
                  |                                                 
                  option(value='12') 12
                |                                                 
                |                                                 
                select#expirationYear(name='expirationYear')
                  option(selected='selected' value='0') year
                  |                                                
                  |                                                 
                  |                                                 
                  option(value='13') 13
                  |                                                 
                  option(value='14') 14
                  |                                                 
                  option(value='15') 15
                  |                                                 
                  option(value='16') 16
                  |                                                 
                  option(value='17') 17
                  |                                                 
                  option(value='18') 18
            |                             
            ul
              li
                label#moko.card(for='cv2') 3 Digit Verification Number
                |                                                 
                input#cv2(size='3' maxlength='3' type='text')
          // end payment
          p.headings  Personal details
          |                                  
          ul
            li
              label.box Title
              |                                             
              select#title
                option(selected='selected' value='Mr') Mr
                |                                             
                option(value='Ms') Ms
                |                                             
                option(value='Mrs') Mrs
                |                                             
                option(value='Miss') Miss
          |  
          |                                                
          |                           
          |                                         
          ul
            li
              label.box First name
              |                                         
              input#firstName(type='text')
          |                                         
          ul
            li
              label.box Surname
              |                                         
              input#surName(type='text')
          |                                          
          ul
            li
              label.box Address
              |                                          
              input#address(type='text')
          |                                          
          ul
            li
              label.box Address Line 2
              |                                          
              input#addressLine2(type='text')
          |                                          
          ul
            li
              label.box Town/City
              |                                          
              input#town(type='text')
          |                                          
          ul
            li
              label.box Post code
              |                                          
              input#postCode(type='text')
          // end left_content
          p.headings Dispatching to
          |                                                           
          |                                         
          ul
            li
              label.box Title
              |                                         
              select#sendingTitle
                option(selected='selected' value='Mr') Mr
                |                                         
                option(value='Ms') Ms
                |                                         
                option(value='Mrs') Mrs
                |                                         
                option(value='Miss') Miss
          |  
          |                                       
          ul
            li
              label.box First name
              |                                         
              input#sendingFirstName(type='text')
          |                                         
          ul
            li
              label.box Surname
              |                                         
              input#sendingSurname(type='text')
          |                                          
          ul
            li
              label.box Address
              |                                         
              input#sendingAddress(type='text')
          |                                          
          ul
            li
              label.box Address Line 2
              |                                         
              input#sendingAddressLine2(type='text')
          |                                          
          ul
            li
              label.box Town/City
              |                                          
              input#sendingTown(type='text')
          |                                          
          ul
            li
              label.box Post code
              |                                          
              input#sendingPostCode(type='text')
          // end right content
          input#calculateButton.detalis(name='Place your order' value='Place your order' onclick='takeDetalis()' type='button')
          |                                      
          |                                       
          |                   
          #details
            .leftdetalis
              p Personal detalis
              |                                                     
              span#dispTitle
              |                                                     
              span#dispFirstName
              |                                                     
              span#dispSurname
              br
              |                                                     
              span#dispAddress
              |                                                     
              span#dispAddressLine2
              br
              |                                                     
              span#dispTown
              br
              |                                                     
              span#dispPostCode
            // end leftdetalis
            .rightdetalis
              p Delivery detalis
              |                                                                      
              span#dispSenTitle
              |                                                                      
              span#dispSenFirstName
              |                                                                      
              span#dispSenSurname
              br
              |                                                                  
              span#dispSenAddress
              |          
              |                                                                  
              span#dispSenAddressLine2
              br
              |                                                                  
              span#dispSenTown
              br
              |                                                                  
              span#dispSenPostCode
            // end rightdetalis
        // end payment_wrapper
    #wrap.wrap
      header
        a.logo(href='#')
          | Home 
          span.brandico-github
          |  Catalog
        |     
        a.cart-link(href='#menu')
          span.cart-text.fontawesome-shopping-cart
            span Cart
          |       
          span.returnToShop &larr; Back
          |       
          span.cart-quantity.empty 0
      |   
      section.shop
      |   
      footer
        p Happy Shopping.
      script#productTemplate(type='text/template').
       <div class="product">
       <h1></h1>
       <p></p>
       <div class="button">
       <div class="price"></div>
       <a class="addtocart">
       <div class="add">Add to Cart</div>
       <div class="added">Added!</div>
       </a>
       </div>
       </div>
     script#cartItem(type='text/template').
       <li><div class="cart-product">
       <input class="quantity" value="1">
       </div><div class="cart-description">
       <h3></h3>
       <span class="subtotal"></span>
       </div></li>

```

HTML to Jade conversion tool
============================
Install
--------
```
npm install -g html2jade
```

Command-line Usage
-------------------
```
html2jade mywebpage.html # outputs mywebpage.jade
html2jade public/*.html  # converts all .html files to .jade
```

Online converter
----------------
http://html2jade.org/

HTML as the view engine in Express
-----------------------------------
```
 npm install consolidate
 npm install swig
```

app.js file
------------
```
var cons = require('consolidate');

// view engine setup
app.engine('html', cons.swig)
app.set('views', path.join(__dirname, 'views'));
app.set('view engine', ‘html');
```

Model-View-Controller (MVC)
===========================
типичная архитектура web-приложения на наиболее высоком уровне абстракции. Самым популярным архитектурным паттерном на сегодняшний день является model-view-controller (MVC), общий смысл паттерна заключается в том, чтобы разделить бизнес логику приложения (её привязывают к моделям) и представление - view. Кроме того, модели реализуют интерфейс к базе данных. Контроллер играет роль посредника между моделью и представлением. В случае web-приложения - это выглядит так: браузер пользователя отправляет запрос на сервер, контроллер обрабатывает запрос, получает необходимые данные из модели и отправляет их во view. View получает данные из контроллера и превращает их в красивую HTML страничку, которую контроллер в итоге отправит пользователю.

Пакеты npm - node package manager
---------------------------------
 В общих чертах пакет npm - это директория содержащая программу и файл package.json, описывающий эту программу, в том числе в этом файле можно указать от каких других пакетов зависит наша программа. 

 создадим в корневой директории нашего проекта файлик:
```
$ touch package.json
package.json:

{
    "name": "node-demo-app"
  , "version": "0.0.1"
  , "scripts": { "start": "node server.js" }
  , "dependencies": { "express": "3.0.x" }
}
```
Теперь можно выполнить
```
$ npm install
```
В результате npm создаст директорию node_modules в которую поместит все модули от которых зависит наш проект.

JSON
=====

Объект JSON содержит методы для разбора объектной нотации JavaScript (JavaScript Object Notation — сокращённо JSON) и преобразования значений в JSON. Его нельзя вызвать как функцию или сконструировать как объект, и кроме своих двух методов он не содержит никакой интересной функциональности.

Объектная нотация JavaScript
----------------------------
JSON является синтаксисом для сериализации объектов, массивов, чисел, строк логических значений и значения null. Он основывается на синтаксисе JavaScript, однако всё же отличается от него: не каждый код на JavaScript является JSON, и не каждый JSON является кодом на JavaScript.

Различия между JavaScript и JSON
--------------------------------

Объекты и массивы   
------------------
Имена свойств должны быть строками, заключёнными в двойные кавычки; конечные запятые запрещены.

Числа
------
Ведущие нули запрещены; перед десятичной запятой обязательно должна быть хотя бы одна цифра.
Строки
-------  
Только ограниченный набор символов может быть заэкранирован; некоторые управляющие символы запрещены; разрешены юникодные символы разделительной линии (U+2028) и разделительного параграфа (U+2029); строки должны быть заключены в двойные кавычки. 
```
var code = '"\u2028\u2029"';
JSON.parse(code); // работает
```
Формат JSON
============
Данные в формате JSON (RFC 4627 http://tools.ietf.org/html/rfc4627) представляют собой:

1. JavaScript-объекты { ... } или
2. Массивы [ ... ] или
3. Значения одного из типов:
- строки в двойных кавычках,
- число,
- логическое значение true/false,
- null.
Почти все языки программирования имеют библиотеки для преобразования объектов в формат JSON.

Объекты и массивы   
------------------
```
var products = {
        'Suit': [
            'Suit',
            'The mug you\'ve been dreaming about. One sip from this ceramic 16oz fluid delivery system and you\'ll never go back to red cups.',
            14,
            '/images/1.jpg',
            1
        ],
        'Bow tie': [
            'Bow tie',
            'These coasters roll all of the greatest qualities into one: class, leather, and octocats. They also happen to protect surfaces from cold drinks.',
            18,
            '/images/2.jpg',
            2
        ],
        'Sweater': [
            'Sweater',
            'Set of two heavyweight 16 oz. Octopint glasses for your favorite malty beverage.',
            16,
            '/images/3.jpg',
            3
        ],
        'Hat': [
            'Hat',
            'Check it. Blacktocat is back with a whole new direction. He\'s exited stealth mode and is ready for primetime, now with a stylish logo.',
            25,
            '/images/4.jpg',
            4
        ],
        'Shoes': [
            'Shoes',
            'Need a huge Octocat sticker for your laptop, fridge, snowboard, or ceiling fan? Look no further!',
            2,
            '/images/5.jpg',
            5
        ],
        'Glasses': [
            'Glasses',
            'Pixels are your friends. Show your bits in this super-comfy blue American Apparel tri-blend shirt with a pixelated version of your favorite aquatic feline',
            25,
            '/images/6.jpg',
            6
        ],
        'Suit 1': [
            'Suit',
            'The mug you\'ve been dreaming about. One sip from this ceramic 16oz fluid delivery system and you\'ll never go back to red cups.',
            14,
            '/images/1.jpg',
            7
        ],
        'Bow tie 1': [
            'Bow tie',
            'These coasters roll all of the greatest qualities into one: class, leather, and octocats. They also happen to protect surfaces from cold drinks.',
            18,
            '/images/2.jpg',
            8
        ],
        'Sweater 1': [
            'Sweater',
            'Set of two heavyweight 16 oz. Octopint glasses for your favorite malty beverage.',
            16,
            '/images/3.jpg',
            9
        ],
        'Hat 1': [
            'Hat',
            'Check it. Blacktocat is back with a whole new direction. He\'s exited stealth mode and is ready for primetime, now with a stylish logo.',
            25,
            '/images/4.jpg',
            10
        ],
        'Shoes 1': [
            'Shoes',
            'Need a huge Octocat sticker for your laptop, fridge, snowboard, or ceiling fan? Look no further!',
            2,
            '/images/5.jpg',
            11
        ],
        'Glasses 1': [
            'Glasses',
            'Pixels are your friends. Show your bits in this super-comfy blue American Apparel tri-blend shirt with a pixelated version of your favorite aquatic feline',
            25,
            '/images/6.jpg',
            12
        ]
    };

```

Основные методы для работы с JSON в JavaScript
-----------------------------------------------
1. JSON.parse – читает объекты из строки в формате JSON.
2. JSON.stringify – превращает объекты в строку в формате JSON, используется, когда нужно из JavaScript передать данные по сети.

Метод JSON.parse
----------------
Вызов JSON.parse(str) превратит строку с данными в формате JSON в JavaScript-объект/массив/значение.

```
var numbers = "[0, 1, 2, 3]";

numbers = JSON.parse(numbers);

alert( numbers[1] ); // 1
```

Данные могут быть сколь угодно сложными, объекты и массивы могут включать в себя другие объекты и массивы. Главное чтобы они соответствовали формату.

JSON-объекты ≠ JavaScript-объекты
----------------------------------
```
{
  name: "Вася",       // ошибка: ключ name без кавычек!
  "surname": 'Петров',// ошибка: одинарные кавычки у значения 'Петров'!
  "age": 35,           // .. а тут всё в порядке.
  "isAdmin": false    // и тут тоже всё ок
}
```
Кроме того, в формате JSON не поддерживаются комментарии. Он предназначен только для передачи данных.

JSON.parse()
=============

Метод JSON.parse() разбирает строку JSON, возможно с преобразованием получаемого в процессе разбора значения.

Пример: использование метода JSON.parse()
-----------------------------------------
```
JSON.parse('{}');              // {}
JSON.parse('true');            // true
JSON.parse('"foo"');           // "foo"
JSON.parse('[1, 5, "false"]'); // [1, 5, "false"]
JSON.parse('null');            // null

```
1 Метод JSON.parse
-------------------
```
var prodstr = '{"Suit":["Suit","The mug you\'ve been dreaming about. One sip from this ceramic 16oz fluid delivery system and you\'ll never go back to red cups.",14,"../images/1.jpg",1],"Bow tie":["Bow tie","These coasters roll all of the greatest qualities into one: class, leather, and octocats. They also happen to protect surfaces from cold drinks.",18,"../images/2.jpg",2],"Sweater":["Sweater","Set of two heavyweight 16 oz. Octopint glasses for your favorite malty beverage.",16,"../images/3.jpg",3],"Hat":["Hat","Check it. Blacktocat is back with a whole new direction. He\'s exited stealth mode and is ready for primetime, now with a stylish logo.",25,"../images/4.jpg",4],"Shoes":["Shoes","Need a huge Octocat sticker for your laptop, fridge, snowboard, or ceiling fan? Look no further!",2,"../images/5.jpg",5],"Glasses":["Glasses","Pixels are your friends. Show your bits in this super-comfy blue American Apparel tri-blend shirt with a pixelated version of your favorite aquatic feline",25,"../images/6.jpg",6]}';
products = JSON.parse(prodstr);

console.log( products['Bow tie'][1] ); 

```

1 Happy Shopping
----------------
...

   for (var item in products) {
        var itemName = products[item][0], 
            itemDescription = products[item][1], 
            itemPrice = products[item][2], 
            itemImg = products[item][3], 
            itemId = products[item][4], 
        
            $template = $($('#productTemplate').html());
        
        $template.find('h1').text(itemName);
        $template.find('p').text(itemDescription);
        $template.find('.price').text('$' + itemPrice);
        $template.css('background-image', 'url(' + itemImg + ')');
        
        $template.data('id', itemId);
        $template.data('name', itemName);
        $template.data('price', itemPrice);
        $template.data('image', itemImg);
        
        $shop.append($template);
    }


```

2 init(products)
----------------
```
$('#prod1').on('click',function(){
    
    var products = {
        'Suit': [
            'Suit',
            'The mug you\'ve been dreaming about. One sip from this ceramic 16oz fluid delivery system and you\'ll never go back to red cups.',
            14,
            '../images/1.jpg',
            1
        ],
        'Bow tie': [
            'Bow tie',
            'These coasters roll all of the greatest qualities into one: class, leather, and octocats. They also happen to protect surfaces from cold drinks.',
            18,
            '../images/2.jpg',
            2
        ],
        'Sweater': [
            'Sweater',
            'Set of two heavyweight 16 oz. Octopint glasses for your favorite malty beverage.',
            16,
            '../images/3.jpg',
            3
        ],
        'Hat': [
            'Hat',
            'Check it. Blacktocat is back with a whole new direction. He\'s exited stealth mode and is ready for primetime, now with a stylish logo.',
            25,
            '../images/4.jpg',
            4
        ],
        'Shoes': [
            'Shoes',
            'Need a huge Octocat sticker for your laptop, fridge, snowboard, or ceiling fan? Look no further!',
            2,
            '../images/5.jpg',
            5
        ],
        'Glasses': [
            'Glasses',
            'Pixels are your friends. Show your bits in this super-comfy blue American Apparel tri-blend shirt with a pixelated version of your favorite aquatic feline',
            25,
            '../images/6.jpg',
            6
        ]
    };
    init(products);
  }); 
 function init(products){
    for (var item in products) {
    
        var itemName = products[item][0], itemDescription = products[item][1], itemPrice = products[item][2], itemImg = products[item][3], itemId = products[item][4], $template = $($('#productTemplate').html());
        $template.find('h1').text(itemName);
        $template.find('p').text(itemDescription);
        $template.find('.price').text('$' + itemPrice);
        $template.css('background-image', 'url(' + itemImg + ')');
        $template.data('id', itemId);
        $template.data('name', itemName);
        $template.data('price', itemPrice);
        $template.data('image', itemImg);
        $shop.append($template);
    }
  }

```

3 $shop.empty()
----------------
```
$('#prod2').on('click',function(){
    $shop.empty();
    var products = {
```
4 #prod0
---------
```
$('#prod0').on('click',function(){
    $shop.empty();

    init(products);
  });
```

5 banner
---------
```
.banner {
  font-family: Raleway;
  font-size: 1.5vw;
  text-align: center;
  display: block;
  width: 10vw;
  margin: 0 auto;
  padding: 0.9vw 1vw 0.8vw;
  background: tomato;
  color: white;
  text-shadow: 0 2px rgba(0, 0, 0, 0.3);
  position: relative;
}


<script id='productTemplate' type='text/template'>
  <div class="product">
  <h2></h2>
  <h1></h1>
  <p></p>
  <div class="button">
  <div class="price"></div>
  <a class="addtocart">
  <div class="add">Add to Cart</div>
  <div class="added">Added!</div>
  </a>
  </div>
  </div>
</script>

var products = {
        'Bike': [
            'Bike',
            'The mug you\'ve been dreaming about. One sip from this ceramic 16oz fluid delivery system and you\'ll never go back to red cups.',
            14,
            '../images/7.jpg',
            1,
            true
        ],
function init(products){
    for (var item in products) {
    
        var itemName = products[item][0], 
            itemDescription = products[item][1], 
            itemPrice = products[item][2], 
            itemImg = products[item][3], 
            itemId = products[item][4], 
            itemDc = products[item][5], 
        $template = $($('#productTemplate').html());
        if(itemDc){
            $template.find('h2').text('BEST PRICE');
            $template.find('h2').addClass('banner');

        }
        
        // itemPriceDc = (itemDc)?itemPrice*0.7:itemPrice;
        itemPriceDc = (itemDc)?(itemPrice*0.7).toFixed(2):itemPrice;
        $template.find('h1').text(itemName);
        $template.find('p').text(itemDescription);
        $template.find('.price').text('$' + itemPriceDc);
        (itemDc)?$template.find('.discont').text('$' + itemPrice):'';
        $template.css('background-image', 'url(' + itemImg + ')');
        $template.data('id', itemId);
        $template.data('name', itemName);
        $template.data('price', itemPrice);
        $template.data('discont', itemDc);
        $template.data('image', itemImg);
        $shop.append($template);
    }
  }
```

JSON.parse(str, reviver)
-------------------------
Метод JSON.parse поддерживает и более сложные алгоритмы разбора.

Например, мы получили с сервера объект с данными события event.
дата события
------------
```
var prodstr =  {"Bike": [
            "Bike",
            "The mug you\'ve been dreaming about. One sip from this ceramic 16oz fluid delivery system and you\'ll never go back to red cups.",
            14,
            "../images/7.jpg",
            1,
            true,
            "2016-02-30T12:00:00.000Z"
        ],
    }
```

Попробуем вызвать для этого JSON.parse:
```
products = JSON.parse(prodstr);

console.log( products['Bike'][6] ); // 2016-02-30T12:00:00.000Z
console.log( products['Bike'][6].getDate() ) ); // ошибка! 
```
Для восстановления из строки у JSON.parse(str, reviver) есть второй параметр reviver, который является функцией function(key, value).

Если она указана, то в процессе чтения объекта из строки JSON.parse передаёт ей по очереди все создаваемые пары ключ-значение и может возвратить либо преобразованное значение, либо undefined, если его нужно пропустить.
2.html
------
```
var prodstr = '{"Suit":["Suit","The mug you\'ve been dreaming about. One sip from this ceramic 16oz fluid delivery system and you\'ll never go back to red cups.",14,"../images/1.jpg",1],"Bow tie":["Bow tie","These coasters roll all of the greatest qualities into one: class, leather, and octocats. They also happen to protect surfaces from cold drinks.",18,"../images/2.jpg",2],"Sweater":["Sweater","Set of two heavyweight 16 oz. Octopint glasses for your favorite malty beverage.",16,"../images/3.jpg",3],"Hat":["Hat","Check it. Blacktocat is back with a whole new direction. He\'s exited stealth mode and is ready for primetime, now with a stylish logo.",25,"../images/4.jpg",4],"Shoes":["Shoes","Need a huge Octocat sticker for your laptop, fridge, snowboard, or ceiling fan? Look no further!",2,"../images/5.jpg",5],"Glasses":["Glasses","Pixels are your friends. Show your bits in this super-comfy blue American Apparel tri-blend shirt with a pixelated version of your favorite aquatic feline",25,"../images/6.jpg",6,true,"2016 03 30"]}';
var products = JSON.parse(prodstr);

console.log( products['Glasses'][6] ); // 2016 03 30

var products = JSON.parse(prodstr, function(key, value) {
  if (key == 6) return new Date(value);
  return value;
});

console.log( products['Glasses'][6]); //Wed Mar 30 2016 00:00:00 GMT+0300 (EEST)

/**/
products['Glasses'][6] = new Date(products['Glasses'][6]); //Wed Mar 30 2016 00:00:00 GMT+0300 (EEST)

console.log( products['Glasses'][6]);
console.log( products['Glasses'][6].getDate() ); // 30!

```

6.html
-------

```
$(document).ready(function () {
    var $shop = $('.shop');
    var $cart = $('.cart-items');

    var product0 = '{"Bike":["Bike","The mug you\'ve been dreaming about. One sip from this ceramic 16oz fluid delivery system and you\'ll never go back to red cups.",14,"../images/7.jpg",1,true,"2016 03 30"],"Bow tie":["Bow tie","These coasters roll all of the greatest qualities into one: class, leather, and octocats. They also happen to protect surfaces from cold drinks.",18,"../images/2.jpg",2,false,""],"Bike Blue":["Bike Blue","Set of two heavyweight 16 oz. Octopint glasses for your favorite malty beverage.",16,"../images/9.jpg",3,false,""],"Hat":["Hat","Check it. Blacktocat is back with a whole new direction. He\'s exited stealth mode and is ready for primetime, now with a stylish logo.",25,"../images/4.jpg",4,true,"2016 03 30"],"Bike Pink":["Bike Pink","Need a huge Octocat sticker for your laptop, fridge, snowboard, or ceiling fan? Look no further!",2,"../images/11.jpg",5,true,"2016 03 30"],"Glasses":["Glasses","Pixels are your friends. Show your bits in this super-comfy blue American Apparel tri-blend shirt with a pixelated version of your favorite aquatic feline",25,"../images/6.jpg",6,true,"2016 03 30"]}';
    
    var product1 = '{"Suit":["Suit","The mug you\'ve been dreaming about. One sip from this ceramic 16oz fluid delivery system and you\'ll never go back to red cups.",14,"../images/1.jpg",1,false,""],"Bow tie":["Bow tie","These coasters roll all of the greatest qualities into one: class, leather, and octocats. They also happen to protect surfaces from cold drinks.",18,"../images/2.jpg",2,false,""],"Sweater":["Sweater","Set of two heavyweight 16 oz. Octopint glasses for your favorite malty beverage.",16,"../images/3.jpg",3,false,""],"Hat":["Hat","Check it. Blacktocat is back with a whole new direction. He\'s exited stealth mode and is ready for primetime, now with a stylish logo.",25,"../images/4.jpg",4,true,"2016 03 30"],"Shoes":["Shoes","Need a huge Octocat sticker for your laptop, fridge, snowboard, or ceiling fan? Look no further!",2,"../images/5.jpg",5,false,""],"Glasses":["Glasses","Pixels are your friends. Show your bits in this super-comfy blue American Apparel tri-blend shirt with a pixelated version of your favorite aquatic feline",25,"../images/6.jpg",6,true,"2016 03 30"]}';
    
    var product2 = '{"Bike":["Bike","The mug you\'ve been dreaming about. One sip from this ceramic 16oz fluid delivery system and you\'ll never go back to red cups.",14,"../images/7.jpg",1,true,"2016 03 30"],"Best Bike":["Best Bike","These coasters roll all of the greatest qualities into one: class, leather, and octocats. They also happen to protect surfaces from cold drinks.",18,"../images/8.jpg",2,false,""],"Bike Blue":["Bike Blue","Set of two heavyweight 16 oz. Octopint glasses for your favorite malty beverage.",16,"../images/9.jpg",3,false,""],"Big Bike Blue":["Bike Blue","Check it. Blacktocat is back with a whole new direction. He\'s exited stealth mode and is ready for primetime, now with a stylish logo.",25,"../images/10.jpg",4,false,""],"Bike Pink":["Bike Pink","Need a huge Octocat sticker for your laptop, fridge, snowboard, or ceiling fan? Look no further!",2,"../images/11.jpg",5,true,"2016 03 30"],"Best Pink Bike":["Best Pink Bike","Pixels are your friends. Show your bits in this super-comfy blue American Apparel tri-blend shirt with a pixelated version of your favorite aquatic feline",25,"../images/12.jpg",6,false,""]}';
    
  init(JSON.parse(product0));
    
  $('#prod0').on('click',function(){
      $shop.empty();
      init(JSON.parse(product0));
  });
  
  $('#prod1').on('click',function(){
    $shop.empty();
    init(JSON.parse(product1));
  });
  
  $('#prod2').on('click',function(){
    $shop.empty();
    init(JSON.parse(product2));
  });
  
  function init(products){
    for (var item in products) {
    
        var itemName = products[item][0], 
            itemDescription = products[item][1], 
            itemPrice = products[item][2], 
            itemImg = products[item][3], 
            itemId = products[item][4], 
            itemDc = products[item][5], 
        $template = $($('#productTemplate').html());
        if(itemDc){
            $template.find('h2').text('BEST PRICE');
            $template.find('h2').addClass('banner');

        }
        
        itemPriceDc = (itemDc)?(itemPrice*0.7).toFixed(2):itemPrice;
        $template.find('h1').text(itemName);
        $template.find('p').text(itemDescription);
        $template.find('.price').text('$' + itemPriceDc);
        (itemDc)?$template.find('.discont').text('$' + itemPrice):'';
        $template.css('background-image', 'url(' + itemImg + ')');
        $template.data('id', itemId);
        $template.data('name', itemName);
        $template.data('price', itemPrice);
        $template.data('discont', itemDc);
        $template.data('image', itemImg);
        $shop.append($template);
    }
  }
});

```
Основы XMLHttpRequest
=====================
Объект XMLHttpRequest (XHR) дает возможность из JavaScript делать HTTP-запросы к серверу без перезагрузки страницы.

Несмотря на слово XML в названии, XMLHttpRequest может работать с любыми данными, а не только с XML.

Как правило, XMLHttpRequest используют для загрузки данных.

routes
======
index.js
--------
```
var express = require('express');
var router = express.Router();

/* GET home page. */
router.get('/', function(req, res, next) {
  res.render('index', { title: 'Express' });
});
router.get('/test1', function(req, res, next) {
  res.render('test1', { title: 'Express Ajax' });
});

module.exports = router;

```

пример использования, который загружает файл test.txt из текущей директории и выдаёт его содержимое:

test1.jade
-----------
```
extends layout

block content
  h1 Test Ajax 1
  button(onclick='loadTest()') Загрузить test.txt!
    script.
      function loadTest() {
      var xhr = new XMLHttpRequest();
      xhr.open('GET', '/ajax/test.txt', false);
      xhr.send();
      if (xhr.status != 200) {
      // обработать ошибку
      alert('Ошибка ' + xhr.status + ': ' + xhr.statusText);
      } else {
      // вывести результат
      alert(xhr.responseText);
      }
      }

```

метод open
----------
Синтаксис:
```
xhr.open(method, URL, async, user, password)
```
Этот метод — вызывается первым после создания объекта XMLHttpRequest.

Задаёт основные параметры запроса:
----------------------------------
- method — HTTP-метод. Как правило, используется GET либо POST, хотя доступны и более экзотические, вроде TRACE/DELETE/PUT и т.п.
- URL — адрес запроса. Можно использовать не только http/https, но и другие протоколы, например ftp:// и file://.
При этом есть ограничения безопасности, называемые «Same Origin Policy»: запрос со страницы можно отправлять только на тот же протокол://домен:порт, с которого она пришла. 

- async — если установлено в false, то запрос производится синхронно, если true — асинхронно.
«Синхронный запрос» означает, что после вызова xhr.send() и до ответа сервера главный поток будет «заморожен»: посетитель не сможет взаимодействовать со страницей — прокручивать, нажимать на кнопки и т.п. После получения ответа выполнение продолжится со следующей строки.

«Асинхронный запрос» означает, что браузер отправит запрос, а далее результат нужно будет получить через обработчики событий, которые мы рассмотрим далее.

- user, password — логин и пароль для HTTP-авторизации, если нужны.

Вызов open не открывает соединение
-----------------------------------
Он лишь настраивает запрос, а коммуникация инициируется методом send.

Отослать данные: send
---------------------
Синтаксис:
```
xhr.send([body])
```
Именно этод метод открывает соединение и отправляет запрос на сервер.

В body находится тело запроса. Не у всякого запроса есть тело, например у GET-запросов тела нет, а у POST — основные данные как раз передаются через body.

Отмена: abort
--------------
Вызов xhr.abort() прерывает выполнение запроса.

Ответ: status, statusText, responseText
-----------------------------------------
Основные свойства, содержащие ответ сервера:

- status
HTTP-код ответа: 200, 404, 403 и так далее. Может быть также равен 0, если сервер не ответил или при запросе на другой домен.
- statusText
Текстовое описание статуса от сервера: OK Not Found, Forbidden и так далее.
- responseText
Текст ответа сервера.
- responseXML
Если сервер вернул XML, снабдив его правильным заголовком Content-type: text/xml, то браузер создаст из него XML-документ. По нему можно будет делать запросы xhr.responseXml.querySelector("...") и другие.
Оно используется редко, так как обычно используют не XML, а JSON. То есть, сервер возвращает JSON в виде текста, который браузер превращает в объект вызовом JSON.parse(xhr.responseText).

Синхронные и асинхронные запросы
---------------------------------
Если в методе open установить параметр async равным false или просто забыть его указать, то запрос будет синхронным.

Синхронные вызовы используются чрезвычайно редко, так как блокируют взаимодействие со страницей до окончания загрузки. Посетитель не может даже прокручивать её. Никакой JavaScript не может быть выполнен, пока синхронный вызов не завершён — в общем, в точности те же ограничения как alert.
```
// Синхронный запрос
xhr.open('GET', 'test.txt', false);

// Отсылаем его
xhr.send();
// ...весь JavaScript "подвиснет", пока запрос не завершится
```
Если синхронный вызов занял слишком много времени, то браузер предложит закрыть «зависшую» страницу.

Из-за такой блокировки получается, что нельзя отослать два запроса одновременно. Кроме того ряд продвинутых возможностей, таких как возможность делать запросы на другой домен и указывать таймаут, в синхронном режиме не работают.

Для того, чтобы запрос стал асинхронным, укажем параметр async равным true.

test1.jade:

```
h2 Test Ajax 2
  button#button(onclick='loadAsyncTest()') Загрузить testa.txt!
    script.
      function loadAsyncTest() {
      var xhr = new XMLHttpRequest();
      xhr.open('GET', '/ajax/testa.txt', true);
      xhr.send(); // (1)
      xhr.onreadystatechange = function() { // (3)
      if (xhr.readyState != 4) return;
      button.innerHTML = 'Готово!';
      if (xhr.status != 200) {
      // обработать ошибку
      alert('Ошибка ' + xhr.status + ': ' + xhr.statusText);
      } else {
      // вывести результат
      alert(xhr.responseText);
      }
      }
      button.innerHTML = 'Загружаю...'; //2
      button.disabled = true;
      }

```

Если в open указан третий аргумент true, то запрос выполняется асинхронно. Это означает, что после вызова xhr.send() код не «зависает», а преспокойно продолжает выполняться.

Событие readystatechange
------------------------
Событие readystatechange происходит несколько раз в процессе отсылки и получения ответа. При этом можно посмотреть «текущее состояние запроса» в свойстве xhr.readyState.

## Все состояния, по спецификации:
```
const unsigned short UNSENT = 0; // начальное состояние
const unsigned short OPENED = 1; // вызван open
const unsigned short HEADERS_RECEIVED = 2; // получены заголовки
const unsigned short LOADING = 3; // загружается тело (получен очередной пакет данных)
const unsigned short DONE = 4; // запрос завершён
```
json
-----
test1.jade
```
h2 Test Ajax 3
  button#button(onclick='loadPhones()') Загрузить phones.json!
    script.
      function loadPhones() {
      // 1. Создаём новый объект XMLHttpRequest
      var xhr = new XMLHttpRequest();
      // 2. Конфигурируем его: GET-запрос на URL 'phones.json'
      xhr.open('GET', '/ajax/phones.json', true);
      // 3. Отсылаем запрос
      xhr.send();
      xhr.onreadystatechange = function() {
      if (xhr.readyState != 4) return;
      button.innerHTML = 'Готово!';
      // 4. Если код ответа сервера не 200, то это ошибка
      if (xhr.status != 200) {
      // обработать ошибку
      alert(xhr.status + ': ' + xhr.statusText);
      } else {
      // вывести результат
      alert(xhr.responseText);
      }
      }
      button.innerHTML = 'Загружаю...';
      button.disabled = true;
      }

```


table.jade
----------
```
extends blog

block content
  h1 Table
    script.
      var USER_FILE;
      var VanillaRunOnDomReady = function() {
      var _table_ = document.createElement('table'),
      _tr_ = document.createElement('tr'),
      _th_ = document.createElement('th'),
      _td_ = document.createElement('td');
      function buildHtmlTable(arr) {
      var table = _table_.cloneNode(false),
      columns = addAllColumnHeaders(arr, table);
      for (var i=0, maxi=arr.length; i < maxi; ++i) {
      var tr = _tr_.cloneNode(false);
      for (var j=0, maxj=columns.length; j < maxj ; ++j) {
      var td = _td_.cloneNode(false);
      cellValue = arr[i][columns[j]];
      td.appendChild(document.createTextNode(arr[i][columns[j]] || ''));
      tr.appendChild(td);
      }
      table.appendChild(tr);
      }
      return table;
      }
      function addAllColumnHeaders(arr, table)
      {
      var columnSet = [],
      tr = _tr_.cloneNode(false);
      for (var i=0, l=arr.length; i < l; i++) {
      for (var key in arr[i]) {
      if (arr[i].hasOwnProperty(key) && columnSet.indexOf(key)===-1) {
      columnSet.push(key);
      var th = _th_.cloneNode(false);
      th.appendChild(document.createTextNode(key));
      tr.appendChild(th);
      }
      }
      }
      table.appendChild(tr);
      return columnSet;
      }
      var persone  =  JSON.parse(USER_FILE);
      document.body.appendChild(buildHtmlTable(persone));
      }
      function loadPhones() {
      // 1. Создаём новый объект XMLHttpRequest
      var xhr = new XMLHttpRequest();
      // 2. Конфигурируем его: GET-запрос на URL 'phones.json'
      xhr.open('GET', '/ajax/phones.json', true);
      // 3. Отсылаем запрос
      xhr.send();
      xhr.onreadystatechange = function() {
      if (xhr.readyState != 4) return;
      button.innerHTML = 'Готово!';
      // 4. Если код ответа сервера не 200, то это ошибка
      // по окончании запроса доступны:
      // status, statusText
      // responseText, responseXML (при content-type: text/xml)
      if (xhr.status != 200) {
      // обработать ошибку
      alert( 'ошибка: ' + this.status + 'запрос не удался');
      return;
      } else {
      // получить результат из this.responseText или this.responseXML
      // вывести результат
      //alert(xhr.responseText);
      USER_FILE = xhr.responseText;
      alreadyrunflag = 1;
      VanillaRunOnDomReady();
      }
      }
      button.innerHTML = 'Загружаю...';
      button.disabled = true;
      }
    button#button(onclick='loadPhones()') Загрузить phones.json!

```

comment.jade
-------------
```
extends blog

block content
  h1 Comments
    script(language='JavaScript').
      function XmlHttp()
      {
      var xmlhttp;
      try{xmlhttp = new ActiveXObject("Msxml2.XMLHTTP");}
      catch(e)
      {
      try {xmlhttp = new ActiveXObject("Microsoft.XMLHTTP");}
      catch (E) {xmlhttp = false;}
      }
      if (!xmlhttp && typeof XMLHttpRequest!='undefined')
      {
      xmlhttp = new XMLHttpRequest();
      }
      return xmlhttp;
      }
      function ajax(param)
      {
      if (window.XMLHttpRequest) req = new XmlHttp();
      method=(!param.method ? "POST" : param.method.toUpperCase());
      if(method=="GET")
      {
      send=null;
      param.url=param.url+"&ajax=true";
      }
      else
      {
      send="";
      for (var i in param.data) send+= i+"="+param.data[i]+"&";
      // send=send+"ajax=true"; // если хотите передать сообщение об успехе
      }
      req.open(method, param.url, true);
      if(param.statbox)document.getElementById(param.statbox).innerHTML = '<img src="/images/wait.gif">';
      req.setRequestHeader("Content-Type", "application/x-www-form-urlencoded");
      req.send(send);
      req.onreadystatechange = function()
      {
      if (req.readyState == 4 && req.status == 200) //если ответ положительный
      {
      if(param.success)param.success(req.responseText);
      }
      }
      }
    #content
      #status(style='width:470px;background:#fff;padding:20px 10px 20px 10px;border:solid 5px #D1D1D1;font: 13 Arial;')
        | Ни одного комментария пока нет.
      br
      form(action='/')
        p
          b Оставьте ваш комментарий
        p
          textarea#area_1(name='area_1', style='height:50px; width:500px;padding:10px;font: 13 Arial;') Введите имя
        p
          textarea#area_2(name='area_1', style='height:100px; width:500px;padding:10px;font: 13 Arial;') Текст сообщения
        input(type='button', value='Сохранить комментарий', onclick='\
        ajax({\
        url:"/",\
        statbox:"status",\
        method:"POST",\
        data:\
        {                                                            first_area:document.getElementById("area_1").value,\
        second_area:document.getElementById("area_2").value\
        },\
        success:function(data){document.getElementById("status").innerHTML=data;}\
        })')
```

index.js
---------
```
var express = require('express');
var router = express.Router();

/* GET home page. */
router.get('/', function(req, res, next) {
  res.render('index', { title: 'Express' });
});
router.get('/shop1', function(req, res, next) {
  res.render('index1', { title: 'Shopping' });
});
router.get('/test1', function(req, res, next) {
  res.render('test1', { title: 'Express Ajax' });
});
router.get('/ajax', function(req, res, next) {
  res.render('ajax', { title: 'Express Ajax Blog' });
});

router.get('/comment', function(req, res, next) {
  res.render('comment', { title: 'Express Ajax Blog' });
});

router.get('/getpost', function(req, res, next) {
  res.render('getpost', { title: 'Express Ajax Blog' });
});


router.get('/table', function(req, res, next) {
  res.render('table', { title: 'Express Ajax Blog' });
});

// routes will go here
router.get('/api/test', function(req, res) {
  var token = req.param('text');

  res.send(token);
});

module.exports = router;

```


index1.jade
-----------
```
extends layout

block content
  script(src='/javascripts/cartj.js')
```

cartj.js
--------
```
$(document).ready(function () {
    var $shop = $('.shop');
    var $cart = $('.cart-items');

    var xmlhttp = new XMLHttpRequest();

    var url = "/ajax/data.json";
    getDate(url);

  
  function getDate(url){
    $shop.empty();
      xmlhttp.onreadystatechange = function() {
        if (xmlhttp.readyState == 4 && xmlhttp.status == 200) {
            var product = xmlhttp.responseText;
 
            init(JSON.parse(product));  
          }
      };
    xmlhttp.open("GET", url, true);
    xmlhttp.send();
  }
  
  function init(products){
    for (var item in products) {
    
        var itemName = products[item][0], 
            itemDescription = products[item][1], 
            itemPrice = products[item][2], 
            itemImg = products[item][3], 
            itemId = products[item][4], 
            
        $template = $($('#productTemplate').html());
        
        
        
        $template.find('h1').text(itemName);
        $template.find('p').text(itemDescription);
        $template.find('.price').text('$' + itemPrice);
        
        $template.css('background-image', 'url(' + itemImg + ')');
        $template.data('id', itemId);
        $template.data('name', itemName);
        $template.data('price', itemPrice);
        
        $template.data('image', itemImg);
        $shop.append($template);
    }
  }
});

```