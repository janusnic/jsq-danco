# jsq-danco The Dialog  dialog1

To use the dialog, the following dependencies are required: 

- jquery-ui-x.x.x.custom.css 
- jquery-x.x.x.js 
- jquery.ui.core.js 
- jquery.ui.widget.js 
- jquery.ui.position.js 
- jquery.ui.dialog.js
```
<!DOCTYPE html> 
<html> 
    <head> 
        <meta charset="utf-8"> 
        <title>Dialog</title> 
        <link rel="stylesheet" href="css/smoothness/jquery-ui-1.8.9.custom.css"> 
    </head> 
    <body> 
        <div id="myDialog" title="This is the title!">Lorem ipsum dolor sit amet, consectetuer adipiscing elit. Aenean sollicitudin. Sed interdum pulvinar justo. Nam iaculis volutpat ligula. Integer vitae felis quis diam laoreet ullamcorper. Etiam tincidunt est vitae est.</div> 
        <script src="development-bundle/jquery-1.4.4.js"></script> 
        <script src="development-bundle/ui/jquery.ui.core.js"></script> 
        <script src="development-bundle/ui/jquery.ui.widget.js"></script> 
        <script src="development-bundle/ui/jquery.ui.position.js"></script> 
        <script src="development-bundle/ui/jquery.ui.dialog.js"></script> 
        <script> 
            (function($){ 
                $("#myDialog").dialog(); 
            })(jQuery); 
        </script> 
    </body> 
</html>
```
## dialog2 resizable.js

- jquery.ui.mouse.js 
- jquery.ui.draggable.js 
- jquery.ui.resizable.js
```
<div id="myDialog" title="This is the title!">Lorem ipsum dolor sit amet, consectetuer adipiscing elit. Aenean sollicitudin. Sed interdum pulvinar justo. Nam iaculis volutpat ligula. Integer vitae felis quis diam laoreet ullamcorper. Etiam tincidunt est vitae est.</div> 
<script src="development-bundle/ui/jquery.ui.mouse.js"></script> 
<script src="devpment-bundle/ui/jquery.ui.draggable.js"></script> 
<script src="devment-bundle/ui/jquery.ui.resizable.js"></script> 
            (function($){ 
                $("#myDialog").dialog(); 
            })(jQuery); 
```
## Dialog options dialog3
```
        <div id="myDialog" title="This is the title!"></div> 
        (function($){ 
            var dialogOpts = { 
                autoOpen: false  
            }; 
        $("#myDialog").dialog(dialogOpts); 
        })(jQuery); 
```

## The title of the dialog 4
```
            (function($){ 
                var dialogOpts = { 
                    title: "<a href='#'>A link title!</a>" 
                }; 
                $("#myDialog").dialog(dialogOpts); 
            })(jQuery); 
```
## Modality 5

```
            (function($){ 
                var dialogOpts = { 
                    modal: true 
                }; 
                $("#myDialog").dialog(dialogOpts); 
            })(jQuery); 
```
## Adding buttons 6
```
            (function($){ 
                var execute = function() {}, 
                    cancel = function() {}, 
                    dialogOpts = { 
                        buttons: { 
                            "Ok": execute, 
                            "Cancel": cancel 
                        } 
                    }; 
                $("#myDialog").dialog(dialogOpts); 
            })(jQuery); 
```
## Enabling dialog animations 7
```<script src="development-bundle/external/jquery.bgiframe-2.1.2.js"></script> 
            (function($){ 
                var dialogOpts = { 
                    show: true, 
                    hide: true                       
                }; 
                $("#myDialog").dialog(dialogOpts); 
            })(jQuery); 
Configuring the dialog's dimensions 8
            (function($){ 
                var dialogOpts = { 
                    width: 500, 
                    height: 300, 
                    minWidth: 150, 
                    minHeight: 150, 
                    maxWidth: 600, 
                    maxHeight: 450 
                }; 
                $("#myDialog").dialog(dialogOpts); 
            })(jQuery); 
```
## Stacking 9
```
            (function($){                
                $("#dialog1, #dialog2").dialog(); 
            })(jQuery); 
```

## Dialog's event model 10
```
        <div id="status" class="ui-widget ui-dialog ui-corner-all ui-widget-content"> 
            <div class="ui-widget-header ui-dialog-titlebar ui-corner-all">Dialog Status</div> 
            <div class="ui-widget-content ui-dialog-content"></div>     </div> 
    <div id="dialog1" title="Dialog 1">Lorem ipsum dolor sit amet, </div> 
        (function($){ 
            var dialogOpts = { 
                open: function() { 
        $("#status").children(":last").text("The dialog is open"); 
                }, 
                close: function() { 
        $("#status").children(":last").text("The dialog is closed"); 
                }, 
                beforeclose: function() {            
                    if ($("#dialog1").width() > 300) { 
                        return false; 
                    } 
                } 
            }; 
            $("#dialog1").dialog(dialogOpts); 
        })(jQuery); 
```

## Toggling the dialog 11
```
<button type="button" id="toggle">Toggle dialog!</button> 
        <div id="myDialog" title="This is the title!">Lorem ipsum 
            (function($){ 
                var dialogOpts = { 
                    autoOpen: false  
                }; 
                $("#myDialog").dialog(dialogOpts); 
                $("#toggle").click(function() { 
                    if (!$("#myDialog").dialog("isOpen")) { 
                        $("#myDialog").dialog("open"); 
                    } else { 
                        $("#myDialog").dialog("close"); 
                    }; 
                }); 
            })(jQuery); 
```
## Getting data from the dialog 12
```
<p>Please answer the opinion poll:</p> 
        <div id="myDialog" title="Best Widget Library"> 
    <p>Is jQuery UI the greatest JavaScript widget library?</p> 
            <label for="yes">Yes!</label> 
    <input type="radio" id="yes" value="yes" name="question" checked="checked"><br> 
            <label for="no">No!</label> 
<input type="radio" id="no" value="no" name="question"> 
        </div>
(function($){ 
    var execute = function() { 
    var answer = $("#myDialog").find("input:checked").val(); 

$("<p>").text("Thanks for selecting " + answer).appendTo($("body")); 
                        $("#myDialog").dialog("close"); 
                    }, 
                    cancel = function() { 
                        $("#myDialog").dialog("close"); 
                    }, 
                    dialogOpts = { 
                        buttons: { 
                            "Ok": execute, 
                            "Cancel": cancel 
                        } 
                    }; 
                $("#myDialog").dialog(dialogOpts); 
            })(jQuery); 
```

