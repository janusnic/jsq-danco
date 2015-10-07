# jsq-danco

package.json
```
{
  "name" : "blog",
  "version" : "0.0.1",
  "description" : "My minimalistic blog",
  "dependencies" : {
    "mime" : "~1.2.7"
  }
}
```
server.js
```
var http = require('http');

var fs = require('fs');
var url = require('url');

var path = require("path");
var mime = require("mime");

function start() {

function send404(response) {
  response.writeHead(404, {"Content-type" : "text/plain"});
  response.write("Error 404: resource not found");
  response.end();
}

function sendPage(response, filePath, fileContents) {
  // response.writeHead(200, {"Content-type" : "text/plain"});
  response.writeHead(200, {"Content-type" : mime.lookup(path.basename(filePath))});
  response.end(fileContents);
}

function serverWorking(response, absPath) {
  fs.exists(absPath, function(exists) {
    if (exists) {
      fs.readFile(absPath, function(err, data) {
        if (err) {
          send404(response)
        } else {
          sendPage(response, absPath, data);
        }
      });
    } else {
      send404(response);
    }
  });
}

var server = http.createServer(function(request, response) {
  var filePath = false;

  if (request.url == '/') {
    filePath = "www/index.html";
  } else {
    filePath = "www" + request.url;
  }

  var absPath = "./" + filePath;
  serverWorking(response, absPath);
});


function onRequest(request, response) {
    console.log("Request received from maim app."); //наш callback
    
    // Parse the request containing file name
    var pathname = url.parse(request.url).pathname;
   
    // Print the name of the file for which request is made.
    console.log("Request for " + pathname + " received.");

      var filePath = false;

      if (request.url == '/') {
        filePath = "www/index.html";
      } else {
        filePath = "www" + request.url;
      }

      var absPath = "./" + filePath;
      serverWorking(response, absPath);

  }

  http.createServer(onRequest).listen(8888);
  
  // Console will print the message
  console.log('Server running at http://127.0.0.1:8888/');

}

exports.start = start;

```
app.js
```
var server = require("./server");

server.start();
```
## app02
How to GET and POST in node.js
```
    <div id="content">
           
    <h2>How to GET and POST in node.js</h2>

    <form method="post" action="/">
        <textarea name="text" id="textbox">Enter text here that will be sent to the server using the POST method.</textarea>
        <br />
        <input type="submit" id="submit" name="submit" value="SUBMIT" />
    </form>
            
    </div>
```
server.js
```
var http = require('http');

var fs = require('fs');
var url = require('url');

var path = require("path");
var mime = require("mime");

var qs = require('qs'); // querystring parser

function start() {

function send404(response) {
  response.writeHead(404, {"Content-type" : "text/plain"});
  response.write("Error 404: resource not found");
  response.end();
}

function sendPage(response, filePath, fileContents) {
  // response.writeHead(200, {"Content-type" : "text/plain"});
  response.writeHead(200, {"Content-type" : mime.lookup(path.basename(filePath))});
  response.end(fileContents);
}

function serverWorking(response, absPath) {

  fs.exists(absPath, function(exists) {
    if (exists) {
      fs.readFile(absPath, function(err, data) {
        if (err) {
          send404(response)
        } else {
          sendPage(response, absPath, data);
        }
      });
    } else {
      send404(response);
    }
  });
}

var server = http.createServer(function(request, response) {


  var filePath = false;

  if (request.url == '/') {
    filePath = "www/index.html";
  } else {
    filePath = "www" + request.url;
  }

  var absPath = "./" + filePath;
  serverWorking(response, absPath);
});


function onRequest(request, response) {

   console.log("Request received from maim app."); //наш callback
    
    // Parse the request containing file name
    var pathname = url.parse(request.url).pathname;
   
    // Print the name of the file for which request is made.
    console.log("Request for " + pathname + " received.");

  // store the contents of 'index.html' to a buffer
  var html = fs.readFileSync('www/index.html');

    // handle the routes
  if (request.method == 'POST') {

    // pipe the request data to the console
    request.pipe(process.stdout);

    // pipe the request data to the response to view on the web
    response.writeHead(200, {'Content-Type': 'text/plain'});
    request.pipe(response);

  } else {
    
    // for GET requests, serve up the contents in 'index.html'
    
      var filePath = false;

      if (request.url == '/') {
        filePath = "www/index.html";
      } else {
        filePath = "www" + request.url;
      }

      var absPath = "./" + filePath;
      serverWorking(response, absPath);
    }

  }

  http.createServer(onRequest).listen(8888);
  
  // Console will print the message
  console.log('Server running at http://127.0.0.1:8888/');

}

exports.start = start;

```
## app03

