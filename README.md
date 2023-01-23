<html>
    <head>
<script type="text/javascript">
// <![CDATA[
var colour="random"; // in addition to "random" can be set to any valid colour eg "#f0f" or "red"
var sparkles=50;


var x=ox=400;
var y=oy=300;
var swide=800;
var shigh=600;
var sleft=sdown=0;
var tiny=new Array();
var star=new Array();
var starv=new Array();
var starx=new Array();
var stary=new Array();
var tinyx=new Array();
var tinyy=new Array();
var tinyv=new Array();
 <!-- SCROLLBAR -->
<style type="text/css">
 
/* width */
::-webkit-scrollbar {
  width: 5px;
}
 
/* Track */
::-webkit-scrollbar-track {
  background: transparent; 
}
 
/* Handle */
::-webkit-scrollbar-thumb {
  background: transparent; 
}
 
 
/* Handle on hover */
::-webkit-scrollbar-thumb:hover {
  background: transparent; 
}
 
window.onload=function() { if (document.getElementById) {
  var i, rats, rlef, rdow;
  for (var i=0; i<sparkles; i++) {
    var rats=createDiv(3, 3);
    rats.style.visibility="hidden";
    rats.style.zIndex="999";
    document.body.appendChild(tiny[i]=rats);
    starv[i]=0;
    tinyv[i]=0;
    var rats=createDiv(5, 5);
    rats.style.backgroundColor="transparent";
    rats.style.visibility="hidden";
    rats.style.zIndex="999";
    var rlef=createDiv(1, 5);
    var rdow=createDiv(5, 1);
    rats.appendChild(rlef);
    rats.appendChild(rdow);
    rlef.style.top="2px";
    rlef.style.left="0px";
    rdow.style.top="0px";
    rdow.style.left="2px";
    document.body.appendChild(star[i]=rats);
  }
  set_width();
  sparkle();
}}

function sparkle() {
  var c;
  if (Math.abs(x-ox)>1 || Math.abs(y-oy)>1) {
    ox=x;
    oy=y;
    for (c=0; c<sparkles; c++) if (!starv[c]) {
      star[c].style.left=(starx[c]=x)+"px";
      star[c].style.top=(stary[c]=y+1)+"px";
      star[c].style.clip="rect(0px, 5px, 5px, 0px)";
      star[c].childNodes[0].style.backgroundColor=star[c].childNodes[1].style.backgroundColor=(colour=="random")?newColour():colour;
      star[c].style.visibility="visible";
      starv[c]=50;
      break;
    }
  }
  for (c=0; c<sparkles; c++) {
    if (starv[c]) update_star(c);
    if (tinyv[c]) update_tiny(c);
  }
  setTimeout("sparkle()", 40);
}

function update_star(i) {
  if (--starv[i]==25) star[i].style.clip="rect(1px, 4px, 4px, 1px)";
  if (starv[i]) {
    stary[i]+=1+Math.random()*3;
    starx[i]+=(i%5-2)/5;
    if (stary[i]<shigh+sdown) {
      star[i].style.top=stary[i]+"px";
      star[i].style.left=starx[i]+"px";
    }
    else {
      star[i].style.visibility="hidden";
      starv[i]=0;
      return;
    }
  }
  else {
    tinyv[i]=50;
    tiny[i].style.top=(tinyy[i]=stary[i])+"px";
    tiny[i].style.left=(tinyx[i]=starx[i])+"px";
    tiny[i].style.width="2px";
    tiny[i].style.height="2px";
    tiny[i].style.backgroundColor=star[i].childNodes[0].style.backgroundColor;
    star[i].style.visibility="hidden";
    tiny[i].style.visibility="visible"
  }
}

function update_tiny(i) {
  if (--tinyv[i]==25) {
    tiny[i].style.width="1px";
    tiny[i].style.height="1px";
  }
  if (tinyv[i]) {
    tinyy[i]+=1+Math.random()*3;
    tinyx[i]+=(i%5-2)/5;
    if (tinyy[i]<shigh+sdown) {
      tiny[i].style.top=tinyy[i]+"px";
      tiny[i].style.left=tinyx[i]+"px";
    }
    else {
      tiny[i].style.visibility="hidden";
      tinyv[i]=0;
      return;
    }
  }
  else tiny[i].style.visibility="hidden";
}

