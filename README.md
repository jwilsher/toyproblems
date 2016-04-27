# toyproblems
solved toy problems

Fibonacci Sequence
    
    function fibo(n) {
        var start = [0, 1];
        if(n <= 2) return 1;
        for (var i = 2; i <= n; i++){
           start[i] = start[i-1] + start[i-2];
        }
        return start;
    }


//create a function that gives the fibonacci sequence index value given 'N'
//fibo called function
//start value to keep track of our fibonacci
//check to make sure input is >=2 return
//for loop to loop through n times at start value two
//math! update start value i-1 i-2

//return start value

------------------------------------------------------

Merge

//Write a function "Merge" that takes in two arrays 'arr1' 'arr2' + a callback 
//merge shuld be able to add the tow arrays returning and calling 
//the result back as a console.log

//ie...merge([1,2,3,4,5], [3,4,5,6,7], function(output) {
//          console.log('Output:', output);
//    })

//"Output:" [4, 6, 8, 10, 12]

//in class solution.....

function merge(arr1, arr2, cb) {

    if (arr1.length !== arr2.length) {
        throw new Error('array]\'s need to be same length'); // stops the execution of the function..throws error to console
    }
    var results = [];
    for (var i = 0; i < arr1.length; i++) {
        results[i] = arr1[i] + arr2[i];
    }

    cb(results);

}

var q = merge([1,2,3,4,5], [3,4,5,6,7], function(output) {
    console.log("Output:", output);
})


-----------------------------------------------------------

Once

//write function 'once' that takes another function as its argument and returns a new version of 
//that function that can only be called once.

//subsequent callls to the resulting function should have no effect (and should return undefined)

    var once = function(fn) {
      return fn;  
    };
    
    //the following is to help you test your code
    
    var f = once(function(x) {
       return x; 
    });
    
    console.log(f(1));
    console.log(f(1));


//my solution stuff...

    function once(cb) {
        var called = false;
        return function() {
            if (!called) {
                called = true;
                return fn.apply(null, arguments); // review this.....???
            }
            else {
                return undefined;
            }
        }
    }

-------------------------------------------

Partially Applied Function 'Add'

//"higher-order " functions that return new functions

//your task is to make this work....

    console.assert(add(2,3) == 5)
    console.assert(add(2)(3)() == 5)
    console.assert(add(2,3,4) == 9)
    console.assert(add(2)(3)(4)() == 9)



//starting to solve it.....

    function add() {
        //if we only got one arguent, return a parially applied function, otherwise return the
        //result of adding everything together
        if (arguments.length > 1) {
            return Array.from(arguments).reduce(function(sum, current) {
            return sum + current;
            }, 0)
        }
    
    }



////class stuff....

    function sum(numbers) {
        return Array.from(numbers).reduce(function(sum,current){
            return sum + current
        }, 0)  //this initializes the sum to be 0
    }
    
    
    function add() {
        if(arguments.length > 1) {
            return sum(arguments)
        } else {
            //do our partial function stuff
            return add.bind(null, arguments[0])
        }
    }

------------------------------------------------------

Sum #'s in an Array

//given any array, pick out the numbers and sum them




///class solution...


    var sumArray = function(arr) {
        var result = 0;
    
        arr.forEach(function(d) {
            if (typeof d === 'number') {
                result += d;
            }
    
            if (Array.isArray(d)) {
                result += sumArray(d);
            }
        });
    
        return result;
    }
    
    
    sumArray([1, 'cat', [2, 'dog']]);

-------------------------------------------------------

Characters between A and B

//write a function that checks to see if the letter 'a' has two or more charers separating it from 'b'

//'a' should come before 'b'

    //console.log(ab('accb')); // true
    //console.log(ab('acb')); // false
    //console.log(ab('basdfb')); //true
    //console.log(ab('a beautiful dog')); //false
    //console.log(ab('another beautiful dog')); // true


//in class solution....

    var ab = function(str) {
    
        for (var i = 0; i < str.length; i++) {
    
            if (str[i] === 'a') {
    
                for (var j = i + 1; j < str.length; j++) {
    
                    if (str[j] === 'b') {
    
                        if (j - i > 2) {
    
                            return true;
                        }
                    }
                }
            }
        }
    
        return false;
    
    };

--------------------------------------------

