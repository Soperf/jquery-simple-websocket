# jQuery Simple WebSocket
Send and receive JSON objects via a single gracefull websocket and use a fluent deferred interface, queuing messages.

## Example

```
<script type="text/javascript" src="https://code.jquery.com/jquery-1.12.0.min.js"></script>
<script type="text/javascript" src="https://cdnjs.cloudflare.com/ajax/libs/jquery-json/2.5.1/jquery.json.min.js"></script>
<script type="text/javascript" src="jquery.simple.websocket.js"></script>
<script type="text/javascript">
    var webSocket = $.simpleWebSocket({ url: 'ws://127.0.0.1:3000/' });

    webSocket.listen(function(message) {
        console.log(message.text);
    }).done(function() {
        // socket closed or listener removed
    }).fail(function(e) {
        // error occurred
    });

    webSocket.send({ 'text': 'hello' }).done(function() {
        // message send
    }).fail(function(e) {
        // error sending
    });
</script>
```

or fluent:
```
var webSocket = $.simpleWebSocket({ url: 'ws://127.0.0.1:3000/' })
.listen(function(message) { console.log('listener1: '+message.text); }).fail(function(e) { console.log(e); })
.listen(function(message) { console.log('listener2: '+message.text); }).fail(function(e) { console.log(e); })
.listen(function(message) { console.log('listener3: '+message.text); }).fail(function(e) { console.log(e); })
.send({'text': 'hello'});
```

# Usage
```
var socket = $.simpleWebSocket({
                                 url: 'ws://127.0.0.1:3000/',
                                 protocols: 'your_protocol', // optional
                                 timeout: 20000, // optional, default timeout between connection attempts
                                 attempts: 60 // optional, default attempts until closing connection
                               });

socket.connect();

socket.isConnected(); // or: socket.isConnected(function(connected) {});

socket.send({'foo': 'bar'});

socket.listen(function(data) {});

socket.remove(listenerCallback);

socket.close();
```
Note: if you want to send messages / listen to another socket, close the previous socket e. g.:
```
var socket = $.simpleWebSocket({ url: 'ws://127.0.0.1:3001/' });
socket.send({'data': 'characters'});

socket.close();

socket = $.simpleWebSocket({ url: 'ws://127.0.0.1:3002/' });
socket.listen(function(message) { console.log(message); });
```

### Web Chat Example
- start nodejs websocket server:
```
$ node tests/server.js
```
- open tests/example.html

# History
- jQuery Simple Web Socket has been forked from https://github.com/dchelimsky/jquery-websocket
- which originates from http://code.google.com/p/jquery-websocket/

# License
Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

   http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.

previously:

The MIT License (MIT)

Copyright (c) 2010 by shootaroo (Shotaro Tsubouchi).

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