document.onmousemove=mouse;
function mouse(e) {
  if (e) {
    y=e.pageY;
    x=e.pageX;
  }
  else {
    set_scroll();
    y=event.y+sdown;
    x=event.x+sleft;
  }
}

window.onscroll=set_scroll;
function set_scroll() {
  if (typeof(self.pageYOffset)=='number') {
    sdown=self.pageYOffset;
    sleft=self.pageXOffset;
  }
  else if (document.body && (document.body.scrollTop || document.body.scrollLeft)) {
    sdown=document.body.scrollTop;
    sleft=document.body.scrollLeft;
  }
  else if (document.documentElement && (document.documentElement.scrollTop || document.documentElement.scrollLeft)) {
    sleft=document.documentElement.scrollLeft;
    sdown=document.documentElement.scrollTop;
  }
  else {
    sdown=0;
    sleft=0;
  }
}

window.onresize=set_width;
function set_width() {
  var sw_min=999999;
  var sh_min=999999;
  if (document.documentElement && document.documentElement.clientWidth) {
    if (document.documentElement.clientWidth>0) sw_min=document.documentElement.clientWidth;
    if (document.documentElement.clientHeight>0) sh_min=document.documentElement.clientHeight;
  }
  if (typeof(self.innerWidth)=='number' && self.innerWidth) {
    if (self.innerWidth>0 && self.innerWidth<sw_min) sw_min=self.innerWidth;
    if (self.innerHeight>0 && self.innerHeight<sh_min) sh_min=self.innerHeight;
  }
  if (document.body.clientWidth) {
    if (document.body.clientWidth>0 && document.body.clientWidth<sw_min) sw_min=document.body.clientWidth;
    if (document.body.clientHeight>0 && document.body.clientHeight<sh_min) sh_min=document.body.clientHeight;
  }
  if (sw_min==999999 || sh_min==999999) {
    sw_min=800;
    sh_min=600;
  }
  swide=sw_min;
  shigh=sh_min;
}

function createDiv(height, width) {
  var div=document.createElement("div");
  div.style.position="absolute";
  div.style.height=height+"px";
  div.style.width=width+"px";
  div.style.overflow="hidden";
  return (div);
}

function newColour() {
  var c=new Array();
  c[0]=255;
  c[1]=Math.floor(Math.random()*256);
  c[2]=Math.floor(Math.random()*(256-c[1]/2));
  c.sort(function(){return (0.5 - Math.random());});
  return ("rgb("+c[0]+", "+c[1]+", "+c[2]+")");
}
// ]]>
</script>
 
                                <!-- MOUSE SCRIPT -->
 
<script type="text/javascript">
// <![CDATA[
var colour="#e8e3cc";
var sparkles=120;
 
/****************************
*  Tinkerbell Magic Sparkle *
* (c) 2005 mf2fm web-design *
*  http://www.mf2fm.com/rv  *
* DON'T EDIT BELOW THIS BOX *
****************************/
var x=ox=400;
var y=oy=300;
var swide=800;
var shigh=600;
var sleft=sdown=0;
var tiny=new Array();
var star=new Array();
var starv=new Array();
var starx=new Array();
var stary=new Array();
var tinyx=new Array();
var tinyy=new Array();
var tinyv=new Array();
 
window.onload=function() { if (document.getElementById) {
  var i, rats, rlef, rdow;
  for (var i=0; i<sparkles; i++) {
    var rats=createDiv(3, 3);
    rats.style.visibility="hidden";
    document.body.appendChild(tiny[i]=rats);
    starv[i]=0;
    tinyv[i]=0;
    var rats=createDiv(5, 5);
    rats.style.backgroundColor="transparent";
    rats.style.visibility="hidden";
    var rlef=createDiv(1, 5);
    var rdow=createDiv(5, 1);
    rats.appendChild(rlef);
    rats.appendChild(rdow);
    rlef.style.top="2px";
    rlef.style.left="0px";
    rdow.style.top="0px";
    rdow.style.left="2px";
    document.body.appendChild(star[i]=rats);
  }
  set_width();
  sparkle();
}}
 
