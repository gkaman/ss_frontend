http://www.gkaman.com/ss_frontend

ss_frontend

STRUCTURE
root:
  index.html (also calls http://code.jquery.com/jquery-latest.js)
	
	_css:
		ss_frontend.css
		
	_js:
		ss_frontend.js
		PX500.js
	
	_php:
		proxy.php
	


SS_FRONTEND.JS
is on $(document).ready().
creates and instance of PX500
creates the category selector from the 'cat' array
binds the onchange function to the category selector
hides the main image div. $('#featuredImg')


PX500.JS
functions:

function: PX500 - constuctor
	 
	params:none
	
	properties:
	_px: Object = this  		self reference
	tileCount: Number		pixel size of tiling thumbnails
	featuredImg:Object		contains original size of featured image before resizing occurs
	tc:Number			incrementing number keeping track of thumbnail count
	photos:Object			json object data return for thumbnails set to global
	loadingID:Number		unique id for thumbnails per category load
	loading:Boolean			if request is in progress
	token:String			consumer key for 500px api





function: getCategory - creates request object for ajax call for image category

	params:
	_cat:String			category of image stream

	properties:
	pxURL:Object			object for ajax call
		url
		feature
		image_size
		category
		only


function: getFeatured - creates request object for ajax call for featured image

	params:
	_id:String			id of image to get

	properties:
	pxURL:Object			object for ajax call
		url

function: send - sends request object to 500px api via _php/proxy.php using POST

	params:
	_url:Object			Object for ajax call
	callback:function		function to call on success of ajax request
	

	success:function
	error:function


function: populatePhotos - populates #photos div with data from ajax json return

	params:
	_data:json			ajax return
	
	
function: populateFeatured - populates and displays main image

	params:
	_data:json			ajax return

	properties:
	infoString:String		string for photo title and ueser name
	vs:Ojbect			viewSize of window
	img:Image			thumbnail
	imgWidth:Number			Width of featured image
	imgHeight:Number		Height of feature image

function: reSize - retiles #photo div to cover page with thumbnails and recenter and resized main image if displayed

	params:none
	
	properties:
	vs:Ojbect			viewSize of window
	viewW:Number			Number of tiles horizonally
	viewH:Number			Number of tiles vertically
	imgWidth:Number			Width of featured image
	imgHeight:Number		Height of featrued image

function: viewSize - returns widht and height of html
	
	params:none
	
	properties:
	widthHeight:Object
		w
		h

proxy.php is a fix for ajax same-origin security policy.  It takes the request object from the ajax call and get the contents from 500px.com from post Variables.
						
	
	


	
		