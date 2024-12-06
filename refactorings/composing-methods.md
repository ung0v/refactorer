# Composing Methods

These technique below mostly help to resolve understandable and readable code.

1. Extract Method
<table>
<tr>
<th> Bad </th>
<th> Good </th>
</tr>
<tr>
<td>

```typescript
printOwing(): void {
  printBanner();

  // Print details.
  console.log("name: " + name);
  console.log("amount: " + getOutstanding());
}
```

</td>
<td>

```typescript
printOwing(): void {
  printBanner();
  printDetails(getOutstanding());
}

printDetails(outstanding: number): void {
  console.log("name: " + name);
  console.log("amount: " + outstanding);
}
```

</td>
</tr>
</table>

2. Inline Method
<table>
<tr>
<th> Bad </th>
<th> Good </th>
</tr>
<tr>
<td>

```typescript
class PizzaDelivery {
  // ...
  getRating(): number {
    return moreThanFiveLateDeliveries() ? 2 : 1;
  }
  moreThanFiveLateDeliveries(): boolean {
    return numberOfLateDeliveries > 5;
  }
}
```

</td>
<td>

```typescript
class PizzaDelivery {
  // ...
  getRating(): number {
    return numberOfLateDeliveries > 5 ? 2 : 1;
  }
}
```

</td>
</tr>
</table>



3. Extract Variable
<table>
<tr>
<th> Bad </th>
<th> Good </th>
</tr>
<tr>
<td>

```typescript
renderBanner(): void {
  if ((platform.toUpperCase().indexOf("MAC") > -1) &&
       (browser.toUpperCase().indexOf("IE") > -1) &&
        wasInitialized() && resize > 0 )
  {
    // do something
  }
}
```

</td>
<td>

```typescript
renderBanner(): void {
  const isMacOs = platform.toUpperCase().indexOf("MAC") > -1;
  const isIE = browser.toUpperCase().indexOf("IE") > -1;
  const wasResized = resize > 0;

  if (isMacOs && isIE && wasInitialized() && wasResized) {
    // do something
  }
}
```

</td>
</tr>
</table>
4. Inline Temp
<table>
<tr>
<th> Bad </th>
<th> Good </th>
</tr>
<tr>
<td>

```typescript
hasDiscount(order: Order): boolean {
  let basePrice: number = order.basePrice();
  return basePrice > 1000;
}
```

</td>
<td>

```typescript
hasDiscount(order: Order): boolean {
  return order.basePrice() > 1000;
}
```

</td>
</tr>
</table>
5. Replace Temp With Query
<table>
<tr>
<th> Bad </th>
<th> Good </th>
</tr>
<tr>
<td>

```typescript
 calculateTotal(): number {
  let basePrice = quantity * itemPrice;
  if (basePrice > 1000) {
    return basePrice * 0.95;
  }
  else {
    return basePrice * 0.98;
  }
}
```

</td>
<td>

```typescript
calculateTotal(): number {
  if (basePrice() > 1000) {
    return basePrice() * 0.95;
  }
  else {
    return basePrice() * 0.98;
  }
}
basePrice(): number {
  return quantity * itemPrice;
}
```

</td>
</tr>
</table>
6. Split Temporary Variable
<table>
<tr>
<th> Bad </th>
<th> Good </th>
</tr>
<tr>
<td>

```typescript
let temp = 2 * (height + width);
console.log(temp);
temp = height * width;
console.log(temp);
```

</td>
<td>

```typescript
const perimeter = 2 * (height + width);
console.log(perimeter);
const area = height * width;
console.log(area);
```

</td>
</tr>
</table>
7. Remove Assignments To Parameters
<table>
<tr>
<th> Bad </th>
<th> Good </th>
</tr>
<tr>
<td>

```typescript
discount(inputVal: number, quantity: number): number {
  if (quantity > 50) {
    inputVal -= 2;
  }
  // ...
}
```

</td>
<td>

```typescript
discount(inputVal: number, quantity: number): number {
  let result = inputVal;
  if (quantity > 50) {
    result -= 2;
  }
  // ...
}
```

</td>
</tr>
</table>
8. Replace Method With Method Object
<table>
<tr>
<th> Bad </th>
<th> Good </th>
</tr>
<tr>
<td>

```typescript
class Order {
  // ...
  price(): number {
    let primaryBasePrice;
    let secondaryBasePrice;
    let tertiaryBasePrice;
    // Perform long computation.
  }
}
```

</td>
<td>

```typescript
class Order {
  // ...
  price(): number {
    return new PriceCalculator(this).compute();
  }
}

class PriceCalculator {
  private _primaryBasePrice: number;
  private _secondaryBasePrice: number;
  private _tertiaryBasePrice: number;
  
  constructor(order: Order) {
    // Copy relevant information from the
    // order object.
  }
  
  compute(): number {
    // Perform long computation.
  }
}
```

</td>
</tr>
</table>
9.  Substitute Algorithm
<table>
<tr>
<th> Bad </th>
<th> Good </th>
</tr>
<tr>
<td>

```typescript
foundPerson(people: string[]): string{
  for (let person of people) {
    if (person.equals("Don")){
      return "Don";
    }
    if (person.equals("John")){
      return "John";
    }
    if (person.equals("Kent")){
      return "Kent";
    }
  }
  return "";
}
```

</td>
<td>

```typescript
foundPerson(people: string[]): string{
  let candidates = ["Don", "John", "Kent"];
  for (let person of people) {
    if (candidates.includes(person)) {
      return person;
    }
  }
  return "";
}
```

</td>
</tr>
</table>
