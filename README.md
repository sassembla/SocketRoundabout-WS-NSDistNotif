# SocketRoundabout
0.8.3  
Connect WS/HTTP/NSDistributedNotification/BT.

*This repository does not contains HTTP/BT connections.


### From Input to Output through connection

####connect
connect the connections & ransfer the message.(string only)

* Input WebSocketClient -> (message:String) -> Output to NSDistNotification 
* Input WebSocketServer -> (message:String) -> Output to Other-WebSocketServer 


####split
split the connection's output to multi connections.

* Input WebSocketClient -> (message:String)  
	-> Output to Other-WebSocketServer_1  
	-> Output to Other-WebSocketServer_2

####join
Join some connection's outputs in one output.

* Input  
	WebSocketClient_1 -> (message:String)  
	WebSocketClient_2 -> (message:String)  
	-> Output to Other-WebSocketServer  
	
####routing
When A received input from B, then output to C.

* Input A -> Output to B -> Input to A -> Output to C  
	

### Setting with *.sr file
	//1.set WebSocket client to specific WS-server.
	id:MyWebSocketConnection type:0 destination:ws://127.0.0.1:SOMEPORT option:websocketas:client

	
	//2.set NSDistNotification client named "testNotif"
	id:MyDistNotifConnection type:1 destination:DISTNOTIFICATION_IDENTITY


	//3.connent with direction (WS -> NSDistNotif)
	connect:MyWebSocketConnection to:MyDistNotifConnection

* trans message.  
	(WSServer@ws://127.0.0.1:SOMEPORT) ->  
	WSClient@ws://127.0.0.1:SOMEPORT -> 
	DISTNOTIFICATION_IDENTITY
* commentable //
* sequential & wait for connect.
* Double-click then run SocketRoundabout.

### Data through modifying
Add the "prefix" & "suffix" When the data through connections.

	//transfer
	trans:MyWebSocketConnection to:MyWebSocketConnection prefix:TEST_PREFIX suffix:TEST_SUFFIX

will change the message through the connection.

### Emit message
Run specific message to connection.

	//emit
	emit:HelloWorld to:MyWebSocketConnection
	
Emit from file

	//emitFile
	emitfile:/Users/sassembla/Desktop/SocketRoundabout/HelloWorld.txt to:rMyWebSocketConnection
	

###Limitation
Use one *.sr per one SocketRocket App. 
