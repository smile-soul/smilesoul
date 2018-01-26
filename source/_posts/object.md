---
title: object
tags: JavaScript
categories: 编程语言
date: 2017-09-29 21:52:18
---

### Object属性：
---
1. configurable: true
	* 能否用delete删除属性
	* 能否修改属性的特性
	* 能否把属性修改为访问器属性
2. enumerable: true
	* 能否用for-in循环返回属性（是否可枚举）
3. writable：true
	* 能否修改属性的值
4. value：undefined
	* 包含这个属性的数据
5. Object.defineProperty(obj, 'name', {}) (ES5)

	```
	Object.defineProperty(obj, 'key', {
		enumerable: false,
		configurable: false,
		writable: false,
		value: 'static'
	});
	```
6. Object.defineProperty(obj, {})
	
	```
	const obj = {};
	Object.defineProperties(obj, {
		"property1": {
			value: true,
			writable: true
		},	
		"property2": {
			value: "Hello",
			writable: false
			}
		});	
	
	cosnt obj = {};
	Object.defineProperty(obj, 'key', {});
	Object.getOwnPropertyDescriptor(obj, 'key');			
	// output: Object {
		value: undefined, 
		writable: false, 
		enumerable: false, 
		configurable: false}
		
	// 注意：在这样定义时候，非定义的configurable等为false
	obj.name = 'lty';
	//这样定义的时候，configurable等才为true
	
	```
7. 一旦把configurable设为false，就不能设回成true，即一切配置都不可使用。

---
### 访问器属性
1. configurable: true
	* 能否用delete删除属性
	* 能否修改属性的特性
	* 能否把属性修改为访问器属性
2. enumerable: true
	* 能否用for-in循环返回属性（是否可枚举）
3. get: undefined
	* 读取数据时候调用
4. set：undefined
	* 写入属性时候调用
5. 访问器属性不能直接定义，只能使用Object.defineProperty()来定义
6. 因为 primitive 是 immutable 的,所以赋值分配新的内存,即为写入

	```
		const book = {
			_year: 2004,
			edition: 1,
		}
		Object.defineProperty(book, 'year', {
			get: () => this._year,
			set: newline => {
				if	(newline > 2000) {
					this._year = newline;
					this.edition += 1;
				};
			},
		})
		book.year = 2005;
		console.log(edition);
		// output: 2
	```
7. 浏览器中一般是使用_defineGetter_和_defineSetter_来代替	