function sparkle() {
  var c;
  if (x!=ox || y!=oy) {
    ox=x;
    oy=y;
    for (c=0; c<sparkles; c++) if (!starv[c]) {
      star[c].style.left=(starx[c]=x)+"px";
      star[c].style.top=(stary[c]=y)+"px";
      star[c].style.clip="rect(0px, 5px, 5px, 0px)";
      star[c].style.visibility="visible";
      starv[c]=50;
      break;
    }
  }
  for (c=0; c<sparkles; c++) {
    if (starv[c]) update_star(c);
    if (tinyv[c]) update_tiny(c);
  }
  setTimeout("sparkle()", 40);
}
 
function update_star(i) {
  if (--starv[i]==25) star[i].style.clip="rect(1px, 4px, 4px, 1px)";
  if (starv[i]) {
    stary[i]+=1+Math.random()*3;
    if (stary[i]<shigh+sdown) {
      star[i].style.top=stary[i]+"px";
      starx[i]+=(i%5-2)/5;
      star[i].style.left=starx[i]+"px";
    }
    else {
      star[i].style.visibility="hidden";
      starv[i]=0;
      return;
    }
  }
  else {
    tinyv[i]=50;
    tiny[i].style.top=(tinyy[i]=stary[i])+"px";
    tiny[i].style.left=(tinyx[i]=starx[i])+"px";
    tiny[i].style.width="2px";
    tiny[i].style.height="2px";
    star[i].style.visibility="hidden";
    tiny[i].style.visibility="visible"
  }
}
 
function update_tiny(i) {
  if (--tinyv[i]==25) {
    tiny[i].style.width="1px";
    tiny[i].style.height="1px";
  }
  if (tinyv[i]) {
    tinyy[i]+=1+Math.random()*3;
    if (tinyy[i]<shigh+sdown) {
      tiny[i].style.top=tinyy[i]+"px";
      tinyx[i]+=(i%5-2)/5;
      tiny[i].style.left=tinyx[i]+"px";
    }
    else {
      tiny[i].style.visibility="hidden";
      tinyv[i]=0;
      return;
    }
  }
  else tiny[i].style.visibility="hidden";
}
 
document.onmousemove=mouse;
function mouse(e) {
  set_scroll();
  y=(e)?e.pageY:event.y+sdown;
  x=(e)?e.pageX:event.x+sleft;
}
 
function set_scroll() {
  if (typeof(self.pageYOffset)=="number") {
    sdown=self.pageYOffset;
    sleft=self.pageXOffset;
  }
  else if (document.body.scrollTop || document.body.scrollLeft) {
    sdown=document.body.scrollTop;
    sleft=document.body.scrollLeft;
  }
  else if (document.documentElement && (document.documentElement.scrollTop || document.documentElement.scrollLeft)) {
    sleft=document.documentElement.scrollLeft;
	sdown=document.documentElement.scrollTop;
  }
  else {
    sdown=0;
    sleft=0;
  }
}
 
window.onresize=set_width;
function set_width() {
  if (typeof(self.innerWidth)=="number") {
    swide=self.innerWidth;
    shigh=self.innerHeight;
  }
  else if (document.documentElement && document.documentElement.clientWidth) {
    swide=document.documentElement.clientWidth;
    shigh=document.documentElement.clientHeight;
  }
  else if (document.body.clientWidth) {
    swide=document.body.clientWidth;
    shigh=document.body.clientHeight;
  }
}
 
function createDiv(height, width) {
  var div=document.createElement("div");
  div.style.position="absolute";
  div.style.height=height+"px";
  div.style.width=width+"px";
  div.style.overflow="hidden";
  div.style.backgroundColor=colour;
  return (div);
}
// ]]>
</script>
 
        <!--  POPUP SCRIPT! -->
 
        <script type="text/javascript"
