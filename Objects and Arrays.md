# Objects and Arrays
### Array declearation
```
	let arrName = [1, 2, 3]; // index start from 0
```
Some function for array
```
	arrName.length(); // output = 3;
	arrName.push(5); // new array = 1, 2, 3, 5
	arrName.pop(); // new array = 1, 2, 3
	console.log(arrName); // output = [1, 2, 3]
```

### Object declearation
object are arbitrary collections of properties. there will be more than one variable. let's see an object
```
	let objectName{
		var1: true,
		var2: 'avash',
		var3: 10,
		arr: [1, 2, 3]
	};
	
	// access properties of object
	objectName.var1
	objectName.arr[1]
```
If we try to access a property that doesn't exist in the object then it will give undefined-
```
	console.log(objectName.undefinedproperty); // output = undefined
```
We can create a new property inside an object by using `=`.
```
	objectName.undefinedproperty = 10;
	console.log(objectName.undefinedproperty); // output = 10
```
We can delete an existion property -
```
	delete objectName.var1;
	console.log(objectName.var1); // output = undefined
```
You can check if a property exist in the object by using `in`-
```
	console.log("propertyName" in objectName); // will be bool type, true or false
	// We can't just use console.log(objectName.propertyName), because it can undefined in 2 case
	// 1) property not exist
	// 2) property exist but value is not set
```

	
