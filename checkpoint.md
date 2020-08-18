## Checkpoint

### 1. What is the Big O for this?

1)	Determine the Big O for the following algorithm: You are sitting in a room with 15 people. You want to find a playmate for your dog, preferably of the same breed. So you want to know if anyone out of the 15 people have the same breed as your dog. You stand up and yell out, who here has a golden retriever and would like to be a playdate for my golden. Someone yells - "I do, be happy to bring him over"
  
        Best Case: O(1)
        Average Case: O(1)
        Worst Case: O(n)
          
2) Determine the Big O for the following algorithm: You are sitting in a room with 15 people. You want to find a playmate for your dog who is of the same breed. So you want to know if anyone out of the 15 people have the same breed as your dog. You start with the first person and ask him if he has a golden retriever. He says no, then you ask the next person, and the next, and the next until you find someone who has a golden or there is no one else to ask.

        Best Case: O(1)
        Average Case: O(n)
        Worst Case: O(n)

### 2. Even or odd

What is the Big O of the following algorithm? Explain your answer

  ```javascript
  function isEven(value) {
    if (value % 2 === 0) {
      return true;
    }
      return false;
  }
  ```

    Best Case: O(1)
    Average Case: O(1)
    Worst Case: O(n)

The function is evaluating 'n % 2' which is a constant time algorithm, unless 'n' changes, then it could become linear.
			
### 3. Are you here?

What is the Big O of the following algorithm? Explain your answer

```javascript
function areYouHere(arr1, arr2) {
  for (let i = 0; i < arr1.length; i++) {
    const el1 = arr1[i];
    for (let j = 0; j < arr2.length; j++) {
      const el2 = arr2[j];
      if (el1 === el2) return true;
    }
  }
  return false;
}
```

      Best Case: O(n^2)
      Average Case: O(n^2)
      Worst Case: O(n^2)

The function is looping through `arr1` - `O(n)` and creating a variable for each element - `O(1)`. Also there is an inner loop of `arr2` - `O(n)` and creates a variable for each element - `O(1)`. Then compares both variables - `O(1)` to return a boolean. Each loop is linear but beacuse of the inner loop the function becomes polynomial - `O(n^2)`

### 4. Doubler

What is the Big O of the following algorithm? Explain your answer
  
  ```javascript
  function doubleArrayValues(array) {
      for (let i = 0; i < array.length; i++) {
          array[i] *= 2;
      }
      return array;
  }
  ```

        Best Case: O(n)
        Average Case: O(n)
        Worst Case: O(n)

The function is looping through each element of an array, multiplying each element - `O(1)`, and returns the altered array which is an `O(n)` operation, because there is action on every element in the array. 

### 5. Naive search

What is the Big O of the following algorithm? Explain your answer
  
  ```javascript
  function naiveSearch(array, item) {
      for (let i = 0; i < array.length; i++) {
          if (array[i] === item) {
              return i;
          }
      }
  }
  ```
      Best Case: O(1)
      Average Case: O(n)
      Worst Case: O(n)

This function searches for an element in an array and checks to see if it 'deep equals' the item parameter. If the first element matches the `item` then the operation is `O(1)`, therefore on average the loop will hit more than one individual element making the operation - `O(n)`     

### 6. Creating pairs:

What is the Big O of the following algorithm? Explain your answer
    
  ```javascript
  function createPairs(arr) {
      for (let i = 0; i < arr.length; i++) {
          for(let j = i + 1; j < arr.length; j++) {
              console.log(arr[i] + ", " +  arr[j] );
          }
      }
  }
  ```

      Best Case: O(n^2)
      Average Case: O(n^2)
      Worst Case: O(n^2)

This function loops through two arrays and prints each element concatenated to the console. Because there are twop loops performing `O(n)` operations the function takes at least `O(n^2)` time.

### 7. Compute the sequence

What does the following algorithm do? What is its runtime complexity? Explain your answer
      
  ```javascript
  function compute(num) {
      let result = [];
      for (let i = 1; i <= num; i++) {

          if (i === 1) {
              result.push(0);
          }
          else if (i === 2) {
              result.push(1);
          }
          else {
              result.push(result[i - 2] + result[i - 3]);
          }
      }
      return result;
  }
  ```
        Best Case: O(n)
        Average Case: O(n)
        Worst Case: O(n)

  This function creates an array `result` and loops for as manny times as the amount of `num`. 
If the `i` is 1, `0` is added to `result`, if `i` is `2`, `1` is pushed to `result`, otherwise, 
the last element and the second to last element of `result` are added together and pushed to `result`. 
Each operation is `O(1)` as it just appends to the end of `result` and acceses the elements by index. 
However, because there is a counter - `i` beginning at `1` and ending with `num`, the operation takes 
as long as the size of `num` making it linear.

### 8. An efficient search

