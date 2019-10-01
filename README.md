<!DOCTYPE html>
<html>
<section class="webdesigntuts-workshop">
	
	<form action="https://www.google.com/search" method="GET">
	<input type="text" name="q" placeholder="Google Seach">
	<input type="submit" value="Google Search">
	</form>
	
</section>
	<p><b><font size = "5", color = "orange">PROGRAMACIÓN APLICADA A ENTORNO SIG</font></b>, <br><font size = 5, color = "red">GEOVISOR ELABORADO POR PABLO CÉSAR DÍAZ</font></br><br>CENTROS REGIONALES DE LA UNIVERSIDAD PEDAGÓGICA NACIONAL FRANCISCO MORAZÁN A NIVEL NACIONAL</br></p>
	
	<font face="Comic Sans MS">Maestría en Gestión y Ordenamiento Territorial MOGT-5/Universidad Nacional Autónoma de Honduras (UNAH)</font><br></br>
	
	
	<head>
		<meta charset="utf-8"/>
		<title>MI GEOVISOR_PABLO DÍAZ</title>
	
		<!--Leaflet-->
		<link rel="stylesheet" href="https://unpkg.com/leaflet@1.5.1/dist/leaflet.css"
		integrity="sha512-xwE/Az9zrjBIphAcBb3F6JVqxf46+CDLwfLMHloNu6KEQCAWi6HcDUbeOfBIptF7tcCzusKFjFw2yuvEpDL9wQ=="
		crossorigin=""/>
  
		<script src="https://unpkg.com/leaflet@1.5.1/dist/leaflet.js"
		integrity="sha512-GffPMF3RvMeYyc1LWMHtK8EbPv0iNZ8/oTtHPx9/cc2ILxQ+u905qIwdpULaqDkyBKgOaB57QTMg7ztg8Jm2Og=="
		crossorigin="">
  
		</script>
		
		<!--Comentario: Agregar ESRIMaps-->
		<script src="https://unpkg.com/esri-leaflet@2.3.0/dist/esri-leaflet.js"
		integrity="sha512-1tScwpjXwwnm6tTva0l0/ZgM3rYNbdyMj5q6RSQMbNX6EUMhYDE3pMRGZaT41zHEvLoWEK7qFEJmZDOoDMU7/Q=="
		crossorigin=""></script>
		
		<!--Plugins de Leaflet-->
		<!--MiniMap-->
		<link rel="stylesheet" href="Control.MiniMap.css" />
		<script src="Control.MiniMap.js" type= "text/javascript">
		</script>
	
		<!--Mouse Position-->
		<link rel="stylesheet" href="L.Control.MousePosition.css" />
		<script src="L.Control.MousePosition.js" type= "text/javascript">
		</script>
		
		<!--Full screen-->
		<link rel='stylesheet' href='leaflet.fullscreen.css'  />
		<script src='Leaflet.fullscreen.js'></script>
		
		<!--Map center-->
		<link rel="stylesheet" href="leaflet.viewcenter.css" />
		<script src="leaflet.viewcenter.js"></script>
	</head>
	
	<body>
		<div id="map" style="width: 1400px; height: 800px;"></div>
		<div class='space-bottom'></div>
        <div id='map' class='col12 row10'></div>
		
		<body background="paisajes-de-primavera-para-fondo-de-pantalla.jpg" bgcolor="#FF7F50">
		
		<marquee scrolldelay= "200" direction = "down" collamount= "10" height = "250px"><center>
		<img src = "https://upnfm.edu.hn/images/2018/05/28/dsc_0690.jpg"/>
		<img src = "https://upnfm.edu.hn/images/2018/03/15/59147420.jpg"/>
		<img src = "https://upnfm.edu.hn/images/2017/08/25/ceiba6.jpg"/>
		<img src = "https://upnfm.edu.hn/images/2018/03/15/vida-estudiantil-5-2.jpg"/>
		<img src = "https://upnfm.edu.hn/images/2018/03/15/sede-gracias.jpg"/>
		
		<script>
	
		var osm = L.tileLayer('https://api.tiles.mapbox.com/v4/{id}/{z}/{x}/{y}.png?access_token={accessToken}', 
		{attribution: 'Map data &copy; <a href="https://www.openstreetmap.org/">OpenStreetMap</a> contributors,<a href="https://creativecommons.org/licenses/by-sa/2.0/">CC-BY-SA</a>, Imagery © <a href="https://www.mapbox.com/">Mapbox</a>', 
		id: 'mapbox.streets', 
		accessToken:'pk.eyJ1IjoicGFibG9jZXNhciIsImEiOiJjazBweThxbmUwMDYyM2xvMjFrb2UwdG82In0.29K56YHY7YuBEHtr3VDdOA',
		maxZoom: 15,
		minZoom: 7,
		keyboard: true
		})
		
			
		var osm2 = L.tileLayer('https://api.tiles.mapbox.com/v4/{id}/{z}/{x}/{y}.png?access_token={accessToken}', 
		{attribution: 'Map data &copy; <a href="https://www.openstreetmap.org/">OpenStreetMap</a> contributors,<a href="https://creativecommons.org/licenses/by-sa/2.0/">CC-BY-SA</a>, Imagery © <a href="https://www.mapbox.com/">Mapbox</a>', 
		id: 'mapbox.satellite', 
		accessToken:'pk.eyJ1IjoicGFibG9jZXNhciIsImEiOiJjazBweThxbmUwMDYyM2xvMjFrb2UwdG82In0.29K56YHY7YuBEHtr3VDdOA',
		maxZoom: 12,
		minZoom: 5,
		keyboard: true
		
		});
		
		var mapa = L.map('map',{
		center: [13.934016, -87.294583],
		zoom:7,
		layers: osm,
		zoomControl: false,
		fullscreenControl: {pseudoFullscreen: false, position: 'topleft'
		},
		maxBounds: [[13.0,-89.5],[ 16.0, -83.0]]
		});
		
		<!--Comentario: marcadores de L.icon-->
		var icono1 = L.icon({
		iconUrl: 'icon1_parquesend.png',
		iconSize: [50, 70],
		});
		var marker1= L.marker([14.094217, -87.201347], {icon: icono1}).addTo(mapa);
		marker1.bindPopup("UPN TEGUCIGALPA.png");
		
		var hn = L.tileLayer.wms("http://localhost:8080/geoserver/MOGT/wms?service=WMS", {
		layers: "MOGT:Hidrografia_Nacional",
		format: 'image/png',
		transparent: true,
		version: '1.1.0',
		attribution: "Limites departamentales, SINIT - oficial"
		}).addTo(mapa);
		
		var hn = L.tileLayer.wms("http://localhost:8080/geoserver/Nacionales%20Sinit/wms", {
		layers: "Nacionales Sinit:departamentos_20c2001wgs84",
		format: 'image/png',
		transparent: true,
		version: '1.1.0',
		attribution: "Limites departamentales"
		}).addTo(mapa);
		
		var ESRI = L.esri.basemapLayer('Topographic');
		
	var ESRI_topo = L.esri.basemapLayer('ShadedRelief');
	
	var ESRI_2 = L.esri.basemapLayer('Terrain');
		
		
		var capasBase = {
		
			"Capa 1 OSM": osm,
			"Capa 2 OSM2": osm2,
			"Capa 3:Departamentos": hn,
			"Esri - Imagery": ESRI_2,
			"Esri - Topografico": ESRI_topo,
			"Esri - National Geopraphic": ESRI,
			};
			
		var capasOverlay = {
		
			"Capa 1": osm,
			"Capa 2": osm2,
			};
						
		new L.control.layers(capasBase, capasOverlay,{collapsed:false}).addTo(mapa);
		
		/*http://localhost:8080/geoserver/MOGT/wms?service=WMS&version=1.1.0&request=GetMap&layers=MOGT:Hidrografia_Nacional&styles=&bbox=245960.5684996972,1435255.6968641817,914205.3946725248,1768409.439797226&width=768&height=382&srs=EPSG:32616&format=application/openlayers*/
		
		
		var plazacentral = L.marker([ 14.0423, -86.5727]);
		mapa.addLayer(plazacentral);
		plazacentral.bindPopup("CURC DANLI");
		
		var sta = L.marker([ 15.7611, -86.8267]);
		mapa.addLayer(sta);
		sta.bindPopup("CURC LA CEIBA");
		
		var sta = L.marker([  14.075418, -87.187839]);
		mapa.addLayer(sta);
		sta.bindPopup("SEDE CENTRAL: TEGUCIGALPA");
		
		var sta = L.marker([   14.664399, -86.221419]);
		mapa.addLayer(sta);
		sta.bindPopup("CUR JUTICALPA");
		
		var sta = L.marker([   13.5372, -87.4892]);
		mapa.addLayer(sta);
		sta.bindPopup("CUR NACAOME");
		
		var sta = L.marker([   13.2959, -87.1886]);
		mapa.addLayer(sta);
		sta.bindPopup("CUR CHOLUTECA");
		
		var sta = L.marker([   14.3061, -88.1663]);
		mapa.addLayer(sta);
		sta.bindPopup("CUR LA ESPERANZA");
		
		var sta = L.marker([   14.9181, -88.2355]);
		mapa.addLayer(sta);
		sta.bindPopup("CUR SANTA BÁRBARA");
		
		var sta = L.marker([  15.4915, -88.0168]);
		mapa.addLayer(sta);
		sta.bindPopup("CUR SAN PEDRO SULA");
		
		var sta = L.marker([  14.5896, -88.5856]);
		mapa.addLayer(sta);
		sta.bindPopup("CUR GRACIAS");
		
		var inl = L.marker([  14.769929, -88.77372]);
		mapa.addLayer(inl);
		inl.bindPopup("CUR SANTA ROSA DE COPÁN");
		
		
		/*<!--Centro del mapa-->
		var mapcenter = L.marker(mapa.getCenter(),{opacity:0.5});
		mapa.addLayer(mapcenter);
		mapcenter.bindPopup("Centro del mapa");*/
		
		new L.Control.Zoom({ position: 'topright'}).addTo(mapa);
		
		var miniMap = new L.Control.MiniMap(osm2,{ toggleDisplay: true, position: 'bottomright' }).addTo(mapa);
		var MousePosition = new L.control.mousePosition(osm).addTo(mapa);
		var escala = L.control.scale().addTo(mapa);
		var viewCenter = new L.Control.ViewCenter(mapa);
			mapa.addControl(viewCenter);
		
	</script>
	
	</body>
	<p><i><strong><font size="4", color="green">Pablo César Díaz</font></strong></i></P>
</html>