## Dialog interoperability 13
```
<div id="myDialog" title="An Accordion Dialog"> 
    <div id="myAccordion"> 
    <h2><a href="#">Header 1</a></h2> 
<div>Lorem ipsum dolor sit amet, consectetuer adipiscing elit. Aenean sollicitudin.</div> 
    <h2><a href="#">Header 2</a></h2> 
<div>Etiam tincidunt est vitae est. Ut posuere, mauris at sodales rutrum, turpis.</div> 
    <h2><a href="#">Header 3</a></h2> 
<div>Donec at dolor ac metus pharetra aliquam. Suspendisse purus.</div> 
    </div> 
</div>
<script src="devement-bundle/ui/jquery.ui.accordion.js"></script>
            (function($){ 
            $("#myDialog").dialog(); 
            $("#myAccordion").accordion(); 
            })(jQuery); 
```

## Creating a dynamic image-based dialog 14
```
<div id="thumbs" class="ui-corner-all"> 
<div class="ui-widget-header ui-corner-top"> 
    <h2>Some Common Flowers</h2> 
</div> 
<p>(click a thumbnail to view a full-size image)</p> 
    <div class="thumb ui-helper-clearfix ui-widget-content"> 
    <a href="img/haFull.jpg" title="Helianthus annuus"><img src="img/haThumb.jpg" alt="Helianthus annuus"></a> 
    <h3>Helianthus annuus</h3> 
    <p>Sunflowers (Helianthus annuus) are annual plants native to the Americas, that possess a large flowering head</p> 
</div> 
<div class="thumb ui-helper-clearfix ui-widget-content"> 
    <a href="img/lcFull.jpg" title="Lilium columbianum"><img src="img/lcThumb.jpg" alt="Lilium columbianum"></a> 
    <h3>Lilium columbianum</h3> 
    <p>The Lilium columbianum is a lily native to western North America. It is also known as the Columbia Lily or Tiger Lily</p> 
</div> 
<div class="thumb ui-helper-clearfix ui-widget-content"> 
    <a href="img/msFull.jpg" title="Myosotis scorpioides"><img src="img/msThumb.jpg" alt="Myosotis scorpioides"></a> 
    <h3>Myosotis scorpioides</h3> 
    <p>The Myosotis scorpioides, or Forget-me-not, is a herbaceous perennial plant of the genus Myosotis.</p> 
</div> 
<div class="thumb ui-helper-clearfix ui-widget-content ui-corner-bottom last"> 
    <a href="img/nnFull.jpg" title="Nelumbo nucifera"><img src="img/nnThumb.jpg" alt="Nelumbo nucifera"></a> 
    <h3>Nelumbo nucifera</h3> 
    <p>Nelumbo nucifera is known by a number of names including Indian lotus, sacred lotus, bean of India, or simply Lotus.</p> 
</div> 
</div> 
    <div id="dialog"></div>
<script src="devment-bundle/ui/jquery.ui.draggable.js"></script> 

            (function($){ 
                var fileName, 
                    titleText, 
                    dialogOpts = { 
                        modal: true, 
                        width: 388, 
                        height: 470, 
                        autoOpen: false, 
                        open: function() { 

                            $("#dialog").empty(); 
                            $("<img />", { 
                                src: fileName 
                            }).appendTo("#dialog"); 
                $("#dialog").dialog("option", "title", titleText); 
                        } 
                    }; 
                $("#dialog").dialog(dialogOpts); 
                $("#thumbs").find("a").click(function(e) { 
                    e.preventDefault(); 
                    fileName = $(this).attr("href"); 
                    titleText = $(this).attr("title"); 
                    $("#dialog").dialog("open"); 
                }); 
            })(jQuery); 

```
## The Slider Widget
### Implementing a slider1
```
<div id="mySlider"></div> 
 <script src="development-bundle/jquery-1.4.4.js"></script> 
 <script src="devpment-bundle/ui/jquery.ui.core.js"></script> 
 <script src="devopment-bundle/ui/jquery.ui.widget.js"></script> 
 <script src="development-bundle/ui/jquery.ui.mouse.js"></script> 
 <script src="development-bundle/ui/jquery.ui.slider.js"></script> 
        <script> 
            (function($){ 
                $("#mySlider").slider(); 
            })(jQuery); 
```
## Custom styling 2
```
<link rel="stylesheet" href="css/sliderTheme.css">
<div class="background-div"> 
<div id="mySlider"></div> 
</div>
            (function($){ 
                $("#mySlider").slider(); 
            })(jQuery); 
```