In this example, we return to the problem of searching using a more sophisticated approach than in naive search, above. Assume that the input array is always sorted. What is the Big O of the following algorithm? Explain your answer

  ```javascript
  function efficientSearch(array, item) {
      let minIndex = 0;
      let maxIndex = array.length - 1;
      let currentIndex;
      let currentElement;

      while (minIndex <= maxIndex) {
          currentIndex = Math.floor((minIndex + maxIndex) / 2);
          currentElement = array[currentIndex];

          if (currentElement < item) {
              minIndex = currentIndex + 1;
          }
          else if (currentElement > item) {
              maxIndex = currentIndex - 1;
          }
          else {
              return currentIndex;
          }
      }
      return -1;
  }
  ```
        Best Case: O(log n)
        Average Case: O(log n)
        Worst Case: O(log n)
        
  This function takes in an array and a item. The item is compared to a sorted array and returns `-1` or the index of the element that equals `item`. `minIndex` starts at `0` and `maxIndex` starts at the end. While the `minIndex` is less than `maxIndex`, `currentIndex` is `minIndex`/`maxIndex` which is rounded down and should represent the middle of the array. `currentElement` is the element at the index of `currentIndex`. If the `currentElement` is less than the item, the `minIndex` or `maxIndex` becomes the next or previous index greater or less than `currentIndex`. `currentIndex` is reassigned, which represents the new middle and comparisons are made again. If neither less or greater, `currentIndex` is returned, if `minIndex` is higher than `maxIndex` (the item was not found in the array) `-1` is returned. The function is splitting the array in half and comparing two numbers which is `O(1)`, however, it is doing this `n` times which makes the function logarithmic.

### 9. Random element

What is the Big O of the following algorithm? Explain your answer

  ```javascript
  function findRandomElement(arr) {
      return arr[Math.floor(Math.random() * arr.length)];
  }
  ```
      Best Case: O(1)
      Average Case: O(1)
      Worst Case: O(1)
      
This is constant time because it just accesses an array with an index which is a random number between 0 and `arr.length` and returns that element.

### 10. What Am I?
What does the following algorithm do? What is the Big O of the following algorithm? Explain your answer

  ```javascript
  function isWhat(n) {
      if (n < 2 || n % 1 !== 0) {
          return false;
      }
      for (let i = 2; i < n; ++i) {
          if (n % i === 0) return false;
      }
      return true;
  }
  ```
      Best Case: O(1)
      Average Case: O(n)
      Worst Case: O(n)
      
This function compares `n`, if `n` is less than `2` or if `n` % `1` is not `0` (not a whole number) it returns false. It loops if the the condition is not met. Starting at two, if `n` is divisible by `i` return false, else return true. Therefore, `n` must be not divisible. If the first condition is met then it is constant, if not than it loops dependent on `n`.

### 11. Tower of Hanoi

  ```javascript
 /**
 * Tower of Hanoi
 * @param {number} disk
 * @param {string} start represents the staring post, which changes depending on which disk you are moving
 * @param {string} destination represents the desination post, which changes ^^
 */
function hanoi(disk, start, destination, intermediate) {
	if (disk === 1) {
		// disk 1 is the smallest disk
		// Base case is moving smallest disk to from Rod A to Rod C
		console.log(`Move disk 1 from Rod ${start} to Rod ${destination}`);
	} else {
		// Solve for n - 1 disks, but move them from Rod A to Rod B
		hanoi(disk - 1, start, intermediate, destination);
		// Move the largest disk (disk n) from Rod A to Rod C
		console.log(`Move disk ${disk} from Rod ${start} to Rod ${destination}`);

		// Compare for the n - 1 disks again, and move them from Rod B to Rod C
		hanoi(disk - 1, intermediate, destination, start);
	}
}

hanoi(4, 'A', 'C', 'B');
```

### 12. Iterative Version

  ```javascript
  function countSheepIt(numOfSheep) {
    for (let i = numOfSheep; i > 0; i--) {
      console.log(`${i}: Another sheep jumps over the fence`);
    }
      console.log('All sheep jumped over the fence');
  }
  ```
  
  ```javascript
  function pwrCalc(base, exp) {
  if (exp < 0) return 'exponent should be >= 0';
	if (exp === 1) return base;
  
	// loop starting at 1, i = 1
    let result = base;
    for (let i = 1; i < exp; i++) {
      // multiply base * exp and save in 'result'
      result *= exp;
    }
  // return result
	return result;
  }
  ```
  
  ```javascript
  function revStr(str) {
	// create result
    let result = '';
    // loop through string
    // add last index to result string
    // decrement i
    for (let i = str.length - 1; i >= 0; i--) {
      result += str[i];
    }
    // return result
    return result;
  }
  ```
  
  ```javascript
  function nthTriangleItt(int) {
    let result = int;
    for (let i = 1; i < int; i++) {
      result += i;
    }
	return result;
  }
  ```
  
  ```javascript
  function stringSep(string, limiter) {
    //set up results
    const results = [];
    // set up good strings variable
    let goodStrings = '';
      // loop through string
      for (let i = 0; i < string.length; i++) {
        if (string[i] !== limiter) {
          // for each good string add to good string variable
          goodStrings += string[i];
        } else {
          // if index equals limiter return push to result
          results.push(goodStrings);
          goodStrings = '';
        }
      }
    // push final good string results
    results.push(goodStrings);
    // return results
    return results;
  }
  ```
  
  ```javascript
  function fibbo(num) {
    // set up variables
    // a = 1
    // b = result
    // temp
    let a = 1,
      b = 0,
      temp;

    // start at 1
    for (let i = 1; i <= num; i++) {
      // copy the first number
      temp = a;
      // add first number to the second number in the sequence
      a += b;
      // copy b for next loop
      b = temp;
    }
    // return result
    return b;
  }
  ```
  
  ```javascript
  function factorial(num) {
    // set up variables
    // a = num
    let a = num;
    for (let i = num - 1; i >= 1; i--) {
      // multiply by next number in sequence
      // add to variable
      a *= i;
    }
    // return result
    return a;
  }
  ```
  
### 13. Recursive Big O

Take your solutions from the recursive exercises that you completed in the previous checkpoint and identify the time complexities (big O) of each of them.

### 14. Iterative Big O

Take your solutions from the iterative exercises today and identify the time complexities (big O) of each of them.
