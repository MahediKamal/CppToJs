# Move to Js from C++. [Reference](https://eloquentjavascript.net/)

 - numbers is js is 64 bit
 - each character in a string in js is 16 bit
 - maximun float number we can use in the range of 10^15
 - naming convection of function is - `newFunctionName`
 - NaN == NaN -> this returns false
 - null == undefined -> this returns true 
 
#### To decleare a variable you can use `var` or `let`. `let` is more standard. lifetime of var is equivalent to the variable of C++. `var` will be global wherever you declear.
```
  	let v1 = 1, v2 = 2;
```

## function
### uning function keyword
```
	const name = function(par1, par2){
		// code
		// return
	};
	name(par1, par2); // function call
```
### We can create function inside a function which was not possible in C++
```
	const name1 = function(par){
		// code
		const name2 = function(par1, par2){
			//code
			// return 
		};
		name2(par1, par2); // function call
		// code
		// return
	};
	name1(par); // function call
```
### if we don't decleare funtion as contant then we can put different function in the same name
```
	let name = function(){
		// function 1
	};
	
	name = function(){
		// function 2
	};
```
### We can also declear function like C++. It is easier and we don't neet to pur `;` at the end.
```
	function funcName(){
		// code
		// return
	}
```
### Arrow fuction. Here we can relate with the first type, we replace `function` with `=>` and put it after the parameter.
```
	const name = (par1, par2) => {
		// code
		// return
	};
```
### Note: If we put extra parameter or less parameter if the function
```
1) ignores the extra arguments
	const name = function(par){
		// here we will get par1, and others have no effect 
	}
	name(par1, par2, par3);
	
2) missing parameters will be undefined
	const name(par1, par2){
		// here par2 = undefined
	}
	name(par1);
	
	but if we do - const name(par1, par2=2){ }. then par2 = 2, if it is not provided/
```

### Closure.
```
	function name(par1){ // first function
		let x = par1;
		// code
		return (par2) => { par1 * par2; } // second function
	}
	let name2 = name(par1); // now name2 holds the second function and it has also the value of par1 given into first function.
	name(par2); // now we can call name2 and it will also use the previos given parameter par1.
	

```
		
		
 

 
