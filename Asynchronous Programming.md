# Asynchronous Programming (callback, Promise, async & await) 
let we have called to function. If they are synchronous then second one will start to execute only when the first one end its process. but if asynchronous then both of them can run parallelly. Asynchronous Programming is helpfull when programm try to access HD, network etc that is slow.

### callback function.
Why we need callback? let's see a code.

```
	setTime(() => {console.log("hello")}, 500);
	// here 500 is millisecond.
	// () => console.log("hello") is the function
	// that will be called after 500 ms.
	
	// you can also use function keyword
	setTime(function() {console.log("hello")}, 500)
	
```

So it will take 500 ms to print `hello` but program will not sit idle in that time, it will execute other instruction. That is asynchronous.

Lets see another code.
```
	const Read = () => {
	   setTimeout(() => {
	      // some operation for read happen.
	   }, 1000)
	}

	const Print = () => {
	   // print something that is read.
	}

	read();
	Print();
```
What will happen in the previos code that `Read()` will end after 1000 ms but `Print()` will not wait so we will not get our expected value. To solve this we will use call back function. When Read() ends it will call print. Modyfied code is given below-
```
	const Read = (callback) => {
	   setTimeout(() => {
	      // some code for read happen.
	      callback(); // print is called here
	   }, 1000)
	}

	const Print = () => {
	   // print something that is read.
	}

	Read(print); // print() will be called after Read()
```
Let's see a reallife problem. A Pseudocode for JS is given below.
```
	let Data = requestData('http://someLink.com');
	console.log(Data); 
```
In the code above `requestData()` is a server request, so it will take time to finish. But as JS is asynchronous, the next line of console.log will be executed and we will get undefined. So we need to use callback here. Modyfied code is-
```
	requestdata('http://someLink.com', (Data) => {
		console.log(Data); 
	});
	// here '(Data) => {console.log(Data); }' is the callback function passed as parameter.
	// Data is the return value of server, and is the parameter of callback function
	// callback function will execute after server give a response
```

### Promise
In a promise there are two callback function(`then(...)`, `catch(...)`). If the called promise is resolved then function inside `then()` will be executed, and if rejected then function inside `catch()` will be executed. Let's see a code of a simple promise-

```
	aPromise(parameter)
	  .then(() => {
	     console.log('request successfull');
	  })
	  .catch(() => {
	     console.log('request Failure');
	  })
```
Most of the time we don't need to implement the promise function. But we need to know how it works. Let's see how a promise function is implemented-
```
	const aPromise = parameter => { 
	   return new Promise((resolve, reject) => {
	      setTimeout(() => { // here setTimeout is used for trying to mimic, that server is taking some time to response.
		 if(control) {
		    resolve(Data); // then() function will be called if success, data will be the parameter of callback function
		 } else {
		    reject(Error); // catch() function will be called if rejected
		 }
	      }, 3000) // 3000 ms, to mimic server time
	   })
	}
	
	/// now call the promise
	aPromise(parameter)
	  .then((Data) => {
	     console.log('request successfull');
	  })
	  .catch((Error) => {
	     console.log('request Failure');
	  })
	
```
Now, we might need to handle more than one promise before executing some code. We can write put all the promise in a array. See the code below-
```
	Promise.all([promise1, promise2])
	  .then((arrayOfData) => {
	     console.log('successfull);
	  })
```

## async & await
Let's recall what problem we were solving-
``` 
	Code: 
		let data = readData('http://...'); //  some request for data
		console.log(data); // use the read data
	Problem:
	The problem in this code is that, as the JS is asunchronus and readData() will take some time 
	to execute, so console.log() will be executed before reading data.
```
We can handle this problem with promise, but nested promise will make the code hard to read. A more easy way to handle this is using `async` function. Inside async function JS will work like synchronous program. So one line will execute first then it will go to the next line. We need to use `await` keyword before exery `promise` inside the async function. Solution code-
```
	async function funcName() {
		let data = await readData('http://...'); //  some request for data
		console.log(data); // this line won't be executed untill previous line is completed and data is read
	}
```
We haven't handle the reject issue in the previos code. We will use `try...catch` for handeling it-
```
	const funcName = async() => {
	   try {
	      const data = await readData('http://...') //  some request for data;
	      console.log(data);
	   } catch(error) {
	      console.log(error);
	   }
	}
```
Handeling more than one promise-
```
	const funcName = async() => {
	   	let data = await Promise.all([promise1, promise2]);
		// work with data
	}
```
So, why we are using `async, wait` is that, we want to make out code more readable. Let's see same code with `promise` and `async, wait`-
```
	Usign promise:
		getModelNo.then((model) => {
		   getPrice(model).then((price) => {
		      console.log('model is' + model + 'and price is' + price);
		   })
		})
	
	Using async, wait:
		const getMyDetails = async() => {
		   const model = await getModelNo;
		   const price = await getPrice(name);
		   console.log('model is' + model + 'and price is' + price);
		}
```

### Consider the fact wile doing asynchronous code
In js, all the synchronous code are run first, then asynchronous code runs. To understand this, let's run a code-
```
	console.log("start"); 
	setTimeout(()=> console.log("asychronous function is called"), 0); // asynchronous code
	for(let i=0; i<1000000000; i++); 
	console.log("end");
	// output-
	// start
	// end
	// asychronous function is called
```
We said in the asynchronous code that, it should be called after 0s but, it will not. First all the synchronous code will be executed. `for` loop is also a part of it. And then finally asynchronous code will be executed.



