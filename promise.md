##Promise
###It is an object and used for <font color="pink">asynchronous</font> operation. And acts as a proxy between asynchronous and callback function.

>3 status:
		
	Pending, resolve, reject

>Syntax

	const promise = new Promise(function(resolve,
	reject) {
	  // ... some code
	
	  if (/* 异步操作成功 */){
	    resolve(value);
	  } else {
	    reject(error);
	  }
	});
	-----------------------------------------------
	promise.then(function(value) {
	  // success
	}, function(error) {
	  // failure
	});


###After all the synchronous tasks executed, resolve() will be executed.

	let promise = new Promise(function(resolve,
	reject) {
	  console.log('Promise');
	  resolve();
	});
	
	promise.then(function() {
	  console.log('resolved.');
	});
	
	console.log('Hi!');
	
	// Promise
	// Hi!
	// resolved
	
	
###Promise implement Ajax call
	
	
