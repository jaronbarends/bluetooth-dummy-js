# bluetooth-dummy.js

Dummy implementation of bluetooth.js for WebBluetooth API

Can be used in combination with bluetooth.js: https://github.com/360fun/bluetooth.js

For web bluetooth, you need a secure webserver which makes it more difficult to develop locally. This script returns resolving promises for all bluetooth calls.

## Usage

Check if we're on localhost or filesystem; if not, use regular webbluetooth; otherwise use dummy version.

````javascript

//
let webbluetooth;
const url = window.location.href;
if (url.indexOf('http') === 0 && url.indexOf('localhost') === -1) {
	webbluetooth = new WebBluetooth();
} else {
	webbluetooth = new WebBluetoothDummy();
}
````

When you have a class instance that has already defined a webbluetooth instance, you can redefine it for local and file system connections

````javascript
// defined somewhere else
const someClassInstance = new SomeClass();

// webbluetooth was defined within that class:
this.webbluetooth = new WebBluetooth();

//
const url = window.location.href;
if (url.indexOf('http') !== 0 || url.indexOf('localhost') > -1) {
	someClassInstance.webbluetooth = new WebBluetoothDummy();
}
````

After instantiating the dummy bluetooth, you can call all methods of bluetooth.js on it. It will always return a resolving promise.