## Creating a vertical slider 3
```
            (function($){ 
                var sliderOpts = { 
                    orientation: "vertical"  
                }; 
                $("#mySlider").slider(sliderOpts); 
            })(jQuery); 
```
## Minimum and maximum values 4
```
            (function($){ 
                var sliderOpts = { 
                    min: -50, 
                    max: 50 
                }; 
                $("#mySlider").slider(sliderOpts); 
            })(jQuery); 
```
## Slider steps 5 
```
            (function($){ 
                var sliderOpts = { 
                    step: 25 
                }; 
                $("#mySlider").slider(sliderOpts); 
            })(jQuery); 
```
## Slider animation 6
```
            (function($){ 
                var sliderOpts = { 
                    animate: true 
                }; 
                $("#mySlider").slider(sliderOpts); 
            })(jQuery); 
```
## Setting the slider's value 7
```
            (function($){ 
                var sliderOpts = { 
                    value: 50 
                }; 
                $("#mySlider").slider(sliderOpts); 
            })(jQuery); 
```
## Using multiple handles 8
```
            (function($){ 
                var sliderOpts = { 
                    values: [25, 75] 
                }; 
                $("#mySlider").slider(sliderOpts); 
            })(jQuery); 
```
## The range element 9
```
            (function($){ 
                var sliderOpts = { 
                    values: [25, 75], 
                    range: true 
                }; 
                $("#mySlider").slider(sliderOpts); 
            })(jQuery); 
```
## A maximum of two handles 10
```
            (function($){ 
                var sliderOpts = { 
                    range: "min" 
                }; 
                $("#mySlider").slider(sliderOpts); 
            })(jQuery); 
```
## Using slider's event API 11
```
 <link rel="stylesheet" href="css/sliderTheme2.css">
            (function($){ 
                var sliderOpts = { 
                    start: function() { 
                        $("#tip").fadeOut(function() { 
                            $(this).remove(); 
                        });  
                    }, 
                    change: function(e, ui) { 
                    $("<div />", { 
                    "class": "ui-widget-header ui-corner-all", 
                            id: "tip", 
                            text: ui.value + "%", 
                            css: { 
                                left: e.pageX - 35                                  } 
                        }).appendTo("#mySlider"); 
                    } 
                }; 
                $("#mySlider").slider(sliderOpts); 
            })(jQuery); 
```
## Slider methods 12
```
value Set a single slider handle to a new value. This will move the handle to the new position on the track automatically. This method accepts a single argument which is an integer representing the new value .
<div id="mySlider"></div> 
   <button type="button" id="setMax">Set to max value</button> 
    (function($){ 
        $("#mySlider").slider(); 
        $("#setMax").click(function() { 
        var maxVal = $("#mySlider").slider("option", "max"); 
        $("#mySlider").slider("value", maxVal); 
        }); 
    })(jQuery); 
```
## Slider methods 13
```
values Set the specified handle to move to a new value when multiple handles are in use. This method is exactly the same as the valu e method, except that it takes two arguments—the index number of the handle followed by the new value.
<div id="mySlider"></div> 
        <button class="preset" id="low">Preset 1 (low)</button> 
    <button class="preset" id="high">Preset 2 (high)</button> 
            (function($){ 
                var sliderOpts = { 
                    values: [25, 75] 
                }; 
                $("#mySlider").slider(sliderOpts); 
                $(".preset").click(function() { 
                    if (this.id === "low") { 
                    $("#mySlider").slider("values", 0, 0); 
                    $("#mySlider").slider("values", 1, 25); 
                    } else { 
                    $("#mySlider").slider("values", 0, 75); 
                    $("#mySlider").slider("values", 1, 100); 
                    } 
                }); 
            })(jQuery); 
```
## audio id="audio" 14
```
<audio id="audio" src="http://upload.wikimedia.org/wikipedia/en/7/77/Jamiroquai_-_Snooze_You_Lose.ogg"> 
    Your browser does not support the audio element. 
</audio>  
<div id="volume"></div>
            (function($){ 
                var audio = $("audio")[0], 
                    sliderOpts = { 
                        value: 5, 
                        min: 0, 
                        max: 10, 
                        orientation: "vertical", 
                        change: function() { 
                        var vol = $(this).slider("value") / 10; 
                            audio.volume = vol; 
                        } 
                    }; 
                audio.volume = 0.5; 
                audio.play(); 
                $("#volume").slider(sliderOpts); 
            })(jQuery); 
```
## A color slider 15
```
<div id="container" class="ui-widget ui-corner-all ui-widget-content ui-helper-clearfix"> 
            <label>R:</label><div id="rSlider"></div><br> 
            <label>G:</label><div id="gSlider"></div><br> 
            <label>B:</label><div id="bSlider"></div> 
<div id="colorBox" class="ui-corner-all ui-widget-content"></div> 
<input id="output" type="text" value="rgb(255,255,255)"> 
<label for="output" id="outputLabel">Color value:</label> 
</div>
(function($){ 
        var sliderOpts = { 
            min:0, 
            max: 255, 
            value: 255, 
    slide: function() { 
        var r = $("#rSlider").slider("value"), 
        g = $("#gSlider").slider("value"), 
        b = $("#bSlider").slider("value"); 
    var rgbString = ["rgb(", r, ",", g, ",", b, ")"].join(""); 
    $("#colorBox").css({ backgroundColor: rgbString }); 
                $("#output").val(rgbString); 
            } 
        }; 
$("#rSlider, #gSlider, #bSlider").slider(sliderOpts); 
})(jQuery); 
```

