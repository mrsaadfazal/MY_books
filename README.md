---
description: Top Array functions/Methods in javascript
cover: >-
  https://images.unsplash.com/photo-1662614380507-72f8d36f1d2b?crop=entropy&cs=tinysrgb&fm=jpg&ixid=MnwxOTcwMjR8MHwxfHNlYXJjaHwyfHxBcnJheXxlbnwwfHx8fDE2NjUwNzk0MzY&ixlib=rb-1.2.1&q=80
coverY: 0
---

# 👨🏫 Array  functions

## Here are 12 javascript array methods:

1. [filter()](./#filter-method)
2. [forEach()](./#foreach-method)
3. [some()](./#some-method)
4. [every()](./#every-method)
5. [includes()](./#includes-method)
6. [map()](./#map-method)
7. [reduce()](./#reduce-method)
8. [sort()](./#sort-method)
9. find()
10. findIndex()
11. Array.from()
12. Array.of()



## Filter method:

`filter` is **the** method whenever you want to, well, filter out values. Only want positive values? Only looking for objects that have a certain property? `filter` is your way to go.



### The following is the signature of the `filter` method:

{% code overflow="wrap" %}
```javascript
filter(function (element, index, array) {
  // element is the element within the array
  // index is the index of the element in the array
  // array is a reference to the array filter works on
}, thisOverride);
// thisOverride is a way to override the semantical this within the callback function.
// If you set it to another object, calling this.anyThing would access anyThing within that
// object, and not the actual array.
```
{% endcode %}

### Example useCase:

Imagine that you have an online shop. And now you want to send a discount code to all customers that live in a certain area.

```javascript
const getElibigleCustomers(customers, zipCode) {
  return customers.filter(
    (customer) => customer.address.zipCode === zipCode
  );
}
```

`getElibigleCustomers` returns all customers that have an address stored with a zipCode, which is the same zipCode you look for. All other customers are filtered out of the array.



## ForEach Method:

`forEach` is a functional way to loop over array elements and execute some logic for each element. The method itself doesn't return a new array.



### The following is the signature of the `forEach` method:

```javascript
forEach(function (element, index, array) {
  // element is the element within the array
  // index is the index of the element in the array
  // array is a reference to the array forEach works on
}, thisOverride);
// thisOverride is a way to override the semantical this within the callback function.
// If you set it to another object, calling this.anyThing would access anyThing within that
// object, and not the actual array.

```

### Example useCase:

Let's stay with the example of the online shop. Now, you want to print all names of the customers you previously filtered out.

```javascript
 getElibigleCustomers(customers, '123456')
  .forEach(
    (customer) => console.log(`${customer.forename} ${customer.surname}`)
  );
```

When forEach executes, the console prints the full name of all customers that were previously filtered out.

#### OR

This method can help you to loop over array’s items.

```javascript
  const arr = [1, 2, 3, 4, 5, 6];

  arr.forEach(item => {
    console.log(item); // output: 1 2 3 4 5 6
  });
```



## Some() method:

`some` is a special array method. It tests whether at least one element within the array tests positive for a specific condition. If so, `some` returns true, otherwise, it returns false.



### The following is the signature of the `some` method:

{% code overflow="wrap" %}
```javascript
some(function (element, index, array) {
  // element is the element within the array
  // index is the index of the element in the array
  // array is a reference to the array some works on
}, thisOverride);
// thisOverride is a way to override the semantical this within the callback function.
// If you set it to another object, calling this.anyThing would access anyThing within that
// object, and not the actual array.
```
{% endcode %}

### Example useCase:

Back to our online shop example. Imagine that you now want to test whether at least some of the customers you filtered out are underage. If so, you want to show them another deal, because everyone else gets a discount for alcoholic drinks. But you don't want to support underage children drinking, of course

```javascript
const eligibleCustomers = getElibigleCustomers(customers, '123456')

const containsUnderAgedCustomers = eligibleCustomers.some(
  (customer) => customer.age < 18
);
```

When `some` executes, it checks each customer's age property. If at least one is below 18, it returns false.

#### OR

This method check if at least one of array’s item passed the condition. If passed, it return ‘true’ otherwise ‘false’.

```javascript
 const arr = [1, 2, 3, 4, 5, 6];

  // at least one element is greater than 4?
  const largeNum = arr.some(num => num > 4);
  console.log(largeNum); // output: true

  // at least one element is less than or equal to 0?
  const smallNum = arr.some(num => num <= 0);
  console.log(smallNum); // output: false
```

## Every() method:

`every` is the counterpart of `some`. It tests whether all elements satisfy a condition. Only then, the method returns true. If only one element fails the test, false is returned.

### The following is the signature of the `every` method:

{% code overflow="wrap" %}
```javascript
every(function (element, index, array) {
  // element is the element within the array
  // index is the index of the element in the array
  // array is a reference to the array every works on
}, thisOverride);
// thisOverride is a way to override the semantical this within the callback function.
// If you set it to another object, calling this.anyThing would access anyThing within that
// object, and not the actual array.
```
{% endcode %}

### Example useCase: <a href="#heading-example-use-case" id="heading-example-use-case"></a>

Many customers who received your discount code have ordered by now. To save on shipment costs, you want to send it out all at once. But first, you need to check whether all those customers have valid address data saved.

```javascript
const customersWhoOrdered = getCustomersForOrder('discount1234');

const allCustomersHaveValidShipmentData = customersWhoOrdered
  .every(
    (customer) => hasValidShipmentData(customer)
  );
```

When `every` executes, it passes each customer to a function that checks whether that customer has valid shipment data stored. If only one customer has invalid data, the whole function returns false.

#### OR

This method check if all array’s item passed the condition. If passed, it return ‘true’ otherwise ‘false’.

```javascript
  const arr = [1, 2, 3, 4, 5, 6];

  // all elements are greater than 4
  const greaterFour = arr.every(num => num > 4);
  console.log(greaterFour); // output: false

  // all elements are less than 10
  const lessTen = arr.every(num => num < 10);
  console.log(lessTen); // output: true
```

## Includes() method:

`includes` is a method that checks whether an array contains a specific element. It's good for a quick check, but it also has its drawbacks, which we talk about in a minute.

### The following is the signature of the `includes` method:

```javascript
includes(function (searchElement, fromIndex) {
  // searchElement is the element you look for
  // fromIndex is the index the search should start at
});
```

### Example useCase: <a href="#heading-example-use-case" id="heading-example-use-case"></a>

`includes` is special. It actually tests for strict equality, which means: It either searches for a value that is strictly equal to the search element, or it looks for the exact reference of an object.

Let's say you want to check whether the customers orders include a very specific order, like this:

```javascript
const allOrders = getAllOrders();

const containsSpecificOrder = allOrders.includes({
  customer: 'John Doe'
  zipCode: '54321'
});
```

You would probably be surprised to find out that include returns false, even if the array contains an object with the exact same properties. This is because it looks for strict equality, and objects are only strictly equal if they are the same reference. JavaScript does not know an equals method.

This reduces `includes`' use cases to primitive values. If you, for example want to check whether an array of numbers contains a specific number like this:

```javascript
const numbers = [1, 2, 3, 4, 5];

const includesFive = numbers.includes(5);
```

Here is a rule of thumb: If you deal with an array of primitive values, use `includes`. If you deal with objects, use `some` because it allows you to pass in a callback with which you can test objects for equality.

#### OR

This method check if array includes the item passed in the method.

```javascript
const arr = [1, 2, 3, 4, 5, 6];

  arr.includes(2); // output: true
  arr.includes(7); // output: false
```

## Map() method:

`map` is one of the most important array methods out there. Whenever you want to transform all values within an array, `map` is **the** way to go.

### The following is the signature of the `map` method:

{% code overflow="wrap" %}
```javascript
map(function (element, index, array) {
  // element is the element within the array
  // index is the index of the element in the array
  // array is a reference to the array map works on
}, thisOverride);
// thisOverride is a way to override the semantical this within the callback function.
// If you set it to another object, calling this.anyThing would access anyThing within that
// object, and not the actual array.

```
{% endcode %}

### Example useCase: <a href="#heading-example-use-case" id="heading-example-use-case"></a>

Let's jump back to the point where you had all eligible customers filtered. Now, you want to send their orders off and need to get all their addresses. This is a great use case for map:

```javascript
const eligibleCustomers = getElibigleCustomers(customers, '123456');

const addresses = eligibleCustomers
  .map((customer) => customer.address);
```

\
`map` iterates over all customers and then extracts all addresses. These are put into a new array and returned from the function.

#### OR

This method create new array by calling the provided function in every element.

```javascript
const arr = [1, 2, 3, 4, 5, 6];

  // add one to every element
  const oneAdded = arr.map(num => num + 1);
  console.log(oneAdded); // output [2, 3, 4, 5, 6, 7]

  console.log(arr); // output: [1, 2, 3, 4, 5, 6]
```

## Reduce() method:

`reduce` is the most powerful array method existing. It can be used to reimplement all existing array methods, and it's the most flexible one. Talking about all the advantages it offers would definitely need an article on its own, but you will get a glimpse of it soon.

### The following is the signature of the `reduce` method:

{% code overflow="wrap" %}
```javascript
reduce(function (accumulator, currentValue, currentIndex, array) {
  // accumulator is the result of the last call, or the initialValue in the beginning
  // currentValue is the value currently processed
  // currentIndex is the index of the current value within the array
  // array is a reference to the array reduce works on
}, initialValue);

```
{% endcode %}

### Example useCase: <a href="#heading-example-use-case" id="heading-example-use-case"></a>

Remember when you wanted to find out whether there were underage customers? Another way to deal with this problem is to group all your eligible customers into two groups. Those of legal age, and those who are underage.



```javascript
const eligibleCustomers = getElibigleCustomers(customers, '123456');

const customerGroups = eligibleCustomers
  .reduce((accumulator, customer) => {
    if (customer.age > 18) {
      accumulator[0].push(customer);
    } else {
      accumulator[1].push(customer);
    }
    return accumulator;
  }, [[], []]);
```

`reduce` can be pretty difficult to understand but we can go over the above code together and see what it does. In this case, the accumulator is a 2-dimensional array. Index 0 contains all customers >= 18 years of age. Index 1 contains all customers who are underage. The first time reduce runs, it sets accumulator to the empty 2-dimensional array. Within the method, the code checks whether the age property of the customer is above 18. If so, it pushes the customer to the first array. If the customer is underaged, they get pushed to the second array. In the end, the 2-dimensional array with the grouped customers is returned.

#### OR

The reduce() method applies a function against an accumulator and each element in the array (from left to right) to reduce it to a single value - MDN

```javascript
  const arr = [1, 2, 3, 4, 5, 6];

  const sum = arr.reduce((total, value) => total + value, 0);
  console.log(sum); // 21  
```

## Sort() method:

The name of `sort` already says it all. Whenever you want to sort an array, this is the method you need to call.

### The following is the signature of the `sort` method:

```javascript
sort(function (firstElement, secondElement) {
  // firstElement is the first element to compare
  // secondElement is the second element to compare
});
```

### Example useCase:

Whenever you need to sort something, you found a use case for `sort`. Let's, for example, try to sort your customers by age. For such a case, `sort` allows you to pass in a comparator function that you can use to tell `sort` how to properly order them.

```javascript
const customers = getCustomers();

customers.sort((a, b) => customer.a - customer.b);
```

The callback function must return a number based on the order of the elements. It should return a value < 0 if a comes before b, 0 if both are equal, and a value > 0 if a comes after b.

#### OR

This method used to arrange/sort array’s item either ascending or descending order.

```javascript
 const arr = [1, 2, 3, 4, 5, 6];
  const alpha = ['e', 'a', 'c', 'u', 'y'];

  // sort in descending order
  descOrder = arr.sort((a, b) => a > b ? -1 : 1);
  console.log(descOrder); // output: [6, 5, 4, 3, 2, 1]

  // sort in ascending order
  ascOrder = alpha.sort((a, b) => a > b ? 1 : -1);
  console.log(ascOrder); // output: ['a', 'c', 'e', 'u', 'y']
```
