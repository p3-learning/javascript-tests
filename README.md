# JavaScript Test

To better undestand testing frameworks this repo goes step by step implementing a simple one.

It's mainly based in the Kent's [blog post](https://kentcdodds.com/blog/but-really-what-is-a-javascript-test)

## Step 1

We have created two helper functions inside the `math.mjs` file which are `sum` and `subtract`, they accept numbers as arguments and return their values.

```javascript
const sum = (a, b) => a + b;
const subtract = (a, b) => a - b;

export { sum, subtract };
```

and our first test is

```javascript
import { sum, subtract } from "./math.mjs";

let result, expected;

result = sum(3, 7);
expected = 10;
if (result !== expected) {
	throw new Error(`${result} is not equal to ${expected}`);
}

result = subtract(7, 3);
expected = 4;
if (result !== expected) {
	throw new Error(`${result} is not equal to ${expected}`);
}
```

Now we can't break any of these functions without breaking our test.

## Step 2

We can use the assert module from node to test and throw errors

```javascript
import assert from "assert";
import { sum, subtract } from "./math.mjs";

let result, expected;

result = sum(3, 7);
expected = 10;
assert.strictEqual(result, expected);

result = subtract(7, 3);
expected = 4;
assert.strictEqual(result, expected);
```

## Step 3

Creating our own expect HOF that returns toBe function

```javascript
import { sum, subtract } from "./math.mjs";

let result, expected;

result = sum(3, 7);
expected = 10;
expect(result).toBe(expected);

result = subtract(7, 3);
expected = 4;
expect(result).toBe(expected);

function expect(actual) {
	return {
		toBe(expected) {
			if (actual !== expected) {
				throw new Error(`${actual} is not equal to ${expected}`);
			}
		}
	};
```