## The Datepicker Widget 1
```
<label>Enter a date: </label><input id="date"> 
        <script src="development-bundle/jquery-1.4.4.js"></script> 
        <script src="devment-bundle/ui/jquery.ui.core.js"></script> 
<script src="devent-bundle/ui/jquery.ui.datepicker.js"></script> 
            (function($){ 
                $("#date").datepicker(); 
            })(jQuery); 
```
## Configurable options of the datepicker 2
```
            (function($){ 
                var pickerOpts = { 
                    appendText: "(mm/dd/yy)", 
                    defaultDate: "+5", 
                    showOtherMonths: true 
                }; 
                $("#date").datepicker(pickerOpts); 
            })(jQuery); 
```
## 3 maxDate
```
            (function($){ 
                var pickerOpts = { 
                    minDate: new Date(), 
                    maxDate: "+10" 
                }; 
                $("#date").datepicker(pickerOpts); 

            })(jQuery); 
```
## 4 changeMonth
```
            (function($){ 
                var pickerOpts = { 
                    changeMonth: true, 
                    changeYear: true 
                }; 
                $("#date").datepicker(pickerOpts); 
            })(jQuery); 
```
## 5 yearRange
```
            (function($){ 
                var pickerOpts = { 
                    changeMonth: true, 
                    changeYear: true, 
                    yearRange: "-25:+25" 
                }; 
                $("#date").datepicker(pickerOpts); 
            })(jQuery); 
```
## 6 showButtonPanel
```            (function($){ 
                var pickerOpts = { 
                    showButtonPanel: true 
                }; 
                $("#date").datepicker(pickerOpts); 
            })(jQuery); 
```
## 7  showOn
```
            (function($){ 
                var pickerOpts = { 
                    showOn: "button" 
                }; 
                $("#date").datepicker(pickerOpts); 
            })(jQuery); 
```
## 8  buttonText
```
            (function($){ 
                var pickerOpts = { 
                    showOn: "button", 
                    buttonText: "Open Picker" 
                }; 
                $("#date").datepicker(pickerOpts); 
            })(jQuery); 
```
## 9  buttonImage
```
            (function($){ 
                var pickerOpts = { 
                    showOn: "button", 
                    buttonText: "Open Picker", 
                    buttonImage: "img/cal.png" 
                }; 
                $("#date").datepicker(pickerOpts); 
            })(jQuery); 
```
## 10  buttonImageOnly
```
            (function($){ 
                var pickerOpts = { 
                    showOn: "button", 
                    buttonText: "Open Picker", 
                    buttonImage: "img/cal.png", 
                    buttonImageOnly: true 
                }; 
                $("#date").datepicker(pickerOpts); 
            })(jQuery); 
```
## 11  duration
```
   
            (function($){ 
                var pickerOpts = { 
                    duration: "fast" 
                }; 
                $("#date").datepicker(pickerOpts); 
            })(jQuery); 
```   
## 12 showOptions
```
<script src="devpment-bundle/ui/jquery.effects.core.js"></script> 
        <script src="devt-bundle/ui/jquery.effects.drop.js"></script> 
            (function($){ 
                var pickerOpts = { 
                    showAnim: "drop", 
                    showOptions: { direction: "up" } 
                }; 
                 
                $("#date").datepicker(pickerOpts); 
            })(jQuery); 
```
## 13 numberOfMonths
```
            (function($){ 
                var pickerOpts = { 
                    numberOfMonths: 3 
                }; 
                $("#date").datepicker(pickerOpts); 
            })(jQuery); 
```
## 14 Changing the date format
```
            (function($){ 
                var pickerOpts = { 
                    dateFormat: "d MM yy" 
                }; 
                $("#date").datepicker(pickerOpts); 
            })(jQuery); 
```

