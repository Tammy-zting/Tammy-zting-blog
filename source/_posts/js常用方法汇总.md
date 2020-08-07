---
title: js常用方法汇总
date: 2020-08-03 16:19:41
tags:
---
# 数组常用方法
##  forEach
##  every 用来判断所有的数组元素都满足一个条件才返回true
##  some 用来判断数组元素中一个元素满足一个条件即返回true
##  sort 排序
##  find()
(ES6 新增) 用来查找目标元素，找到就返回该元素，找不到返回 undefined
- 语法：arr.find(callback(element index array),thisArg]) 
- 参数： 
    - callback 在数组每一项上执行的函数，接收 3 个参数 element:当前遍历到的元素 
    - index:可选 当前遍历到的索引 
    - array:可选 数组本身 
    - thisArg 可选。指定 callback 的 this 参数。 
    返回值：当某个元素通过 callback 的测试时，返回数组中的一个值，否则返回 undefined。

## findIndex()
ES6 新增) 方法返回数组中满足提供的测试函数的第一个元素的索引。否则返回-1
- 语法：arr.findIndex(callback(element index array),thisArg]) 
- 参数： 
    - callback 在数组每一项上执行的函数，接收 3 个参数 element:当前遍历到的元素 
    - index:可选 当前遍历到的索引 
    - array:可选 数组本身 
    - thisArg 可选。指定 callback 的 this 参数。 
    返回值：返回数组中满足提供的测试函数的第一个元素的索引。否则返回-1。

##  map 返回一个重新拼装的数组

		var arr =[1,2,3,4,5]

		arr.forEach(function(item,index){....})

		//注意：forEach如果遍历的是对象参数则为function(key,value)

		var result=arr.every(function(item,index){
			if(item <6){
				return true
			}
		})//result true
		
		var result=arr.some(function(item,index){
			if(item === 5){
				return true
			}
		})//result true

		var arr2=arr.sort(function(a,b){
			//从大到小排序
			return b-a
		}) 

		var arr3=arr.map(function(item,index){
			return '<b>'+ item +'</b>'
		})

##  forEach提升，写一个能遍历对象和数组的forEach函数
	
		function forEach(obj,fn){
			var key
			if(obj instanceof Array){
				obj.forEach(function(item,index){
					fn(index,item)
				})
			}else{
				for(key in obj){
					fn(key,obj[key])
				}
			}
		
		}

		var arr=[1,2,3]
		forEach(arr,function(index,item){
			console.log(index,item)
		})
		var obj={x:1,y:2}
		forEach(obj,function(key,val){
			console.log(key,val)
		})
##  reduce() 对数组中的元素依次处理，将上次处理结果作为下次处理的输入，最后得到最终结果。
##  pop() 删除数组末尾元素并返回元素 
##  shift() 删除数组最前面的元素并返回删除的元素
##  unshift() 添加元素到数组头部并返回新数组的长度
##  indexOf() 找元素索引  返回 索引 / ## 1表示找不到
##  includes() 找某个元素 返回 true / false
##  splice(pos,n,...) 通过索引pos删除n个或者添加多个元素...
##  slice() 复制数组
##  concat()将元素连接到数组中
##  join() 将数组元素以逗号连接成字符串
##  reverse() 颠倒数组中的元素
##  fill()
用一个固定值填充一个数组中从起始索引到终止索引内的全部元素
- 语法：Arr.fill(value, start, end)
- 参数：
    - value:用来填充数组元素的值
    - start:可选 起始索引，默认值为 0
    - end:可选 终止索引，默认值为 this.length。
    返回值：修改后的原数组。

## filter()
创建一个新数组, 其包含通过所提供函数实现的测试的所有元素
- 语法：arr.filter(callback(element index array),thisArg]) 
- 参数： 
    - callback 用来测试数组的每个元素的函数。调用时使用参数 (element, index, array)。返回 true 表示保留该元素（通过测试），false 则不保留。它接受三个参数 - - - element:当前在数组中处理的元素 
    - index:可选 正在处理元素在数组中的索引 
    - array:可选 调用了 filter 筛选器的数组 
    - thisArg 可选。执行 callback 时的用于 this 的值。 
    返回值：一个新的通过测试的元素的集合的数组，如果没有通过测试则返回空数组

## from()
(ES6 新增) from() 方法用于通过拥有 length = - 属性的对象或可迭代的对象来返回一个数组。如果对象是数组返回 true，否则返回 false。
- 语法：Array.from(object, mapFunction, thisValue) 
- 参数： 
    - object:必需，要转换为数组的对象。 
    - mapFunction:可选，数组中每个元素要调用的函数。 
    - thisValue:可选，映射函数(mapFunction)中的 this 对象。 
    - 返回值：对象是数组返回 true，否则返回 false

# 常用Math函数
## Math.round()  “四舍五入”， 该函数返回的是一个四舍五入后的的整数
## Math.ceil()  “向上取整”， 即小数部分直接舍去，并向正数部分进1
## Math.floor()  “向下取整” ，即小数部分直接舍去