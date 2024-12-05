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

=> More readable code, less code duplication, isolates independent parts of code.

2. Inline Method



3. Extract Variable
4. Inline Temp
5. Replace Temp With Query
6. Split Temporary Variable
7. Remove Assignments To Parameters
8. Replace Method With Method Object
9.  Substitute Algorithm
