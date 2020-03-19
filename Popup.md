# Popup

#### HTML:
``` html
<!--
	HTML, CSS & JQuery based Popup
	V1 22-1-2020
	Tested in Spotfire 10.6.1 app & webplayer
	David-van.Dorsten@klm.com
//-->
<p><a onclick="activatePopup('#Popup1','open');" style="cursor:pointer;">Popup 1</a></p>

<p><a onclick="activatePopup('#Popup2','open');" style="cursor:pointer;">Popup 2</a></p>
```
Link calls function activatePopup() that accepts 2 arguments.
Argument 1: Div name which one to open.
Argument 2: Action 'open' or 'close'

``` html
<!-- Overlay to darken background. -->
<div class='overlay'></div>

<!-- 3 Popup examples -->
<div id='Popup1' class="popup" style="visibility:hidden;opacity:0;transition:all 500ms;">
	
	<!-- Close button -->
	<a class="close" onclick="activatePopup('#Popup1','close');" style="cursor:pointer;">&times;</a>
	<h1>Title Popup 1</h1>
	<p>body...</p>

</div>

<div id='Popup2' class="popup" style="visibility:hidden;opacity:0;transition:all 500ms;">
	
	<!-- Close button -->
	<a class="close" onclick="activatePopup('#Popup2','close');" style="cursor:pointer;">&times;</a>
	<h1>Title Popup 2</h1>
	<p>body...</p>

</div>
```
1 Overlay container is needed for the darkening effect when popup is opened.
Div for popups has a style tag with necessary CSS for initial hidden state


#### CSS:
``` css
<style>
.overlay {
  position: fixed;
  top: 0;
  right: 0;
  left: 0;
  bottom: 0;
  opacity: 0.3;
  background: rgba(0, 0, 0, 0);
  transition: all 500ms;
  visibility: hidden;
  z-index: 1;
}
.popup {
  position: fixed;
  top: 10%;
  left: 50%;
  width: 20%;
  margin-left: -10%; /*Should be halve the width*/
  padding: 20px;
  heigth: auto;
  border-radius: 10px;
  background-color: #fff;
  z-index: 200;
}
.popup .close {
  position: absolute;
  top: 20px;
  right: 30px;
  transition: all 100ms;
  font-size: 30px;
  font-weight: bold;
  text-decoration: none;
  color: #333;
}
.popup .close:hover {
  color: #06D85F;
}
</style>
```

#### JQuery:
``` javascript
<script>
/*
	Function activateSidebar has 2 states:
	'open' or 'close'
	Edits CSS transform
*/
function activatePopup(id,action) {

  switch(id,action) {
    case action = 'open':
    $(".overlay").css({background: 'rgba(0, 0, 0, 0.6)'})
    $(".overlay").css({visibility: 'visible'})
    $(id).css({visibility: 'visible'})
    $(id).css({opacity: '1'})
    break;

    case action = 'close':
    $(".overlay").css({background: 'rgba(0, 0, 0, 0)'})
    $(".overlay").css({visibility: 'hidden'})
    $(id).css({visibility: 'hidden'})
    $(id).css({opacity: '0'})
    break;
  }
}
</script>
```
