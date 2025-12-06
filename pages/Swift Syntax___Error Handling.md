- ``` swift
  func makeASandwich() throws {
      // ...
  }
  
  
  do {
      try makeASandwich()
      eatASandwich()
  } catch SandwichError.outOfCleanDishes {
      washDishes()
  } catch SandwichError.missingIngredients(let ingredients) {
      buyGroceries(ingredients)
  }
  ```
- ---
- ## 参考
	- [Swift Docs - Error Handling](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/errorhandling)
	  logseq.order-list-type:: number
	-
	- logseq.order-list-type:: number