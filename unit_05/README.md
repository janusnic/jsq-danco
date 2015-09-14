# jsq-danco

# hide
```
$(document).ready(function(){
                           
    $(".pane .delete").click(function(){
        $(this).parents(".pane").animate({ opacity: 'hide' }, "slow");
    });

});
```

# jQuery. Animated Menu Hover 1
```
$(document).ready(function(){

    $(".menu a").hover(function() {
        $(this).next("em").stop(true,true)
                          .animate({opacity: "show", top: "-75"}, "slow");
    }, function() {
        $(this).next("em").stop(true,true)
                          .animate({opacity: "hide", top: "-85"}, "fast");
    });


});

```
# jQuery. Animated Menu Hover 2
```
$(document).ready(function(){

    $(".menu2 a").append("<em></em>");
    
    $(".menu2 a").hover(function() {
        $(this).find("em").stop(true, true).animate({opacity: "show", top: "-75"}, "slow");
        var hoverText = $(this).attr("title");
        $(this).find("em").text(hoverText);
    }, function() {
        $(this).find("em").stop(true, true).animate({opacity: "hide", top: "-85"}, "fast");
    });


});
```

# accordion
```
$(document).ready(function(){
    
    $(".accordion h3:first").addClass("active");
    $(".accordion p:not(:first)").hide();

    $(".accordion h3").click(function(){
        $(this).next("p").slideToggle("slow")
        .siblings("p:visible").slideUp("slow");
        $(this).toggleClass("active");
        $(this).siblings("h3").removeClass("active");
    });

});
```
# accordion
```
$(document).ready(function(){
    
    $(".accordion2 h3").eq(2).addClass("active");
    $(".accordion2 p").eq(2).show();

    $(".accordion2 h3").click(function(){
        $(this).next("p").slideToggle("slow")
        .siblings("p:visible").slideUp("slow");
        $(this).toggleClass("active");
        $(this).siblings("h3").removeClass("active");
    });

});
```

# slideToggle
```
$(document).ready(function(){

    $(".btn-slide").click(function(){
        $("#panel1").slideToggle("slow");
        $(this).toggleClass("active"); return false;
    });
    
    $(".btn-slide2").click(function(){
        $("#panel2").slideToggle("slow");
        $(this).toggleClass("active2"); return false;
    });
    
     
});
```

# on
```

$(document).ready(function(){
    $(".btn-slide").on('click', function(){
        if($(".panel1").css('width') === '120px'){
            $(".panel1").animate({width: '0px'}, 'slow');
        }
        else {
            $(".panel1").animate({width: '120px'}, 'slow');
        }
    });  
});

```

# drop down 

```
$(document).ready(function(){
    $('.topmenu ul li').hover(
        function() {
            $(this).addClass("active");
            $(this).find('ul').stop(true, true);
            $(this).find('ul').slideDown();
        },
        function() {
            $(this).removeClass("active");
            $(this).find('ul').slideUp('slow');
        }
    );
});

$(document).ready(function(){

    $("ul.subnav").parent().append("<span></span>"); //Only shows drop down trigger when js is enabled - Adds empty span tag after ul.subnav
    
    $("ul.topnav li span").click(function() { //When trigger is clicked...
        
        //Following events are applied to the subnav itself (moving subnav up and down)
        $(this).parent().find("ul.subnav").slideDown('fast').show(); //Drop down the subnav on click

        $(this).parent().hover(function() {
        }, function(){  
            $(this).parent().find("ul.subnav").slideUp('slow'); //When the mouse hovers out of the subnav, move it back up
        });

        //Following events are applied to the trigger (Hover events for the trigger)
        }).hover(function() { 
            $(this).addClass("subhover"); //On hover over, add class "subhover"
        }, function(){  //On Hover Out
            $(this).removeClass("subhover"); //On hover out, remove class "subhover"
    });

});
```

# JQuery Animated Menu
```
$(document).ready(function(){
      // Get the ID of the body
      var parentID = $("body").attr("id");
      // Loop through the nav list items
      $("#nav li").each(function() {
        // compare IDs of the body and list-items
        var myID = $(this).attr("id");
        // only perform the change on hover if the IDs don't match (so the active link doesn't change on hover)
        if (myID != "n-" + parentID) {
          // for mouse actions
          $(this).children("a").hover(function() {
            // add a class to the list item so that additional styling can be applied to the <em> and the text
            $(this).addClass('over');
              // add in the span that will be faded in and out
                        $(this).append("<span><\/span>");
            $(this).find("span").fadeIn(400);
          }, function() {
            $(this).removeClass('over');
                        // fade out the span then remove it completely to prevent the animations from continuing to run if you move over different items quickly
            $(this).find("span").fadeOut(400, function() {
                      $(this).remove();
                        });
          });
          // for keyboard actions
          $(this).children("a").focus(function() {
                        //check whether the link is already being hovered over before applying the class and extra span
                        //required for Firefox which makes the link unclickable if there's two spans layered on top of the anchor
                        if ($(this).attr('class')!='over') {
                            $(this).addClass('over');
                            $(this).append("<span><\/span>");
                            $(this).find("span").fadeIn(400);
                        }
          });
          $(this).children("a").blur(function() {
                        $(this).removeClass('over');
                        $(this).find("span").fadeOut(400, function() {
                            $(this).remove();
                        });
          });
        }
      });
    });
```

# CSS Sprites

```
$(document).ready(function(){
    
        // remove link background images since we're re-doing the hover interaction below 
        // (doing it this way retains the CSS default hover states for non-javascript-enabled browsers)
        // we also want to only remove the image on non-selected nav items, so this is a bit more complicated
        $(".nav").children("li").each(function() {
            var current = "nav current-" + ($(this).attr("class"));
            var parentClass = $(".nav").attr("class");
            if (parentClass != current) {
                $(this).children("a").css({backgroundImage:"none"});
            }
        }); 


        // create events for each nav item
        attachNavEvents(".nav", "home");
        attachNavEvents(".nav", "about");
        attachNavEvents(".nav", "services");
        attachNavEvents(".nav", "contact");
    

        function attachNavEvents(parent, myClass) {
            $(parent + " ." + myClass).mouseover(function() {
                $(this).append('<div class="nav-' + myClass + '"></div>');
                $("div.nav-" + myClass).css({display:"none"}).fadeIn(200);
            }).mouseout(function() {
                $("div.nav-" + myClass).fadeOut(200, function() {
                    $(this).remove();
                });
            }).mousedown(function() {
                $("div.nav-" + myClass).attr("class", "nav-" + myClass + "-click");
            }).mouseup(function() {
                $("div.nav-" + myClass + "-click").attr("class", "nav-" + myClass);
            });
        }



    });
```