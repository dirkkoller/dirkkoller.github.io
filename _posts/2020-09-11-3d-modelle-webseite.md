---
layout: default
title:  "3D-Modelle auf der Webseite"
categories: 3D Photogrammetrie 
permalink: /3d-modell-webseite
---

<head>
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

</head>
<body>

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
</body>