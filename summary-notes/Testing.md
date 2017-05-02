# Testing

## Reasons for testing
1. To make sure that there are no bugs in the program.
2. To make sure as you develop new features in the program, the new features do not impact the old features.

## Three step process 

The three step process is called: **Red, Green, Refactor**

**Red**: Write tests that fail - so that you know tests are working.   
**Green**: Write the minimal amount of code possible so that tests pass.   
**Refactor**: Refactor your code to be more efficient and ensure the code keeps passing all tests.

## Tools
In testing we use Jasmine and Mocha + Chai - generally these tools function the same way, but with slightly different syntax.

The required syntax as of follows: 

```javascript
describe("description of function", callback() {
	it("description of test" callback_expect(){
		expect(function()).to.equal(expectedValue);
	});
});
```

1. describe - Is used to descibe which function you are testing, it requires two parameters: 
	* A string to describe your test.
	* A callback function to hold your test.
2. it - Is used to describe our expectations, it requires two parameters:
	* A string to describe what we expect
	* A callback function to hold the expectatons
3. expect - Is the function for the tests. it requires three components:
	* Actual return value
	* A comparator function
	* Expected return value

Jasmine | Mocha | Comparator functions
---|---| ---
toBe | to.equal | tests the value is equal
toEqual | to.deep.equal | tests the array and object is equal

For Chai assertion styles, please see the following link: http://chaijs.com/guide/styles/#expect  
For Chai comparator function chains, please see the following link: http://chaijs.com/api/bdd/  
For Jasmine comparator functions, please see the following link: https://jasmine.github.io/2.0/introduction.html

## Examples

```javascript
describe("Testing expand on an array", function(){
	it("repeats array n times on a array of numbers", function(){
		expect(expand([1,2,3],3)).to.deep.equal([1,2,3,1,2,3,1,2,3]);
	});
	it("repeats array n times on a array of stings", function(){
		expect(expand(["foo", "test"], 1)).to.deep.equal(["foo","test"]);
	});
});

describe("Testing acceptNumbersOnly to accept numbers only in arguments", function(){
	it("tests an only number arguments", function(){
		expect(acceptNumbersOnly(1,2,3,4,5,6,7)).to.equal(true);
	});
	it("tests a mixed arguments", function(){
		expect(acceptNumbersOnly(1,"foo")).to.equal(false);
		expect(acceptNumbersOnly(1,2,3,4,5,6,NaN)).to.equal(false);
		expect(acceptNumbersOnly(1,[2,3,4])).to.equal(false);
	});
});
```