src="https://ajax.googleapis.com/ajax/libs/jquery/1.4.1/jquery.min.js"></script>
<script>
$(document).ready(function() {
//
$('a.poplight[href^=#]').click(function() {
var popID = $(this).attr('rel'); //Get Popup Name
var popURL = $(this).attr('href'); //Get Popup href to define size
var query= popURL.split('?');
var dim= query[1].split('&');
var popWidth = dim[0].split('=')[1]; //Gets the first query string value
$('#' + popID).fadeIn().css({ 'width': Number( popWidth ) }).prepend('<a href="#" class="close"></a>');
var popMargTop = ($('#' + popID).height() + 80) / 2;
var popMargLeft = ($('#' + popID).width() + 80) / 2;
//Apply Margin to Popup
$('#' + popID).css({
'margin-top' : -popMargTop,
'margin-left' : -popMargLeft
});
$('body').append('<div id="fade"></div>');
$('#fade').css({'filter' : 'alpha(opacity=80)'}).fadeIn(); //Fade in the fade layer - .css({'filter' : 'alpha(opacity=80)'})
return false;
});
$('a.close, #fade').live('click', function() {
$('#fade , .popup_block').fadeOut(function() {
$('#fade, a.close').remove(); //fade them both out
});
return false;
});
});
</script>
 
 
                                <!-- META -->
        <meta name="color:text" content="#fff" />
        <meta name="color:Link" content="#fff" />
        <meta name="color:Zelda" content="#000" />
        <meta name="color:Italy" content="#fff" />
        <meta name="color:Belgium" content="#fff" />
 
 
                                <!-- FONTS -->
<link href="https://fonts.googleapis.com/css?family=Shadows+Into+Light" rel="stylesheet">
<link href="https://fonts.googleapis.com/css?family=Sacramento" rel="stylesheet">
<link href="https://fonts.googleapis.com/css?family=Yellowtail" rel="stylesheet">
 
<!DOCTYPE html>
<html>
  <head>
    <title>My Space Website</title>
  </head>
  <body>
    <header>
      <h1>Welcome to My Space Website</h1>
    </header>
    <nav>
      <ul>
        <li><a href="#solar-system">Solar System</a></li>
        <li><a href="#space-exploration">Space Exploration</a></li>
        <li><a href="#news-and-discoveries">News and Discoveries</a></li>
        <li><a href="#resources">Resources</a></li>
      </ul>
    </nav>
    <main>
      <section id="solar-system">
        <h2>Solar System</h2>
        <p>poop about the solar system and the planets that are in it</p>
      </section>
      <section id="space-exploration">
        <h2>Space Exploration</h2>
        <p>Information about the history of space exploration, including notable missions and spacecraft</p>
      </section>
      <section id="news-and-discoveries">
        <h2>News and Discoveries</h2>
        <p>The latest news and discoveries from space, such as new exoplanets, or updates from current missions</p>
      </section>
      <section id="resources">
        <h2>Resources</h2>
        <p>Links and resources for people who are interested in learning more about space and astronomy</p>
      </section>
    </main>
    <footer>
      <p>Copyright © My Space Website</p>
    </footer>
  </body>
</html>

 
 
    </head>
                            <!-- SCROLLBAR -->
<style type="text/css">
 
/* width */
::-webkit-scrollbar {
  width: 5px;
}
 
/* Track */
::-webkit-scrollbar-track {
  background: transparent; 
}
 
/* Handle */
::-webkit-scrollbar-thumb {
  background: transparent; 
}
 
 
/* Handle on hover */
::-webkit-scrollbar-thumb:hover {
  background: transparent; 
}
 
 
                                /* BODY AND HEAD */
 
body {
    background:#641387;    
    color:{color:text};
    font-family:'calibri';
    text-align:justify;
    background-image:url('https://static.tumblr.com/hgwpeok/PXFpnfvv0/bg.png');
    background-position: bottom left;
    background-repeat: no-repeat;
    background-attachment: fixed;
}
 
 
#heads {
    position:fixed;
    bottom:120px;
    left:115px;
    width:100px;
    padding:10px;
    text-align:center;
    overflow:hidden;
 
}
 
#heads a {
    color:black;
    font-size:45px;
    line-height:40px;
}
 
#heads a:hover {
    color:white;
    text-shadow:1px 1px 1px #000,
                -1px -1px 1px red,
                -1px 1px 1px #000,
                1px -1px 1px red;
}
 
#tails {
    background:transparent;
    color:#fff;
    position:fixed;
    bottom:30px;
    left:30px;
    height:115px;
    width:300px;
    font-size:12px;
    text-align:left;
    line-height:12px;
    overflow:auto;
    -webkit-transition: all 0.9s ease;
    -moz-transition: all 0.9s ease;
    -o-transition: all 0.9s ease;
}
 
#tails a {
    color:{color:Belgium};
}
 
#tails i {
    font-size:15px;
    text-shadow:1px 0px 0px #000;
}
 
 
 
                                /* NAVI */