## Событие readystatechange

Событие readystatechange происходит несколько раз в процессе отсылки и получения ответа. При этом можно посмотреть «текущее состояние запроса» в свойстве xhr.readyState.

## Все состояния, по спецификации:
```
const unsigned short UNSENT = 0; // начальное состояние
const unsigned short OPENED = 1; // вызван open
const unsigned short HEADERS_RECEIVED = 2; // получены заголовки
const unsigned short LOADING = 3; // загружается тело (получен очередной пакет данных)
const unsigned short DONE = 4; // запрос завершён

```
## POST
```
function startAjax(url){
  var request; 
  if(window.XMLHttpRequest){ 
      request = new XMLHttpRequest(); 
  } else if(window.ActiveXObject){ 
      request = new ActiveXObject("Microsoft.XMLHTTP");  
  } else { 
      return; 
  } 
  
  request.onreadystatechange = function(){
    switch (request.readyState) {
      case 1: print_console("<br/><em>1: вызван open...</em>"); break
      case 2: print_console("<br/><em>2: получены заголовки...</em>"); break
      case 3: print_console("<br/><em>3: загружается тело..</em>"); break
      case 4:{
       if(request.status==200){   
            print_console("<br/><em>4: запрос завершён</em>"); 
            document.getElementById("printResult").innerHTML = "<b>"+request.responseText+"</b>"; 
           }else if(request.status==404){
            alert("HTTP Status: 404 : NOT FOUND!");
           }
            else alert("текущее состояние запроса: "+ request.status);
       
      break
      }
    }   
    } 
  //request.open("GET",url+"?a1=1&a2=2",true);
  request.open("POST",url,true);
  request.setRequestHeader("Content-type","application/x-www-form-urlencoded");
  request.send("param1=1&param2=2");
  } 
  function print_console(text){
    document.getElementById("console").innerHTML += text; 
  }


<a href="#" onclick="startAjax('/');">Post Ajax</a>  
<div id="console" style="border: 1px solid gray; width:250px; height: 110px; padding: 10px; background:lightgray;">
Cosole log panel
</div>
<br/>
<div id="printResult">
print result
</div>

```

##

```
## app04
Оставьте ваш комментарий
```
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
                if(param.statbox)document.getElementById(param.statbox).innerHTML = '<img src="www/wait.gif">';
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

    </head>
    <body>
        <div id="header">
            <span>My Simple Blog</span>
            <ul id="menu">
                <li><a class="article" href="hode.html">Comments</a></li>
                <li><a href=getpost.html class="article">Get/Post</a></li>
                <li><a href=ajax.html class="article">Ajax</a></li>
                <li><a href=table.html class="article">Table</a></li>
            </ul>
        </div>
        <div id="content">
        <div id="status" style="width:470px;background:#fff;padding:20px 10px 20px 10px;border:solid 5px #D1D1D1;font: 13 Arial;">
            Ни одного комментария пока нет.
        </div>
      <form action="/">
      <p><b>Оставьте ваш комментарий</b></p>
      <p><textarea id="area_1" name="area_1" style="height:50px; width:500px;padding:10px;font: 13 Arial;">Введите имя</textarea></p>
      <p><textarea id="area_2" name="area_1" style="height:100px; width:500px;padding:10px;font: 13 Arial;">Текст сообщения</textarea></p>
      <input type='button' value='Сохранить комментарий' onclick='
            ajax({
                  url:"/",
                  statbox:"status",
                  method:"POST",
                  data:
                 {                                                          first_area:document.getElementById("area_1").value,
                  second_area:document.getElementById("area_2").value
                 },
                 success:function(data){document.getElementById("status").innerHTML=data;}

                 })'
                >
                </form>
        </div>
```

