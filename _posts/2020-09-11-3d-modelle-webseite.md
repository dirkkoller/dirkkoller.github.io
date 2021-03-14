---
layout: default
title:  "3D-Modelle auf der Webseite"
categories: 3D Photogrammetrie 
permalink: /3d-modell-webseite
---

Hochauflösende 3D-Modelle wie man sie mit Hilfe von Lascerscanning oder Photogrammetrie erzeugen kann werden schnell recht groß. Anders als ein "von Hand" (also zum Beispiel mit Blender) erzeugtes Modell besteht ein Gebäudemodell schnell aus Millionen von Flächen und ist viele Megabyte groß. Um solch ein riesiges 3d-Modell auf der Webseite trotzdem performant anzuzeigen, eignet sich der *3D Heritage Online Presenter*, kurz *3DHOP*. Das Javascript-Projekt wurde vom italienischen Istituto di Scienza e Tecnologie dell’Informazione “A. Faedo” entwickelt und bietet die Möglichkeit große Modelle auflösungsabhängig in mehrere kleinere Modelle aufzuteilen.

Der Viewer lädt dann selbständig während des Betrachtens die erforderlichen Teile nach. 3DHOP nutzt intern WebGL 2, das von Safari nicht unterstützt wird. Wer diese Seite also mit einem Apple-Gerät anzeigt sollte dies mit Chrome oder Firefox tun um die 3D-Präsentation auch zu sehen. 

Die Integration von 3DHOP erfolgt, indem zunächst die im Download im Verzeichnins *minimal* enthaltenen Ordner js, css und skins dem Webprojekt zugefügt werden. Anschließend sind die css- und js-Dateien im Head-Bereich des HTML-Codes einzubinden.

Ist das geschehen, wird der Viewer mit Hilfe eines div-Tags eingebunden. Diesen Bereich kann man anpassen. Es ist zum Beispiel möglich nur einen Teil der Stuerungselemente anzuzeigen oder den Hintergrund auszuwechseln. Details dazu finden sich auf der Webseite des Projekts.

Zu guter Letzt muss der Viewer mit Hilfe eines JavaScripts initialisiert werden. An dieser Stelle wird auch definiert, wo das anzuzeigende Modell zu finden ist.


<!--STYLESHEET-->
<link type="text/css" rel="stylesheet" href="3dhop/stylesheet/3dhop.css"/>  
<!--SPIDERGL-->
<script type="text/javascript" src="3dhop/js/spidergl.js"></script>
<!--JQUERY-->
<script type="text/javascript" src="3dhop/js/jquery.js"></script>
<!--PRESENTER-->
<script type="text/javascript" src="3dhop/js/presenter.js"></script>
<!--3D MODELS LOADING AND RENDERING-->
<script type="text/javascript" src="3dhop/js/nexus.js"></script>
<script type="text/javascript" src="3dhop/js/ply.js"></script>
<!--TRACKBALLS-->
<script type="text/javascript" src="3dhop/js/trackball_sphere.js"></script>
<script type="text/javascript" src="3dhop/js/trackball_turntable.js"></script>
<script type="text/javascript" src="3dhop/js/trackball_turntable_pan.js"></script>
<script type="text/javascript" src="3dhop/js/trackball_pantilt.js"></script>
<!--UTILITY-->
<script type="text/javascript" src="3dhop/js/init.js"></script>


<div id="3dhop" class="tdhop" onmousedown="if (event.preventDefault) event.preventDefault()"><div id="tdhlg"></div>
 <div id="toolbar">
  <img id="home"       title="Home"                  src="3dhop/skins/dark/home.png"         /><br/> 
  <img id="zoomin"     title="Zoom In"               src="3dhop/skins/dark/zoomin.png"       /><br/>
  <img id="zoomout"    title="Zoom Out"              src="3dhop/skins/dark/zoomout.png"      /><br/>
  <img id="light_on"   title="Disable Light Control" src="3dhop/skins/dark/lightcontrol_on.png" 
                                                          style="position:absolute; visibility:hidden;"/>
  <img id="light"      title="Enable Light Control"  src="3dhop/skins/dark/lightcontrol.png" /><br/>
  <img id="full_on"    title="Exit Full Screen"      src="3dhop/skins/dark/full_on.png" 
                                                          style="position:absolute; visibility:hidden;"/>
  <img id="full"       title="Full Screen"           src="3dhop/skins/dark/full.png"         />
 </div>
 <canvas id="draw-canvas" style="background-image: url(3dhop/skins/backgrounds/dark.jpg)"/>
</div>

<script type="text/javascript">
var presenter = null;

function setup3dhop() { 
	presenter = new Presenter("draw-canvas");

	presenter.setScene({
		meshes: {
			"Gargoyle" : { 
				url: "3dhop/models/full.nxz",
				transform: { scale : [15, 15, 15]}
			}
		},
		modelInstances : {
			"Model2" : {
				mesh : "Gargoyle"
			}
		}
	});
}

function actionsToolbar(action) {
	if(action=='home') presenter.resetTrackball(); 
	else if(action=='zoomin') presenter.zoomIn();
	else if(action=='zoomout') presenter.zoomOut(); 
	else if(action=='light' || action=='light_on') { presenter.enableLightTrackball(!presenter.isLightTrackballEnabled()); lightSwitch(); } 
	else if(action=='full'  || action=='full_on') fullscreenSwitch(); 
}

$(document).ready(function(){
	init3dhop();

	setup3dhop();
});
</script>
