**Building a Chrome extension**

At a very basic level, a Chrome extension is just some HTML, CSS and JavaScript that allows you to add some functionality to Chrome through some of the JavaScript APIs Chrome exposes. An extension is basically just a web page that is hosted within Chrome and can access some additional APIs.

Chrome extensions can also be created to work only on certain pages through the use of Page Actions, they can run code in the background using Background Pages, and they can even modify an existing page loaded in the browser using Content Scripts. But for this tutorial we are going to keep things simple and not use any of that..as we are going to just use the Chrome Storage API t(there's a bunch of chrome API's Like scrape 

**Steps**

 1. Create your working directory- which I'll point chrome to in a few steps.
 2. All Chrome extensions require a manifest file (manifest.json)- basically our config file. so create that. This is telling  Chrome what the extension is going to do, and what permissions it requires in order to do those things. In our example's manifest, we will declare a browser action, the activeTab permission to see the URL of the current tab.
 {
  "manifest_version": 2,
	  "name": "Gisella's First Plugin",
  "description": "This extension will do something useful and cool",
  "version": "1.0",
	"browser_action": {
   "default_icon": "icon.png",
   "default_popup": "popup.html"
  },
  "permissions": [
   "activeTab" 
	"https://ajax.googleapis.com/"
	   ]
}
	
3. 19x19px PNG file (icon for our extension)
4.  We’ll need an HTML page to show when a user clicks our Browser Action, so we’ll create a popup.html file.
	
		<!doctype html>
		<html>
		  <head>
		    <title>Gisella's First Browser Plugin</title>
		    <script src="popup.js"></script>
		  </head>
		  <body>
		    <h1>G's Mystery Browser Plugin</h1>
		    <button id="checkPage">Do Something Now!</button>
		  </body>
		</html>
		
5. And due to security constraints, we can’t put inline JavaScript into our HTML file so we'll create a separate  popup.js file. 
		
		
		document.addEventListener('DOMContentLoaded', function() {
		  var checkPageButton = document.getElementById('checkPage');
		  checkPageButton.addEventListener('click', function() {
		
		    chrome.tabs.getSelected(null, function(tab) {
		      d = document;
		
		      var f = d.createElement('form');
		      f.action = 'http://gtmetrix.com/analyze.html?bm';
		      f.method = 'post';
		      var i = d.createElement('input');
		      i.type = 'hidden';
		      i.name = 'url';
		      i.value = tab.url;
		      f.appendChild(i);
		      d.body.appendChild(f);
		      f.submit();
		    });
		  }, false);
		}, false);
		
	
	
6. Testing it out
	Extensions that you download from the Chrome Web Store are packaged up as .crx files, which is great for distribution, but not so great for development.  Recognizing this, Chrome gives you a quick way of loading up your working directory for testing. Let's do that now.
	It’s really easy to test a new extension in Chrome. Type “chrome://extensions” in a tab to bring up the extensions page.
	Make sure you are in developmetn mode.
	click “Load unpacked extension”


Great Tutorial
https://www.sitepoint.com/create-chrome-extension-10-minutes-flat/