Factorial

//write a function that returns !n

    //console.log(factorial(3)); // returns 6
    //console.log(factorial(5)); // 120

//My solution....

    function factorial(n) {
    
        var tracker = n;
    
        for (var i = 1; i < n; i++ ) {
    
            tracker = tracker * (n-i);
        
        }
    
        return tracker;
    
    }
    
    factorial(3);

//in class solution...

//with RECURSION...
    function factorail(n) {
    
        if(n === 1) return n; // this is called a base case
        return n * factorial(n-1); /// this won't return until factorial(n-1) can evaluate
    }

------------------------------------

Fix It to Print 1,2,3,4,5

//This prints out " 5, 5, 5, 5, 5"....fix it to say "1, 2, 3, 4, 5"
    for (var i = 0; i < 5; i++) {
        setTimeout(function() {
            console.log(i);
        }, 0);
    }

//solution...with immmediately invoked function expression....
    for (var i = 0; i < 5; i++) {
       (function (i) {
            setTimeout(function() {
                console.log(i);
            }, 0);
        })(i);
    }

//another solution...
    function doTimeout(index) {
        setTimeout(function() {
            console.log(index);
        }, 0);
    }
    
    for (var i = 0; i < 5; i++) {
        doTimeout(i);
    }
    }

-------------------------------------

Functions in Functions

//write a function that takes in an array of numbers, adds them all
//together, and returns a function that when set to a variable
//and called, returns the original array with the sum added to the
//end as the last element

//hint:  what higher order function can you use to sum an array?

//in class answer....

    function reduceAndAdd(arr) {
        if (!arr) throw new error ("the reduceAndAdd function requires an array argument");
    
        arr.forEach(function(item) {
            if (typeof item !== "number")
                throw new error("array must be numbers only");
        });
    
        var arrSum = arr.reduce(function(a, b) {return a + b});
        return function() {
            arr.push(arrSum);
            return arr;
        };
    }
    
    var numArr = [1,2,3,4,5];
    
    var testReduceAndAdd = reduceAndAdd(numArr);
    testReduceAndAdd();

---------------------------------

greatestPrimePalindrome

//find the largest palandrone that is prime and less than 1000

    function isPrime(n) {
      if( n % 2 === 0) return false;
      for (var i = 3; i < n; i += 2) {
        if (n % i === 0) {
          return false;
        }
      }
      return true;
    }
    
    
    function palFinder() {
      var tracker;
      for (var i = 2; i < 1000; i++) {
        if (isPrime(i)){
          if (i.toString().split('').reverse().join('') === i.toString()) {
            tracker = i;
          }
        }
      }
      return tracker;
    }

///in class solution...

    function greatestPrimePalindrome() {
      for (var i = 1000; i > 1; i--) {
        var isPrime = true;
        for (var j = i - 1; j > 1; j--) {
          if (i % j === 0) {
            isPrime = false;
            break;
          }
        }
        if (isPrime && parseInt(i.toString().split('').reverse().join('')) === i) {
          return i;
        }
      }
    }
    
    console.log(greatestPrimePalindrome());

------------------------------------

greetSupremeLeaderFirst

///Partially applied functions

    function greet() {
        return Array.from(arguments).map(function(name){
            return "hi" + name
        })
    }
    
    greetButGreetSupremeLeaderFirst = greet.bind(null, "Supreme Leader");
    
    
    greetButGreetSupremeLeaderFirst('jaci');

---------------------------

isPalindrome

//write a function that determines if a given string is palindrome or not

    function isPalindrome (str) {
        
        if(str.split('').reverse().join('') === str) {
            return true;
        }
        return false;
    }
    
    isPalindrome('racecar'); // true
    isPalindrome('cats'); // false

---------------------------------

isPrime

    function isPrime(n) {
      if( n% 2 === 0) return false;
      for (var i = 3; i < n; i += 2) {
        if (n % i === 0) {
          return false;
        }
      }
      return true;
    }
    
    isPrime(6);

--------------------------------

longestWord

///my solution...
    function longestWord(sentence) {
      
      var tracker;
      var myArray = sentence.split(' ');
      tracker = myArray[0];
      
      for (var i = 1; i < myArray.length; i++) {
         if (myArray[i].length > myArray[0].length) {
           tracker = myArray[i];
         }
      }
      return tracker;
    }

