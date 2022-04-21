# React Calculator

- We use Reducer to changing of the state , as it change the state or we say it ensure the smooth transition of input and output , all cases are defined in this only.

```js
function reducer(state, { type, payload })
```

## Resourses

### Actions Objects

In this there is all of the operation or we say that the processes which help us to drive a good flow in our calculator project.

```js
ACTIONS = {
	ADD_DIGIT: "add-digit",
	CHOOSE_OPERATION: "choose-operation",
	CLEAR: "clear",
	DELETE_DIGIT: "delete-digit",
	EVALUATE: "evaluate",
};
```

### keys JS

This is the component which made a button for the numbers.

```js
<Digibutton digit="2" dispatch={dispatch} />

// digit & Dispatch act as a prop.
```

### Operator JS

This is the component which made a button for the numbers.

```js
<Digibutton operation="2" dispatch={dispatch} />

// operation & Dispatch act as a prop.
```

### Clearing

here we simply add an event button `onclick` one and dispatch a case of type `ACTION_CLEAR`.

```js
case ACTIONS.CLEAR: return {};
```

## Edge Cases

### More zeroes pressing

Here we check that our `payload digit` means the digit we are entering by pressing and current is also zero then we dont change state.

```js
if (payload.digit === "0" && state.currentOperand === "0") {
	return state;
}
```

### More than one decimal point

Here we check if there one decimal already in expression then we check if includes the `"."` then we return simply the state.

```js
if (payload.digit === "." && state.currentOperand.includes(".")) {
	return state;
}
```

### If we change the operator

If the current operator or we say only one operand is present and we chaging the operand , we can do that we reserving the prevoius state and append new operator.

```js
if (state.currentOperator == null) {
	return {
		...state,
		operation: payload.operation,
	};
}
```

### Overwride

In this we check if there is overwrite thing then we clear the scren and print payload digit.

```js
if (state.overwrite) {
	return {
		...state,
		currentOperand: payload.digit,
		overwrite: false,
	};
}
```

## Operations

### First case

If we dont enter any operand or we say `current` and `previousoperand` both are **NULL** we return state.

```js
if(state.currentOperand== null && state)
```

### Second case

If the previous operand is `null` then we have to operation is the key which we press and make `previousOperand` is changed to `state.currentOperand` .... at last set `currentOperand` is **NULL**.

```js
if(state.prebiousOperand==null){
    ...state,
    operation: payload.operation,
    previousOperand: state.currentOperand,
    currentOperand: null,
}
```

### Evaluation

Evaluate the expression.

```js
return {
	...state,
	operation: evaluate(state),
	previousOperand: state.currentOperand,
	currentOperand: null,
};
```

### Evaluate Function

```js
function evaluate({ currentOperand, previousOperand, operation }) {
	const prev = parseFloat(previousOperand);
	const curr = parseFloat(currentOperand);
	if (isNaN(prev) || isNaN(curr)) return "";
	let computation = "";
}
```

### Operations Switch cases

```jsx
switch (operation) {
	case "+":
		computation = prev + current;
		break;
	case "-":
		computation = prev - current;
		break;
	case "*":
		computation = prev * current;
		break;
	case "÷":
		computation = prev / current;
		break;
}
```

Note: At last we convert the `computation` variable to the string to display as output.
