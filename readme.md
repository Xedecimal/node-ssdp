## Usage - Server

```javascript
var SSDP = require('ssdp').SSDP;

var server = new SSDP;
server.addUSN('upnp:rootdevice');
server.addUSN('urn:schemas-upnp-org:device:MediaServer:1');
server.addUSN('urn:schemas-upnp-org:service:ContentDirectory:1');
server.addUSN('urn:schemas-upnp-org:service:ConnectionManager:1');

server.on('advertise-alive', function (heads) {
	// Expire old devices from your cache.
	// Register advertising device somewhere (as designated in http headers heads)
}

server.on('advertise-bye', function (heads) {
	// Remove specified device from cache.
}

// This should get your local ip to pass off to the server.
require('dns').lookup(require('os').hostname(), function (err, add) {
	server.server(add);
};
```

## Usage - Client

```javascript

var SSDP = require('ssdp').SSDP;
var client = new SSDP;

client.on('notify', function () {
	console.log('Got a notification.');
});

client.on('response', function inResponse(msg, rinfo) {
	console.log('Got a response to an m-search.');
});

ssdp.search('urn:schemas-upnp-org:service:ContentDirectory:1');

// Or maybe if you want to scour for everything

ssdp.search('ssdp:all');

// This should get you at least started.

```