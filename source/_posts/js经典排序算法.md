---
title: js经典排序算法
date: 2020-08-03 15:05:14
---
# 冒泡排序

思路
1. 外层循环，从最大值开始递减，因为内层是两两比较，因此最外层当>=2时即可停止；
1. 内层是两两比较，从0开始，比较inner与inner+1，因此，临界条件是inner<outer -1

    ```
    function bubleSort(arr){
        let len = arr.length
        for(let i = len;i >= 2 ; i--){
            for(let j = 0 ;j <= i - 1;j++){
                if(arr[j] > arr[j+1]){
                    //传统写法
                    // let temp = arr[inner];
                    // arr[inner] = arr[inner + 1]
                    // arr[inner + 1] = temp;
                    [arr[j],arr[j+1]]= [arr[j+1],arr[j]]
                }
            }
        return arr
    }
    ```

    ![](https://note.youdao.com/yws/api/personal/file/9D56FADF8ECC4E62B007176FE7B9364B?method=download&shareKey=762262b91d9bb703f0f0b2d34eb25202)

# 选择排序

思路：每一次待排序的数组选择最大（最小）的一个元素作为首元素，直到排完为止

    ```
    function selectSort(arr){
        let len = arr.length;
        for(let i = 0;i<len-1;i++){
            for(let j = i+1;j<len;j++){
                if(arr[i] > arr[j]){
                    [arr[i],arr[j]]=[arr[j],arr[i]]
                }
            }
        }
    }
    ```
![](https://note.youdao.com/yws/api/personal/file/6575CF271AE84CDA9563368BBF6F4DC4?method=download&shareKey=9bf6a129848f1bda9ea9dd7a254862de)

# 插入排序

思路：第一个元素作为已经排序的，取下一个元素，在已经排序的元素序列中从后往前扫描

    ```
    function insertSort(arr) {
        let len = arr.length
        for(let i = 1;i < len; i++){
            for(let j = i;j > 0;j--){  //往前查找
                if(arr[j] < arr[j-1]){
                    [arr[j],arr[j-1]] = [arr[j-1],arr[j]]
                }
            }
        }
    }
    ```
![](https://note.youdao.com/yws/api/personal/file/4611597EE12E428A8D6598ABE6341D61?method=download&shareKey=3f16e37d37c88bad2a39e790db6da1ff)

# 快速排序

思路
1. 选择一个基准元素，将列表分割成两个子序列；
1. 对列表重新排序，将所有小于基准值的元素放在基准值前面，所有大于基准值的元素放在基准值的后面
1. 分别对较小元素的子序列和较大元素的子序列重复步骤1和2

    ```
    function quickSort(arr){
        if(arr.length <= 1){
            return arr
        }
        let left = [],right = [];
        let current =  arr.splice(0,1)//注意splice后，数组长度少了一个
        for(let i = 0 ;i<arr.length;i++){
            if(arr[i]< current){
                left.push(arr[i])
            }else{
                right.push(arr[i])
            }
        }
        return quickSort(left).concat(current,quickSort(right))
    }
    ```

     ![](https://note.youdao.com/yws/api/personal/file/D10E41DC761D4999B09C575F29A37362?method=download&shareKey=6a30ffd45a6debf0d5a82c6bd4d54478)

# 常用Math函数
## Math.round()  “四舍五入”， 该函数返回的是一个四舍五入后的的整数
## Math.ceil()  “向上取整”， 即小数部分直接舍去，并向正数部分进1
## Math.floor()  “向下取整” ，即小数部分直接舍去