## 15 dateFormat: "Selecte'd': d MM yy" 
```
 <script src="devment-bundle/ui/jquery.effects.core.js"></script> 
<script src="devment-bundle/ui/jquery.effects.drop.js"></script> 
            (function($){ 
                var pickerOpts = { 
                    dateFormat: "Selecte'd': d MM yy" 
                }; 
                $("#date").datepicker(pickerOpts); 
            })(jQuery); 
```
## 16 dateFormat: $.datepicker.ATOM    
```
<script src="devment-bundle/ui/jquery.effects.core.js"></script> 
        <script src="devt-bundle/ui/jquery.effects.drop.js"></script> 
            (function($){ 
                var pickerOpts = { 
                    dateFormat: $.datepicker.ATOM                   }; 
                $("#date").datepicker(pickerOpts); 
            })(jQuery); 
```
## 17  TIMESTAMP
```
<script src="devment-bundle/ui/jquery.effects.core.js"></script> 
<script src="devment-bundle/ui/jquery.effects.drop.js"></script> 
        <script> 
            (function($){ 
                var pickerOpts = { 
                    altField: "#alt", 
                    altFormat: $.datepicker.TIMESTAMP                           }; 
            $("#date").datepicker(pickerOpts); 
            })(jQuery); 
        </script>
```
## 18 Localization
```
<script src="development-bundle/ui/i18n/jquery.ui.datepicker-fr.js"></script> 
        <script> 
            (function($){ 
                $("#date").datepicker(); 
            })(jQuery); 
        </script>
```
## 19  For example, to implement a Lolcat datepicker, change the configuration object of datePicker6.html to the following:
``` 
 <script> 
    (function($){ 
            var pickerOpts = { 
        closeText: "Kthxbai", 
            currentText: "Todai", 
            nextText: "Fwd", 
            prevText: "Bak", 
monthNames: ["January", "February", "March", "April", "Mai", "Jun", "July", "August", "Septembr", "Octobr", "Novembr", "Decembr"], 
monthNamesShort: ["Jan", "Feb", "Mar", "Apr", "Mai", "Jun", "Jul", "Aug", "Sep", "Oct", "Nov", "Dec"], 
dayNames: ["Sundai", "Mondai", "Tuesdai", "Wednesdai", "Thursdai", "Fridai", "Katurdai"], 
dayNamesShort: ["Sun", "Mon", "Tue", "Wed", "Thu", "Fri", "Kat"], 
    dayNamesMin: ["Su", "Mo", "Tu", "We", "Th", "Fr", "Ka"], 
                    dateFormat: 'dd/mm/yy', 
                    firstDay: 1, 
                    isRTL: false, 
                    showButtonPanel: true    
            }; 
        $("#date").datepicker(pickerOpts); 
    })(jQuery); 
</script>
```
## 20 Callback properties
```
<label>Enter a date: </label><input id="date"> 
        <select id="language"> 
            <option id="en-GB">English</option> 
            <option id="ar">Arabic</option> 
            <option id="uk">Ukrainian</option> 
            <option id="zh-TW">Taiwanese</option> 
        </select> 
Next link to the i18n.js roll-up file as follows:
        <script src="development-bundle/ui/i18n/jquery-ui-i18n.js"></script> 
Now change the final <script> element so that it appears as follows:
            (function($){ 
                var pickerOpts = { 
                    beforeShow: function() { 
    var lang = $(":selected", $("#language")).attr("id"); 
                        $.datepicker.setDefaults($.datepicker.regional[lang]); 
                    } 
                }; 
                $("#date").datepicker(pickerOpts); 
                $.datepicker.setDefaults($.datepicker.regional['']); 
            })(jQuery); 
```
## 21 Utility methods Selecting a date programmatically
```
            (function($){ 
                $("#date").datepicker(); 
                $("#select").click(function() { 
                    $("#date").datepicker("setDate", "+7"); 
                }); 
            })(jQuery); 
```
## 22  Date picking methods  updateDate
```
            (function($){ 
                function updateDate(date) { 
                    $("#date").val(date); 
                } 
        $("#date").focus(function() { 
            $(this).datepicker("dialog", null, updateDate); 
        }); 
    })(jQuery); 
```
## 23  Showing the datepicker in a dialog box
```
<div id="bookingForm" class="ui-widget ui-corner-all"> 
            <div class="ui-widget-header ui-corner-top"> 
                <h2>Booking Form</h2> 
            </div> 
            <div class="ui-widget-content ui-corner-bottom"> 
        <label>Appointment date:</label><input id="date"> 
            </div> 
</div> 
<script src="development-bundle/jquery-1.4.4.js"></script> 
<script src="development-bundle/ui/jquery.ui.core.js"></script> 
<script src="devent-bundle/ui/jquery.ui.datepicker.js"></script> 

    (function($){ 
        var months = [], 
        days = []; 
$.getJSON("http://www.danwellman.co.uk/bookedDates.php?jsoncallback=?", function(data) { 
        for (var x = 0; x < data.dates.length; x++) { 
            months.push(data.dates[x].month); 
            days.push(data.dates[x].day); 
            } 
        }); 
function addDates(date) { 
        if (date.getDay() == 0 || date.getDay() == 6) { 
            return [false, ""]; 
        } 
for (var x = 0; x < days.length; x++) { 
if (date.getMonth() == months[x] - 1 && date.getDate() == days[x]) {                        
return [false, "preBooked_class"];                      } 
        } 
        return [true, ""]; 
    } 
    var pickerOpts = { 
        beforeShowDay: addDates, 
        minDate: "+1" 
        }; 
    $("#date").datepicker(pickerOpts); 
})(jQuery); 
```
## Progressbar
### 1 The default progressbar implementation
```
<div id="myProgressbar"></div> 
<script src="development-bundle/jquery-1.4.4.js"></script> 
 <script src="development-bundle/ui/jquery.ui.core.js"></script> 
<script src="development-bundle/ui/jquery.ui.widget.js"></script> 
<script src="devnt-bundle/ui/jquery.ui.progressbar.js"></script> 
            (function($){ 
                $("#myProgressbar").progressbar(); 
            })(jQuery); 
```
## 2  Setting progressbar's value
```
            (function($){ 
                var progressOpts = { 
                    value: 50    
                }; 
            $("#myProgressbar").progressbar(progressOpts); 
            })(jQuery); 
```
## 3  Progressbar's event API
```
(function($){ 
var progress = $("#myProgressbar"), 
    progressOpts = { 
    change: function() { 
            var val = $(this).progressbar("option", "value"); 
                            if (!$("#value").length) { 
                                $("<span />", { 
                                    text: val + "%", 
                                    id: "value", 
                                    css: { 
                                        float: "right", 
                                        marginTop: -28, 
                                        marginRight: 10 
                                    } 
                                }).appendTo(progress); 
                            } else { 
                            $("#value").text(val + "%");     
                            } 
                        } 
                    }; 
progress.progressbar(progressOpts); 
    $("#increase").click(function() { 
        var currentVal = progress.progressbar("option", "value"), 
        newVal = currentVal + 10; 
        progress.progressbar("option", "value", newVal); 
                }); 
            })(jQuery); 
```
## 4 Progressbar methods
```
(function($){ 
var progress = $("#myProgressbar"); 
progress.progressbar(); 
$("#increase").click(function() { 
    var currentVal = progress.progressbar("option", "value"), 
            newVal = currentVal + 10; 
            progress.progressbar("value", newVal); 
                if (!$("#value").length) { 
                    $("<span />", { 
                        text: newVal + "%", 
                            id: "value", 
                            css: { 
                                float: "right", 
                                marginTop: -28, 
                                marginRight: 10 
                            } 
                        }).appendTo(progress); 
                    } else { 
                        $("#value").text(val + "%");     
                    } 
                }); 
            })(jQuery); 
```
## 5 User initiated progress
```
        <link rel="stylesheet" href="css/progressTheme.css"> 
    <div class="form-container ui-helper-clearfix ui-corner-all"> 
            <h1>Registration Form</h1> 
            <p>Progress:</p> 
            <div id="myProgressbar"></div> 
            <label id="amount">0%</label> 
            <form action="serverScript.php"> 
                <div class="form-panel"> 
                    <h2>Personal Details</h2> 
<fieldset class="ui-corner-all"> 
                        <label>Name:</label><input type="text"> 
                        <label>D.O.B:</label><input type="text"> 
<label>Choose password:</label><input type="password"> 
<label>Confirm password:</label><input type="password"> 
                    </fieldset> 
                </div> 
                <div class="form-panel ui-helper-hidden"> 
<h2>Contact Details</h2> 
<fieldset class="ui-corner-all"> 
<label>Email:</label><input type="text"> 
<label>Telephone:</label><input type="text"> 
<label>Address:</label><textarea rows="3" cols="25"> </textarea> 
</fieldset> 
</div> 
                <div class="form-panel ui-helper-hidden"> 
                    <h2>Registration Complete</h2> 
                    <fieldset class="ui-corner-all"> 
                        <p>Thanks for registering!</p> 
                    </fieldset> 
                </div> 
            </form> 
<button id="next">Next</button><button id="back" disabled="disabled">Back</button> 
</div> 
(function($){ 
var prog = $("#myProgressbar"), 
progressOpts = { 
    change: function() { 
        prog.next().text(prog.progressbar("value") + "%"); 
        } 
    }; 
        prog.progressbar(progressOpts); 
        $("#next, #back").click(function() { 
        $("button").attr("disabled", true); 
    if (this.id === "next") { 
prog.progressbar("option", "value", prog.progressbar("option", "value") + 50); 
    $("form").find("div:visible").fadeOut().next().fadeIn(function(){ 
        $("#back").attr("disabled", false); 
        if (!$("form").find("div:last").is(":visible")) { 
        $("#next").attr("disabled", false); 
    } 
    }); 
    } else { 
prog.progressbar("option", "value", prog.progressbar("option", "value") - 50); 
$('form').find("div:visible").not(".buttons").fadeOut().prev().fadeIn(    
function()  { 
$("#next").attr("disabled", false); 
            if (!$("form").find("div:first").is(":visible")) { 
                $("#back").attr("disabled", false);  
                } 
            }); 
        } 
    }); 
})(jQuery); 
```
## 6   Rich uploads with progressbar
```
        <link rel="stylesheet" href="css/progressTheme2.css"> 
        <h2>AJAX File Upload</h2> 
        <input type="file" id="file" /> 
        <div id="myProgressbar"></div> 
            (function($){ 
                var prog = $("#myProgressbar"), 
                inputFile = $("#file"), 
                progressOpts = { 
                complete: function() { 
                $("#filename").text("Complete!"); 
            } 
        } 
            inputFile.change(function() { 
            prog.progressbar(progressOpts); 
var files = inputFile.attr("files"), 
        file = files[0], 
        xhr = new XMLHttpRequest(); 
xhr.upload.onprogress = function updateProgress(e) { 
    var loaded = (e.loaded / e.total); 
prog.progressbar("value", Math.round(loaded * 100)); 
                    } 
                    xhr.upload.onload = function() { 
                        prog.progressbar("value", 100); 
                    } 
                    $("<apan />", { 
                        id: "filename", 
                        text: file.fileName 
                    }).insertAfter(prog); 
                xhr.open("POST", "progressUpload.php"); 
            xhr.sendAsBinary(file.getAsBinary()); 
        }); 
    })(jQuery); 
```
## Autocomplete Widgets
```        
<link rel="stylesheet" href="css/smoothness/jquery-ui-1.8.9.custom.css"> 
<label>Enter your city:</label><input id="city"> 
<script src="development-bundle/jquery-1.4.4.js"></script> 
<script src="development-bundle/ui/jquery.ui.core.js"></script> 
<script src="development-bundle/ui/jquery.ui.widget.js"></script> 
<script src="development-bundle/ui/jquery.ui.position.js"></script> 
<script src="development-bundle/ui/jquery.ui.autocomplete.js"></script> 
        <script> 
            (function($){ 
                var autoOpts = { 
                    source: [ 
                        "Aberdeen", 
                        "Armagh", 
                        "Bangor", 
                        "York" 
                    ] 
                }; 
                $("#city").autocomplete(autoOpts); 
            })(jQuery); 
```
## 2  Using an array of objects as the data source
```
            (function($){ 
                var autoOpts = { 
                    source: [ 
                        { value: "AB", label: "Aberdeen" }, 
                        { value: "AR", label: "Armagh" }, 
                        { value: "BA", label: "Bangor" }, 
                    ] 
                }; 
                $("#city").autocomplete(autoOpts); 
            })(jQuery); 
```
## 3 Configuring minimum length
```
            (function($){ 
                var autoOpts = { 
                    minLength: 2, 
                    source: [ 
                        "Aberdeen", 
                        "Armagh", 
                        "Bangor", 
                    ] 
                }; 
        $("#city").autocomplete(autoOpts); 
    })(jQuery); 
```
## 4 Appending the suggestion list to an alternative element