.navi_one {
    position:fixed;
    font-size:105px;
    bottom:497px;
    left:485px;
    text-shadow:1px 1px 1px #000,
                -1px -1px 1px #000,
                -1px 1px 1px #000,
                1px -1px 1px #000;
}
 
.navi_one a {
    padding: 1px 3px;
    margin:5px;
    text-align:center;
    color:#fff;
    -webkit-transition: all 0.9s ease;
    -moz-transition: all 0.9s ease;
    -o-transition: all 0.9s ease;
 
}
 
.navi_one a:hover {
    opacity:0.3;
    -webkit-transition: all 0.9s ease;
    -moz-transition: all 0.9s ease;
    -o-transition: all 0.9s ease;
}
 
 
 
 
.navi_two {
    position:fixed;
    font-size:55px;
    bottom:520px;
    left:406px;
    text-shadow:1px 1px 1px #000,
                -1px -1px 1px #000,
                -1px 1px 1px #000,
                1px -1px 1px #000;
}
 
.navi_two a {
    padding: 1px 3px;
    margin:5px;
    text-align:center;
    color:#fff;
    -webkit-transition: all 0.9s ease;
    -moz-transition: all 0.9s ease;
    -o-transition: all 0.9s ease;
 
}
 
.navi_two a:hover {
    opacity:0.3;
    -webkit-transition: all 0.9s ease;
    -moz-transition: all 0.9s ease;
    -o-transition: all 0.9s ease;
}
 
 
 
.navi_three {
    position:fixed;
    font-size:55px;
    bottom:520px;
    left:555px;
    text-shadow:1px 1px 1px #000,
                -1px -1px 1px #000,
                -1px 1px 1px #000,
                1px -1px 1px #000;
}
 
.navi_three a {
    padding: 1px 3px;
    margin:5px;
    text-align:center;
    color:#fff;
    -webkit-transition: all 0.9s ease;
    -moz-transition: all 0.9s ease;
    -o-transition: all 0.9s ease;
 
}
 
.navi_three a:hover {
    opacity:0.3;
    -webkit-transition: all 0.9s ease;
    -moz-transition: all 0.9s ease;
    -o-transition: all 0.9s ease;
}
 
 
.navi_four {
    position:fixed;
    font-size:25px;
    bottom:528px;
    left:355px;
    text-shadow:1px 1px 1px #000,
                -1px -1px 1px #000,
                -1px 1px 1px #000,
                1px -1px 1px #000;
}
 
.navi_four a {
    padding: 1px 3px;
    margin:5px;
    text-align:center;
    color:#fff;
    -webkit-transition: all 0.9s ease;
    -moz-transition: all 0.9s ease;
    -o-transition: all 0.9s ease;
 
}
 
.navi_four a:hover {
    opacity:0.3;
    -webkit-transition: all 0.9s ease;
    -moz-transition: all 0.9s ease;
    -o-transition: all 0.9s ease;
}
 
 
.navi_five {
    position:fixed;
    font-size:25px;
    bottom:528px;
    left:634px;
    text-shadow:1px 1px 1px #000,
                -1px -1px 1px #000,
                -1px 1px 1px #000,
                1px -1px 1px #000;
}
 
.navi_five a {
    padding: 1px 3px;
    margin:5px;
    text-align:center;
    color:#fff;
    -webkit-transition: all 0.9s ease;
    -moz-transition: all 0.9s ease;
    -o-transition: all 0.9s ease;
 
}
 
.navi_five a:hover {
    opacity:0.3;
    -webkit-transition: all 0.9s ease;
    -moz-transition: all 0.9s ease;
    -o-transition: all 0.9s ease;
}
 
                                /* POSTS */
 
.peekaboo img {
    width:300px;
    height:auto;
}
 
                                /* NOTES */
{block:PermalinkPage} 
 
.whathappened {
    width:300px;
    padding:5px;
    margin-bottom:30px;
    font-size:12px;
    text-align:block;
    letter-spacing:3px;
}
 
.whathappened img {
    border-radius:100%;
    margin:-5px 5px;
}
 
{/block:PermalinkPage}
 
.credit {
position:fixed;
bottom:4px;
right:4px;
font-size:20px;
}
 
                                /* MISC HTML */
ol {
  padding: 0px 30px;
}
 
ol li {
  margin: 5px;
}
 
