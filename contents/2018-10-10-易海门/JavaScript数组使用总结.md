## JavaScript数组使用总结

> 减少for与if嵌套使用  
> 我用的少或没用的可能就没总结

 1. `concat(...array | ...element)`连接两个或多个数组（元素），不改变原数组
 
 ```js
   let array1 = [1, 2, 3]
   array1.concat([4, 5, 6]) // [1 ,2 ,3 ,4 ,5 ,6]
   array1.concat(7, 8, 9) // [1, 2, 3, 7, 8, 9]
   array1.concat([4, 5, 6], [7, 8, 9]) // [1, 2, 3, 4, 5, 6, 7, 8, 9]
   array1.concat([4, 5], 6) // [1, 2, 3, 4, 5, 6]
 ```
 
 2. `copyWithin(target, start, end)`将指定位置的元素拷贝到另一个指定位置，改变原数组
 
 ```js
   let a1 = [1, 2, 3, 4, 5, 6]
   a1.copyWithin(2) // [1, 2, 1, 4, 5, 6]
   // 将下标3~5且不包含下标5的元素，从下标0开始替换
   a1.copyWithin(0, 3, 5) // [4, 5, 3, 4, 5, 6]
 ```
 
 3. `every((currentValue,index,arr)=> {})`用于检测数组元素是否都符合指定条件（通过函数提供），不对空数组检测，不改变原数组

 ```js
   // 在检测过程中，若遇到不符合条件的元素，则停止检测，直接返回false
   // 全部通过返回true
   let a1 = [1, 2, 3, 4, 5, 6]
   a1.every(value=>{return value > 3}) // false
   a1.every(value=>{return value > 0}) // true
 ```
 
 4. `fill(value, start, end)`用于将一个固定值替换数组的元素，改变原数组

 ```js
   // 这个方法看上去和copyWithin很像，需要注意它们第一个参数的意思不同
   // 一个是传值，一个是传下标
   a1.fill(1,0,2) // [1, 1, 3, 4, 5, 6]
 ```
 
 5. `filter((currentValue,index,arr)=> {})`创建一个新的数组，新数组中的元素是通过检查指定数组中符合条件的所有元素，不对空数组检测，不改变原数组

 ```js
   // 不难看出这个和every()很像，不同的是filter()会对所有的元素进行检测，
   // 且返回的是条件的数组，不是boolean值
   let a1 = [1, 1, 3, 4, 5, 6]
   a1.filter((value) => {return value > 3}) // [4, 5, 6]
 ```
 
 6. `find((currentValue,index,arr)=> {})`找到符合条件的第一个元素并返回该元素的值，没有则返回**undefined**，不对空数组检测，不改变原数组

 ```js
   // 这个也可以和every()做比较，every是遇到第一个不符合的就返回false（布尔值），
   // 而find是遇到第一个符合的就返回该元素（值）了
   let a1 = [1, 1, 3, 4, 5, 6]
   a1.find(value=>{return value > 2}) // 3
 ```
 
 7. `findIndex((currentValue,index,arr)=> {})`找到符合条件的第一个元素并返回该元素的下标，没有则返回**-1**，不对空数组检测，不改变原数组

 ```js
   // 与find相似，只不过返回的是下标
 ```
 
 8. `forEach()`调用数组的每个元素，不对空数组检测，不改变原数组
 
 ```js
   let a1 = [1, 2, 3]
   a1.forEach(value=> console.log(value + 2)) // 依次打印，可以认为没有返回值，可与map()进行对比
 ```
 
 9. `from(object, mapFunction=>{})`将拥有**length**属性的对象或可迭代的对象变成一个数组

 ```js
   Array.from("123") // ["1", "2", "3"]
   Array.from("123",value => value*2) // [2, 4, 6] 这里有强制转换
   Array.from([1,2,3],value => value*2) // [2, 4, 6]
 ``` 
 
 10. `includes(searchElement, fromIndex)`判断一个数组是否包含一个指定的值，如果是返回true，否则false

 ```js
   [1, 2, 3].includes(2) // true
   [1, 2, 3].includes(4) // false
   [1, 2, 3].includes(2, 0) // false 第二个参数是下标
 ```
 
 11. `indexOf(item,start)`从某个位置开始检索，start可不传，默认为0，其它类似findIndex

 ```js
   let a1 = [1, 1, 3, 4, 5, 6]
   a1.indexOf(3,1) // 2下标
   a1.indexOf(2,1) // -1
 ```
 
 12. `isArray(obj)`，判断一个对象是否为数组，是数组返回 true，否则返回 false

 ```js
   let a1 = [1, 1, 3, 4, 5, 6]
   Array.isArray(a1) // true
   Array.isArray(123) // false
 ```
 
 13. `join(separator)`把数组中的所有元素转换一个字符串

 ```js
   [1,2,3].join() // 1,2,3 默认加,
   [1,2,3].join(' or ') // 1 or 2 or 3
 ```
 
 14. `lastIndexOf()`，与`indexOf`相似，只不过从后向前搜索
 
 15. `map((currentValue,index,arr)=> {})`返回调用函数处理后的值，不对空数组检测，不改变原数组

 ```js
   // forEach返回的是一个一个的，map返回数组
   [1,2,3].map(value=>{return value*2}) // [2, 4, 6] 
 ```
 
 16. `pop()`删除数组的最后一个元素并返回删除的元素，`shift()`删除数组的第一个元素并返回删除的元素

 17. `push()`向数组的末尾添加一个或多个元素，类比`concat()`，`unshift()`向数组的开头添加一个或更多元素

 18. `reduce((total, currentValue, currentIndex, arr)=>{})`作为累加器，`reduceRight()`同样作为累加器，从末尾向前，都不改变原数组
 
 ```js
   [1,2,3].reduce((total,value)=>{return total + value}) // 6
 ```
 
 19. `reverse()`数组反转

 ```js
   [1,2,3].reverse() // [3, 2, 1]
 ```
 
 20. `slice(startIndex,endIndex)`截取数组中的一部分，并返回，不改变原数组

 ```js
   [1,2,3,4,5,6].slice(2,5) // [3, 4, 5] 下标是[2,5)包含2不包含5，即截取下标2~4的元素
 ```
 
 21. `some((currentValue,index,arr)=> {})`检测数组中的元素是否满足指定条件，不对空数组检测，不改变原数组

 ```js
   // 是不是又联想到every，不同的是some遇到第一个符合条件的即返回true，后边的不再执行，刚好相反哈。
   // 若没有满足的则返回false
   let a1 = [1, 2, 3, 4, 5, 6]
   a1.some(value=>{return value > 5}) // true
   a1.some(value=>{return value > 6}) // false
 ```
 
 22. `sort()`对数组的元素进行排序，类比`reverse()`
 
 23. `splice(index,howmany,item1,.....,itemX)`插入、删除或替换数组的元素，改变原始数组
 
 ```js
   // 要是只是前面的两个参数，可以类比slice，不过splice第二个是个数，不是下标
   let a1 = [1,2,3]
   let b1 = a1.splice(0,1,4,5) // b1 = [1] a1 = [4, 5, 2, 3]
 ```
 
 24. `flat()`将二维数组变为一维数组，不改变原数组

 ```js
   [1, 2, 3, [4, 5]].flat() // [1, 2, 3, 4, 5]
   [1, 2, 3, [4, 5, [6, 7, [8, 9]]]].flat() //  [1, 2, 3, 4, 5, Array(3)] 所以是二维数组
 ```
 
 
 
 
 
 
 
 
 
 
 
 
 
 