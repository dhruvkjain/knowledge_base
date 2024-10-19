## Node.js

<details>
<summary>Basics</summary>
<be>

> ### **`Basics`** :
Node REPL = read evaluate print loop <br>
JavaScript is synchronous / single threaded but in Web V8 engine is run in Web API's which make it asynchronous. <br>
Node(V8) has some reserved token so it separates them from words which it can't understand and pass them to Node.js APIs which then use libuv to interact with OS or Threads init.<br>
Node runs an EVENT LOOP for asynchronous operations by making Threads (from a Thread pool of 4(default) Threads) or use our OS to run operations in it's own call-stack (FIFO). This call-stack is called EVENT QUEUES.<br>


>Now EVENT LOOP has many Phases (here are only main Phases):
- Timer                 - setTimeout , setInterval
- I/O callbacks      - network and file operations and anything that doesn't fit in other phases
- setImmediate     - runs immediately after all I/O operations are done
- Close callbacks   - closing files networks


>Node.js is an Events-driven which follows an Observer pattern. 

```javascript
const EventEmitter = require('node:events');

const MyEmitter = new EventEmitter();
MyEmitter.on('event' , ()=>{
	console.log('event occured');
})

// passing event to MyEmitter
MyEmitter.emit('event');

// ==============================================
// OUTPUT : event occured
// ==============================================
```

>Process which is an event emitter :

IN TERMINAL :
```javascript
node name_of_file.js something
```

IN name_of_file.js :
```javascript
process.argv.forEach((val , index)=>{
	console.log('${index}: ${val}');
});

// OUTPUT : 
// 0: node 
// 1: name_of_file.js
// 2: something
```

process.argv is an array that has elements as follows :
process.argv = [ process.execPath , name_of_js_file , arguments..... ]

So process.on is also an observer like MyEmitter.on (in above example) :
```javascript
process.on('exit' , (code)=>{
	console.log('Process exit event with an code: ', code);
})

// ====================================================
// OUTPUT : Process exit event with an code: 0
// ====================================================
```

```javascript
// ========================================================
// Method 1 : To securely only receive data (get end() automatically)
const { get } = require('https');

get('https://www.google.com' ,(res)=>{
	res.on('data' ,(chunk)=>{
		console.log(`Data chunk: ${chunk}`);
	});
	res.on('end' , ()=>{
		console.log('NO more data');
	});
});

// ==========================================================
// Method 2 : To securely receive and send data
const { request } = require('https');
const req = request('https://www.google.com' ,(res)=>{
	res.on('data' ,(chunk)=>{
		console.log(`Data chunk: ${chunk}`);
	});
	res.on('end' , ()=>{
		console.log('NO more data');
	});
})
req.end();

// ==========================================================
// Method 3 : To receive and send data
const { request } = require('http');
const req = request('http://www.google.com' ,(res)=>{
	res.on('data' ,(chunk)=>{
		console.log(`Data chunk: ${chunk}`);
	});
	res.on('end' , ()=>{
		console.log('NO more data');
	});
})
req.end();
```

> When we import using require in a program the file/module is executed and then store in require.cache . 
> So if we do 'require' multiple time it returns the function which is exported and does not rerun it. 

>if we try to 'require' a folder, node automatically exports any file with name " index.js ".

>AXIOS :
```javascript
const axios = require('axios');

axios.get('https://www.google.com')
	.then((res)=>{
		console.log(res);
	})
	.catch((err)=>{
		console.log(err);
	});
```

> Stream and Buffers :

Stream is to wait for a minimum chunk of data (data received before minimum data is reached is stored in a BUFFER) and load it when reached and then wait for another chunk of data to load.

```javascript
const buffer = new Buffer.from('abcde');

buffer.write('codevolution');
console.log(buffer.toString());
console.log(buffer);
console.log(buffer.toJSON());

// ======================================================
// OUTPUT : 
// codev
// <Buffer 63 6f 64 65 76>
// { type: 'Buffer', data: [ 99, 111, 100, 101, 118 ] }
// ======================================================

// <Buffer 63 6f 64 65 76> : this is in hexadecimals
// { type: 'Buffer', data: [ 99, 111, 100, 101, 118 ] } : are UNICODE/ASCII code

```
> Connect Streams :
```javascript
fs.createReadStream('data.csv')
    .pipe(parser)
```
Like above, after reading a chunk of data received from a fs stream it is piped to csv parser to parse the data from csv to objects/json.
>MVC (Model - View - Controller) pattern :
<img src="https://upload.wikimedia.org/wikipedia/commons/thumb/a/a0/MVC-Process.svg/300px-MVC-Process.svg.png">

> ROUTER :
 
Routers are used to bundle a group of controllers who have same base endpoint . So this isolates this bundle from others and we can make router folder like controllers.

For Example :
```javascript
// =======================================================
// Here friendsController is an js file in controllers file 
// from which post and get friend fuction are exported.
// =======================================================

// without routes
app.post('/friends' , friendsController.postFriend);
app.get('/friends' , friendsController.getFriend);
app.get('/friends/:friendId' , friendsController.getFriend);

// =======================================================

// with routes
const friendRouter = express.Router();
app.use('/friends' , friendsRouter);

friendRouter.post('/' , friendsController.postFriend);
friendRouter.get('/' , friendsController.getFriend);
friendRouter.get('/:friendId' , friendsController.getFriend);

```

> we can know IP address of each request by `req.ip`


> NOTE : In LINUX and MAC path to a folder is /folder/file but in Windows path is \\folder\\file 
> Therefore use path 
```javascript
const path = require('path');

path.join(__dirname , '..' , public , 'file-name');

// ===========================================================
// To send a file for example .jpg use sendFile

res.sendFile( path.join(__dirname , '..' , public , 'file-name.jpg') );
```

>To send some static files like html css js we can use express.static() middleware.
```javascript
app.use(express.static(path.join(__dirname , 'public' , 'index.html')));
```

```javascript
const requestData = { 
	[req.body.field]: req.body.value 
};
```
> In this code, we use square brackets `[]` around `req.body.field` to create a dynamic key based on the value of `req.body.field`, and then assign `req.body.value` as the value associated with that key. This will create a JSON object with the structure you desire.

</details>

<details>
<summary>Articles/Blogs</summary>
<br>

>[Javascript Hidden Classes and Inline Caching in V8 (richardartoul.github.io)](https://richardartoul.github.io/jekyll/update/2015/04/26/hidden-classes.html)

>[Optimization killers · petkaantonov/bluebird Wiki (github.com)](https://github.com/petkaantonov/bluebird/wiki/Optimization-killers)

>[Redis uses](https://www.instagram.com/p/C2ILjZErICX/)


</details>