ul {
  padding: 0px 30px;
}
 
ul li {
  margin: 5px;
}
 
a {
    color:{color:link};
    text-decoration: none;
    -webkit-transition: all 0.9s ease;
    -moz-transition: all 0.9s ease;
    -o-transition: all 0.9s ease;
}    
 
a:hover {
    color:{color:zelda};
    text-shadow:1px 1px 1px #000,
                -1px -1px 1px #000,
                -1px 1px 1px #000,
                1px -1px 1px #000;
    -webkit-transition: all 0.9s ease;
    -moz-transition: all 0.9s ease;
    -o-transition: all 0.9s ease;
}
 
i, em {
    color:{color:italy};
    font-family:'Shadows Into Light';
}
 
b, strong {
    color:{color:belgium};
}
 

big {
    color:#555;   
    text-shadow:0px 1px 1px #000;
}
 
h1 {
   font-size:30px;
   line-height:10px;
   text-align:left;
   padding:10px;
   font-family: 'Yellowtail', cursive;
}
 
h2 {
    font-size:18px;
    line-height:10px;
    font-family: 'Yellowtail', cursive;
}
 
h3 {
    font-size:14px;
    text-align:center;
    padding:3px;
    border:2px solid black;
    background:url('https://66.media.tumblr.com/1fa029b8611ee8ec725f694cb2817f07/tumblr_pabrf1CylX1xp1j77o1_500.gif');
    font-family:'Shadows Into Light';
}
 
hr {
    height:2px;
    border:2px solid black;
    background:url('https://66.media.tumblr.com/1fa029b8611ee8ec725f694cb2817f07/tumblr_pabrf1CylX1xp1j77o1_500.gif');
}
                                /* PERMALINKS */
 
.permalinks { 
   text-align:center;
   font-size:12px;
   letter-spacing:2px;
}
 
.permalinks a { 
    color:{color:link};
    text-decoration: none;
    -webkit-transition: all 0.9s ease;
    -moz-transition: all 0.9s ease;
    -o-transition: all 0.9s ease;
}
 
.permalinks a:hover { 
    color:{color:zelda};
    -webkit-transition: all 0.9s ease;
    -moz-transition: all 0.9s ease;
    -o-transition: all 0.9s ease;    
}
 
 
.tags { 
    text-align:center;
}
 
.tags a { 
    text-decoration:none;
    font-size: 8px;
    color:#fff;
    -webkit-transition: all 0.9s ease;
    -moz-transition: all 0.9s ease;
    -o-transition: all 0.9s ease;
}
 
.tags a:hover { 
    color:#000;
    -webkit-transition: all 0.9s ease;
    -moz-transition: all 0.9s ease;
    -o-transition: all 0.9s ease;
}
 
.stats {
    text-align:center;
    font-size:10px;
}
 
.stats a {
    color:{color:link};
    display:inline;
    margin:5px;
    font-size:18px;
    text-decoration:none;
    -webkit-transition: all 0.9s ease;
    -moz-transition: all 0.9s ease;
    -o-transition: all 0.9s ease;
 
}
 
.stats a:hover {
    color:{color:zelda};
    -webkit-transition: all 0.9s ease;
    -moz-transition: all 0.9s ease;
    -o-transition: all 0.9s ease;
}
 
 
.goon {
    position:fixed;
    bottom:180px;
    left:241px;
 
}
 
.goon img {
    height:100px;
    width:100px;
}
 
.goon img:hover {
    opacity:0.3;
    -webkit-transition: all 0.9s ease;
    -moz-transition: all 0.9s ease;
    -o-transition: all 0.9s ease;
}
 
.gooff {
    position:fixed;
    bottom:180px;
    left:10px;
}
 
.gooff img {
    height:100px;
    width:100px;
}
 
.gooff img:hover {
    opacity:0.3;
    -webkit-transition: all 0.9s ease;
    -moz-transition: all 0.9s ease;
    -o-transition: all 0.9s ease;
}
 
                                /* ASKS */
.fus { /*Asker*/
    font-size:25px;
    font-style:italic;
    text-align:center;
    color:#fff;
    margin-bottom:0px;
    background-image:url('https://66.media.tumblr.com/1fa029b8611ee8ec725f694cb2817f07/tumblr_pabrf1CylX1xp1j77o1_500.gif');
}
.ro { /*Question*/
    padding:10px 25px;
    text-align:justify;
    color:#000;
    background:transparent;
    border-bottom: 2px solid black;
}
 