//in class solution....

    function longestWordInSentence(sentence) {
        var longest = '';
        sentence.split(' ').forEach(function(word) {
            longest = word.length > longest.length ? word : longest; // This is a ternary operator >>> if the length of word is greater
            //than the length of longest, assign longest the value of word. Otherwise assign longest the 
            //value of longest. Before the ? is the conditon, after is the true case result, then after
            //the ":" is the false case result.
        });
        return longest;
    }
    
    console.log(longestWordInSentence('hello everyone what is up'));

------------------------------

meanMode

//Write a function that returns true if the mean and the mode of a given array are the same..
    // ie...
    // var arr = [1,2,3,4,5];
    // var arr2 = [2,2,2,3,5,25];

    //var meanMode = function(numbers) {
    
    //};
    
    //console.log(meanMode(arr)); // true
    //console.log(meanMode(arr2)); //false


//My solution...

    function mean(arr) {
        var result = 0;
        arr.forEach(function(elem, index) {
            result = result + elem;
        });
        console.log(result);
        result = result / arr.length;
        return result;
    }
    mean([1, 2, 3]);
    
    function mode(arr) {
        var result = 0;
        arr.forEach(function(elem, index) {
            
        });
    }


//in class...

    var meanMode = function(numbers) {
        var total = 0
            , numCount = {}
            , mode = 0
            , highestOccurrence = 0
            , mean
            ;
    
        numbers.forEach(function(number) {
            total += number; //mean
            if (numCount[number]) {    //does the key of "1" exist? if so we will increment it
                numCount[number]++;   
            } else {   //mode
                numCount[number] = 1;  // if it doesn't exist, we are going to create a key of "1" with a value of "1"
            }
        });
    
        mean = total / numbers.length;
        console.log(mean);
    
        for (var key in numCount) {
            if (numCount[key] > highestOccurrence) {
                highestOccurrence = numCount[key];
                mode = parseInt(key);
            }
        }
        console.log(mode);
        return mean === mode;
    };
    
    meanMode([1,2,3,4,5]);

---------------------------------------------

removeDuplicates

//write a function that removes the duplicates in a given array of integers

    function removeDuplicates(arr) {
    
       for(var i = 0; i < arr.length - 1; i++) {
           for(var j = i + 1; j < arr.length; j++) {
    
               if(arr[i] === arr[j]) {
                   arr.splice(j, 1);
               }
           }
       }
    
        return arr;
    }
    
    removeDuplicates([1,2,3,3,4,4]);
    
    //in class solutions....
    
    function removeDuplicates(arr) {
    
        var uniqObj = {};
        var uniqArr = [];
    
        arr.forEach(function(item) {
            uniqObj[item] = null;
    
        });
        for (var key in uniqObj) {
            uniqArr.push(parseInt(key));
        }
        return uniqArr;
    
    }

----------------------------------------------

sumOfTwo

//write a function that, given an unsorted array, checks whether there are any 2 numbers that
//will sum up to the given number
//ie... var arr = [1,3,4,5,7]
//sumOfTwo(arr, 6); --> true


//solution...

    function sumOfTwo (arr, num) {
       for (var i = 0; i < arr.length - 1; i++) {
           for (var j = i + 1; j < arr.length; j++) {
               var total = arr[i] + arr[j];
               if (total === num) return true;
           }
       }
        return false;
    }
    
    sumOfTwo([1, 5, 2, 3], 8);

-----------------------------

//my solution...
    function switchCase(str) {
      var myArray = [];
      myArray = str.split('');
      myArray.forEach(function(letter, index){
        if (letter === letter.toUpperCase()) {
          myArray[index] = letter.toLowerCase();
        }
        else {
          myArray[index] = letter.toUpperCase();
        }
      });
      
      var newArray = myArray.join('');
      return newArray;
    }
    
    switchCase('Hello');

//in class solution....
    function switchCase(str) {
        var letters = str.split('');
        letters.forEach(function(letter, i) {
            var isUpperCase = letter.toUpperCase() === letter; // if the comparison is true or false, it
            //will assign either true or false to "isUpperCase"
            letters[i] = isUpperCase ? letter.toLowerCase() : letter.toUpperCase();
        });
        return letters.join('');
    }
    
    switchCase('Hello');
