# localStorageDB
Increase localStorage size 10 times or more! This tiny script uses bare minimum of IndexedDB to give you a simple key - value local storage system. It's asnychchronous so it's performance is also faster than native localStorage(in theory and this must be confirmed by testing)

* 10x more space than localStorage
* Asynchronous - faster than localStorage
* Minimal code - 0.76kB!
* No dependencies
* Cross-browser support: Chrome, Firefox, IE 11+, Edge, iOS Safari, mobile Chrome, Android Browser

## Usage

```javascript
// Setting values
ldb.set('nameGoesHere', 'value goes here');
// or 
ldb.set('nameGoesHere', 'value goes here', function(){
  console.log("Data is successfully written to the disk.")
}); 

// Getting values - callback is required because the data is being retrieved asynchronously:
ldb.get('nameGoesHere', function (value) {
  console.log('And the value is', value);
});
```

## For modern browsers only(Chrome, Firefox, Edge) but not IE or Safari

This version makes setting values even easier and it looks more like original localStorage. To use this mode uncomment marked section in localStorageDB.js

Now you can set values like this:
```javascript
ldb.nameGoesHere = 'value goes here';
```

Getting will stay the same, because callback is still needed for asynchronous retrieval

### You can use it as a one-liner in your JS code:
Instead of including a file you can copy and paste this piece of code to your JS file

> Minified by `uglifyjs -c -m -- localStorageDB.js > localStorageDB.min.js`

```javascript
!function(){var r,c,e=window.indexedDB||window.mozIndexedDB||window.webkitIndexedDB||window.msIndexedDB;e?(c={k:"",v:""},(e=e.open("d2",1)).onsuccess=function(e){r=this.result},e.onerror=function(e){console.error("indexedDB request error"),console.log(e)},e.onupgradeneeded=function(e){r=null,e.target.result.createObjectStore("s",{keyPath:"k"}).transaction.oncomplete=function(e){r=e.target.db}},window.ldb={get:function e(t,n){r?r.transaction("s").objectStore("s").get(t).onsuccess=function(e){e=e.target.result&&e.target.result.v||null,n(e)}:setTimeout(function(){e(t,n)},100)},set:function(e,t,n){c.k=e,c.v=t;let o=r.transaction("s","readwrite");o.oncomplete=function(e){"Function"==={}.toString.call(n).slice(8,-1)&&n()},o.objectStore("s").put(c),o.commit()}}):console.error("indexDB not supported")}();

```