.dah { /*Answer*/
    padding-left:10px;
    padding-right:10px;
}
 
.dah blockquote{ /*Answer*/
    margin:0px;
    padding:0px;
    border-left:0px solid black;
}
 
 
                               /* QUOTES */
.tobe {
    font-size:30px;
    letter-spacing:1px;
    text-align:center;
    font-family: 'Sacramento', cursive;
    margin-bottom:5px;
    padding-bottom:3px;
    border-bottom:2px solid black;
}
 
.ornottobe {
   font-size:10px;
   letter-spacing:1px;
   text-align:center;
   margin-bottom:5px;
}
                                /* POPPY UPPY */
.popup_block {
    display:none;
    height:400px;
    overflow:auto;
    background:#81464f;
    background:url('https://static.tumblr.com/hgwpeok/r9kpnfvv2/popup.png');
    padding:20px;
    padding-left:260px;
    float:left;
    position:fixed;
    top:50%;left:50%;
    z-index: 99999;
    -webkit-box-shadow: 0px 0px 20px #000; /* delete for solid white */
    -moz-box-shadow: 0px 0px 20px #000; /* delete for solid white */
    box-shadow: 0px 0px 20px #000; /* delete for solid white */
}
 
.popup_block img {
    float:right;
    opacity:1;
    -webkit-transition: all 0.9s ease;
    -moz-transition: all 0.9s ease;
    -o-transition: all 0.9s ease;
}
 
.popup_block a img:hover {
    opacity:0.3;
    -webkit-transition: all 0.9s ease;
    -moz-transition: all 0.9s ease;
    -o-transition: all 0.9s ease;
}
 
*html #fade {position: absolute;}
*html .popup_block {position: absolute;}
#fade {
    display:none;
    position:fixed;
    left:0px;
    top:0px;
    width:100%;
    height:100%;
    z-index:9999;
    background:#000; /* change to #fff for solid white */
    opacity:0.5; /* change to opacity:1; */
}
 
 
.navigator {
    text-align:center;
    padding:5px;
}
 
.navigator a {
    display:inline-block;
    width:100px;
    height:10px;
    line-height:10px;
    margin:2px;
    padding:8px;
    text-align:center;
    background:transparent;
    background-image:url('https://66.media.tumblr.com/1fa029b8611ee8ec725f694cb2817f07/tumblr_pabrf1CylX1xp1j77o1_500.gif');
    border:double 7px #a3a5a9; /* BORDER COLOR */
    font-size:12px;
    color:#fff;
    opacity:1;
    text-transform:uppercase;
    text-shadow:1px 1px 0px #000, /* TEXT SHADOW */
      1px -1px 0px #000,
      -1px -1px 0px #000,
      -1px 1px 0px #000,
      0px 1px 0px #000,
      0px -1px 0px #000,
      1px 0px 0px #000,
      -1px 0px 0px #000;
    -webkit-transition: all 0.9s ease;
    -moz-transition: all 0.9s ease;
    -o-transition: all 0.9s ease;
}
 
.navigator a:hover {
    opacity:0.3;
    -webkit-transition: all 0.9s ease;
    -moz-transition: all 0.9s ease;
    -o-transition: all 0.9s ease;
}
                                /* END */
 
</style>

 

 

 
 
 
   
 
 
<!– {SOURCEURL}{BLOCK:SOURCELOGO}<IMG SRC="{BLACKLOGOURL}"
WIDTH="{LOGOWIDTH}" HEIGHT="{LOGOHEIGHT}" ALT="{SOURCETITLE}" />
 
                       
 
                            <!-- POP UPS -->
 
<div id="ask" class="popup_block">
 

 
</div>
 
<div id="rules" class="popup_block">
<h1>Guidelines</h1>
<hr>
 
Rules here
 
</div>
 
 
<h3>Relationships</h3>
<img src="https://static.tumblr.com/hgwpeok/BtNpnfvv2/icon.png"/><a 
 
 
</div>
 
 



 
</div>
 
 
</div></div></div></div></div></div></div></div></div></div>
 
</html>

<!-- END OF HTML! -->


# cosmos
TSA
testing if this works