```
        <div id="container"> 
            <label>Enter your city:</label><input id="city"> 
        </div>

            (function($){ 
                var autoOpts = { 
                    appendTo: "#container", 
                    source: [ 
                        "Aberdeen", 
                        "Armagh", 
                        ] 
            }; 
        $("#city").autocomplete(autoOpts); 
})(jQuery); 
```
## 5  Autocomplete events select A suggestion from the list is selected 
```
(function($){ 
var autoOpts = { 
    source: [ 
    { value: "AR", label: "Armagh", population: 54263 }, 
    { value: "BA", label: "Bangor", population: 21735 }, 
    { value: "BA", label: "Bath", population: 83992 }, 
            ], 
select: function(e, ui) { 
if ($("#pop").length) { 
$("#pop").text(ui.item.label + "'s population is: " + ui.item.population);   
        } else { 
        $("<p></p>", { 
        id: "pop", 
text: ui.item.label + "'s population is: " + ui.item.population 
            }).insertAfter("#city"); 
        } 
    } 
}; 
    $("#city").autocomplete(autoOpts); 
})(jQuery); 
```
## 6 Working with remote data sources
```
(function($){ 
var autoOpts = { 
    source: "http://danwellman.co.uk/countries.php?callback=?" 
        }; 
        $("#country").autocomplete(autoOpts); 
})(jQuery); 
```
## 7 Using a function as the value of the source option
```
<link rel="stylesheet" href="css/autocompleteTheme.css"> 
<div id="formWrap"> 
<form id="messageForm" action="#"> 
<fieldset> 
    <legend>New message form</legend> 
    <span>New Message</span> 
           <div class="inner-form ui-helper-clearfix"> 
    <label>To:</label> 
    <div id="toList" class="ui-helper-clearfix"> 
    <input id="to"> 
                  <input id="emails" type="hidden"> 
    </div> 
<label>Message:</label> 
<textarea id="message" name="message" rows="2" cols="50"></textarea> 
            </div> 
           <div class="buttons ui-helper-clearfix"> 
                        <button type="submit">Send</button> 
            <a href="#" title="Cancel">Cancel</a> 
          </div> 
</fieldset> 
</form> </div> 
            (function($){ 
    var autoOpts = { 
    source: function(req, resp){ 
                         
    //request data 
                    $.getJSON("http://danwellman.co.uk/contacts.php?callback=?", req, function(data) { 
                                 
//create array for response objects 
    var suggestions = []; 
                                 
    //process response 
    $.each(data, function(i, val){ 
    var obj = {}; 
    obj.value = val.name; 
    obj.email = val.email;                               
    suggestions.push(obj); 
    }); 
                         
    //pass array to callback 
    resp(suggestions); 
    }); 
}, 
    select: function(e, ui) { 
    //create formatted email 
            var emailList = $("#emails"), 
            emails = emailList.val().split(","), 
            span = $("<span></span>", { 
            text: ui.item.value, 
            data: {"email": ui.item.email} 
            }), 
            a = $("<a></a>", { 
            "class": "remove", 
            href: "#", 
            title: "Remove", 
            text: "x" 
            }).appendTo(span); 
                             
        //add contact to friend div 
            span.insertBefore("#to"); 
         //update emails list                                
            emails.push(ui.item.email); 
            emailList.val(emails.join(",")); 
        //tidy input 
            $("#to").remove(); 
            $("<input/>", { 
            id: "to"     
            }).insertBefore("#emails").autocomplete(autoOpts); 
            } 
        }; 
        //attach autocomplete 
            $("#to").autocomplete(autoOpts); 
            //add click handler to friends div 
            $("#toList").click(function(){ 
            $("#to").focus(); 
        }); 
    //add delegate handler for clicks on remove links 
        $("#toList").delegate("a", "click", function(){ 
    //get email address of contact 
        var email = $(this).parent().data("email"), 
        emails = $("#emails").val().split(","); 
    //remove contact 
        $(this).parent().remove(); 
    //remove email 
        $.each(emails, function(i, val) { 
        if (val === email) { 
        emails.splice(i, 1); 
        } 
    }); 
        $("#emails").val(emails); 
    });              
})(jQuery); 
```
## 8 Displaying HTML in the list of suggestions
```
        <script src="js/jquery.ui.autocomplete.html.js"></script> 

            (function($){ 
                var data = [ 
                    { value: "Aberdeen", label: "Aberdeen" }, 
                    { value: "Armagh", label: "Armagh" }, 
                    { value: "Bangor", label: "Bangor" }, 
                ], 
                autoOpts = { 
                    html: true, 
                    source: function(req, resp) { 
                        var suggestions = [], 
                    regEx = new RegExp("^" + req.term, "i"); 
                        //match suggestions to input 
                        $.each(data, function(i, val){   
                            if (val.label.match(regEx)) { 
                                var obj = {}; 
                                obj.value = val.value; 
obj.label = val.label.replace(regEx, "<span>" + req.term + "</span>"); 
                                suggestions.push(obj);       
                            } 
                        }); 
                        resp(suggestions); 
                    } 
                }; 
                $("#city").autocomplete(autoOpts); 
            })(jQuery); 
```
## The button widget 
## 1 Standard implementations
```
<link rel="stylesheet" href="css/smoothness/jquery-ui-1.8.9.custom.css"> 
<a href="#" id="myButton">A link button</a> 
<script src="development-bundle/jquery-1.4.4.js"></script> 
<script src="development-bundle/ui/jquery.ui.core.js"></script> 
<script src="development-bundle/ui/jquery.ui.widget.js"></script> 
<script src="development-bundle/ui/jquery.ui.button.js"></script> 
            (function($){ 
                $("#myButton").button(); 
            })(jQuery); 
```
## 2 Theming
```
<link rel="stylesheet" href="css/smoothness/jquery-ui-1.8.9.custom.css"> 
<a href="#" id="myButton">A link button</a> 
            (function($){ 
                var buttonOpts = { 
                    label: "A configured label"  
                }; 
                $("#myButton").button(buttonOpts); 
            })(jQuery); 
```
## 3 Button icons
```
<a href="#" id="myButton">A link button</a> 
            (function($){ 
                var buttonOpts = { 
                    icons: { 
                        primary: "ui-icon-disk", 
                        secondary: "ui-icon-triangle-1-s" 
                    } 
                }; 
                $("#myButton").button(buttonOpts); 
            })(jQuery); 
```
## 4  Button icons
```
        <link rel="stylesheet" href="css/smoothness/jquery-ui-1.8.9.custom.css"> 
<a href="#" id="myButton">A link button</a> 
<script src="development-bundle/ui/jquery.ui.button.js"></script> 

            (function($){ 
                var buttonOpts = { 
                    icons: { 
                        primary: "ui-icon-disk", 
                        secondary: "ui-icon-triangle-1-s" 
                    }, 
                    text: false 
                }; 
                $("#myButton").button(buttonOpts); 
            })(jQuery); 
```
## 5  Button events
```
<link rel="stylesheet" href="css/smoothness/jquery-ui-1.8.9.custom.css"> 
<link rel="stylesheet" href="css/buttonTheme.css"> 
<div class="iconic-input ui-button-text-icons ui-state-default ui-corner-all"> 
<span class="ui-button-icon-primary ui-icon ui-icon-disk"></span> 
<input id="myButton" type="button" value="Input icons" class="ui-button-text"> 
<span class="ui-button-icon-secondary ui-icon ui-icon-triangle-1-s"></span> 
        </div> 
<script src="development-bundle/ui/jquery.ui.button.js"></script> 
            (function($){ 
                $("#myButton").button().hover(function() { 
                $(this).parent().addClass("ui-state-hover"); 
                }, function() { 
                $(this).parent().removeClass("ui-state-hover"); 
                }); 
            })(jQuery); 
```
## 6  create
```
        <link rel="stylesheet" href="css/smoothness/jquery-ui-1.8.9.custom.css"> 
        <button id="myButton">A button</button> 
        <script src="development-bundle/jquery-1.4.4.js"></script> 
<script src="development-bundle/ui/jquery.ui.core.js"></script> 
<script src="development-bundle/ui/jquery.ui.widget.js"></script> 
<script src="development-bundle/ui/jquery.ui.button.js"></script> 
            (function($){ 
                var buttonOpts = { 
                    create: function() { 
                        $(this).css("display", "none")   
                    } 
                }; 
                $("#myButton").button(buttonOpts) 
            })(jQuery); 
```
## 7  Register  form
```
<title>Button</title> 
        <link rel="stylesheet" href="css/smoothness/jquery-ui-1.8.9.custom.css"> 
        <form> 
<label for="name">Name: <input id="name" name="name"></label> 
<label for="email">Email: <input id="email" name="email"></label> 
            <button id="myButton">Register</button> 
        </form> 
<script src="development-bundle/jquery-1.4.4.js"></script> 
<script src="development-bundle/ui/jquery.ui.core.js"></script> 
<script src="development-bundle/ui/jquery.ui.widget.js"></script> 
<script src="development-bundle/ui/jquery.ui.button.js"></script> 
            (function($){                
                $("#myButton").button().click(function(e) { 
                    e.preventDefault(); 
                    var form = $("form"), 
                        formData = { 
                        name: form.find("#name").val(), 
                            email: form.find("#email").val() 
                        }; 
            $.post("register.php", formData, function() { 
            $("#myButton").button("option", "disabled", true); 
                        form.find("label").remove(); 
                        $("<label></label>", { 
                            text: "Thanks for registering!" 
                        }).prependTo(form); 
                    }); 
                }); 
            })(jQuery); 
```
## 8  buttonset
```
        <link rel="stylesheet" href="css/smoothness/jquery-ui-1.8.9.custom.css"> 
        <div id="buttons"> 
            <h2>Programming Languages</h2> 
            <p>Select all languages you know:</p> 
<label for="js">JavaScript</label><input id="js" type="checkbox"> 
<label for="py">Python</label><input id="py" type="checkbox"> 
<label for="cSharp">C#</label><input id="cSharp" type="checkbox"> 
<label for="jv">Java</label><input id="jv" type="checkbox"> 
        </div> 
        <script src="development-bundle/jquery-1.4.4.js"></script> 
<script src="development-bundle/ui/jquery.ui.core.js"></script> 
<script src="development-bundle/ui/jquery.ui.widget.js"></script> 
<script src="development-bundle/ui/jquery.ui.button.js"></script> 
            (function($){                
                $("#buttons").buttonset();   
            })(jQuery); 
```
## 9   buttonset       
```
        <link rel="stylesheet" href="css/smoothness/jquery-ui-1.8.9.custom.css"> 
        <div id="buttons"> 
            <h2>Programming Languages</h2> 
            <p>Select your most proficient languages:</p> 
<label for="js">JavaScript</label><input id="js" type="radio" name="lang"> 
        <label for="py">Python</label><input id="py" type="radio" name="lang"> 
    <label for="cSharp">C#</label><input id="cSharp" type="radio" name="lang"> 
<label for="jv">Java</label><input id="jv" type="radio" name="lang"> 
        </div> 
        <script src="development-bundle/jquery-1.4.4.js"></script> 
        <script src="development-bundle/ui/jquery.ui.core.js"></script> 
<script src="development-bundle/ui/jquery.ui.widget.js"></script> 
<script src="development-bundle/ui/jquery.ui.button.js"></script> 
            (function($){                
                $("#buttons").buttonset();   
            })(jQuery); 
```
## 10 Checkbox buttonsets
```
<title>Button</title> 
<link rel="stylesheet" href="css/smoothness/jquery-ui-1.8.9.custom.css"> 
<div id="buttons"> 
<h2>Programming Languages</h2> 
<p>Select all languages you know:</p> 
<label for="js1">JavaScript</label><input id="js1" type="checkbox"> 
<label for="py1">Python</label><input id="py1" type="checkbox"> 
<label for="cSharp1">C#</label><input id="cSharp1" type="checkbox"> 
<label for="jv1">Java</label><input id="jv1" type="checkbox"> 
        </div> 
        <button id="select">Select All</button> 
        <button id="deselect">Deselect All</button>        
        <script src="development-bundle/jquery-1.4.4.js"></script> 
<script src="development-bundle/ui/jquery.ui.core.js"></script> 
<script src="development-bundle/ui/jquery.ui.widget.js"></script> 
<script src="development-bundle/ui/jquery.ui.button.js"></script> 
            (function($){                
                $("#buttons").buttonset(); 
            $("#select").button().click(function() { 
$("#buttons").find("input").attr("checked", true).button("refresh"); 
    }); 
         
            $("#deselect").button().click(function() { 
$("#buttons").find("input").attr("checked", false).button("refresh"); 
    });              
            })(jQuery); 

```
## jQuery UI Sortable
```
    <link rel="stylesheet" href="http://necolas.github.com/normalize.css/2.0.1/normalize.css">
    <link rel="stylesheet" href="style.css" />
    <script src="http://code.jquery.com/jquery-1.8.2.js"></script>
    <script src="http://code.jquery.com/ui/1.9.1/jquery-ui.js"></script>

    <script>
    $(function() {
        $( "#sortable" ).sortable({ 
            placeholder: "ui-sortable-placeholder" 
        });
    });
    </script>

<ul id="sortable">
    <li class="ui-state-default">Item 1</li>
    <li class="ui-state-default">Item 2</li>
    <li class="ui-state-default">Item 3</li>
    <li class="ui-state-default">Item 4</li>
    <li class="ui-state-default">Item 5</li>
    <li class="ui-state-default">Item 6</li>
    <li class="ui-state-default">Item 7</li>
</ul>
```

