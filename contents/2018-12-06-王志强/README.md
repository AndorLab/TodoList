```typescript
// 为函数定义类型
let sum = function (x: number, y: number): number {
	return x + y;
}

// 完整的函数类型
let sums: (baseValue: number, increment: number) => number = 
	function (x, y) { return x + y; }

// 一般的判断函数
function handleFn ( x: number | string ): number | string {
	if ( typeof x === 'number') {
		console.log(x.toFixed(2));
	} else if ( typeof x === 'string' ) {
		console.log(x.split(''));
	}
	return x;
}

/**
 * 函数重载，
 * 先定义；最后实现；
 * 最后实现的时候可以省略参数类型；编译器可以通过上下文推论来确认参数的类型
 * */
function handle1Fn( x: number ): number;
function handle1Fn( x: string): string;
function handle1Fn(x): any {
	if ( typeof x === 'number') {
		console.log(x.toFixed(2));
	} else if ( typeof x === 'string' ) {
		console.log(x.split(''));
	}
	return x;
}

// 泛型
function genericFn<T>(name: T): T {
	return name;
}
genericFn(1)

// 这种方式是否可以当做泛型
function genericFn1<T>(name: T): number[] {
	return [1,2,2];
}
genericFn1(1)

// 泛型类型
function genericFn2<T>(name: T): T {
	return name;
}
let generic2: <T>(name: T) => T = genericFn2;
genericFn2(4)

// 用对象字面量替代 => 来定义泛型函数
function genericFn3<T>(name: T): T {
	return name;
}
let generic3: {<T>(name: T): T} = genericFn3;

// 泛型接口
interface int {
  <action>(action: number): number
}
function people<T>(action: T): T {
	return action;
}
let p: {} = people;


// 泛型类
class Int<T> {
  val: T;
  sum: (x: T,y: T) => string = function (x, y) {
    return x.toString() + y.toString()
  }
}
let s = new Int<number>();
s.val = 1;
s.sum(1,2) 


// 泛型约束
interface Lengthwise {
	length: number;
}
function loggingFn<T extends Lengthwise> (name:  T) : T {
	console.log(name.length);
	return name;
}


// 数字枚举 ==》 正向映射与反向映射
enum N {
	x,
  y
}
N.x;
N[0];

// 字符串枚举 ==》 正向映射
enum F {
	x = 'X',
  y = 'Y'
}
// todo 枚举和类的静态变量使用场景
F.x;

// 运行时的枚举
enum E {
	x, y
}
function f( obj: {x: number, y: number}) {
	console.log(obj.y);
	return obj.x;
}
f(E)
```
