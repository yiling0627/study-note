#ES6
>let var & const

	const:
	declare one read-only constant
	needs to be initialized when it is
	declared
	scope:
	let,const - in the current code block 
	var - global varible
	
	hoisting:
	let,const - no hoisting
	var - moving the declaration to the top of the
	      current scope
	// var 的情况
	console.log(foo); // 输出undefined
	var foo = 2;

	// let 的情况
	console.log(bar); // 报错ReferenceError
	let bar = 2;
	
	
	let - temporal dead zone