## jQuery Sortable With AJAX &amp; MYSQL
```
<script type="text/javascript" src="../js/jquery.min.js"></script>
<script type="text/javascript" src="../js/jquery-ui.min.js"></script>
<link rel='stylesheet' href='styles.css' type='text/css' media='all' />
<script type="text/javascript">
// When the document is ready set up our sortable with it's inherant function(s)
  $(document).ready(function() {
    $("#test-list").sortable({
      handle : '.handle',
      update : function () {
          var order = $('#test-list').sortable('serialize');
        $("#info").load("process-sortable.php?"+order);
      }
    });
});
</script>


<pre>
<div id="info">Waiting for update</div>
</pre>
<ul id="test-list">
  <li id="listItem_1"><img src="arrow.png" alt="move" width="16" height="16" class="handle" /><strong>Item 1 </strong>with a link to <a href="http://www.google.co.uk/" rel="nofollow">Google</a></li>
  <li id="listItem_2"><img src="arrow.png" alt="move" width="16" height="16" class="handle" /><strong>Item 2</strong></li>
  <li id="listItem_3"><img src="arrow.png" alt="move" width="16" height="16" class="handle" /><strong>Item 3</strong></li>
  <li id="listItem_4"><img src="arrow.png" alt="move" width="16" height="16" class="handle" /><strong>Item 4</strong></li>
</ul>
```

## process-sortable.php

```
<?php
/* This is where you would inject your sql into the database 
   but we're just going to format it and send it back
*/

foreach ($_GET['listItem'] as $position => $item) :
    $sql[] = "UPDATE `table` SET `position` = $position WHERE `id` = $item";
endforeach;

print_r ($sql);
?>
```
