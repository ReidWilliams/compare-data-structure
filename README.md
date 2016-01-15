# treetorn

A JavaScript package that helps you enforce data strucutre consistency and write schemas by example.

## Installation

```
npm install treetorn --save
```

You may instead just want to use treetorn for testing:

```
npm install treetorn --save-dev
```

## Examples

Compare two data structures that are equivalent:

```javascript

import compare from 'treetorn';

let a = {
	cities: [
		{ name: 'San Francisco', nicknames: ['SF', 'the city'], id: 0 },
		{ name: 'Orlando', nicknames: ['O-town', 'The city beautiful'], id: 1 }
	],
	people: [
		{ name: 'Reid', hometown: 1, current_home: 0 },
		{ name: 'Joe', hometown: 2, current_home: 2 }
	]
}

let b = {
	cities: [
		{ name: 'Sun Valley', nicknames: ['A great place to ski'], id: 0 },
		{ name: 'San Francisco', nicknames: ['SF', 'the city'], id: 1 }
	],
	people: [ { name: 'Piper', hometown: 0, current_home: 1 } ]
}

compare(a, b);
// returns { passes: true, err: undefined }
```

Compare two data structures that have a small difference:

```javascript
let oops = {
	cities: [
		{ name: 'San Francisco', nicknames: ['SF', 'the city'], id: 0 },
		// oops, here id is a list but should be a scalar
		{ name: 'Orlando', nicknames: ['O-town', 'The city beautiful'], id: [] }
		],
	people: [
		{ name: 'Reid', hometown: 1, current_home: 0 },
		{ name: 'Joe', hometown: 2, current_home: 2 }
	]
}

compare(b, oops);
// returns { passes: false, err: '0 is a leaf but [] is not' }
```




