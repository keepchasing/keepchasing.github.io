---
layout:     post
title:      "数字转大写汉字"
subtitle:   "支持千万亿单位"
date:       2017-06-28 12:00:00
author:     "the Little Prince"
header-img: "img/post-bg.jpg"
catalog: true
navbarClass: ""
tags:
    - js
---

```

let tiles = ['零','一','二','三','四','五','六','七','八','九']
let units = [
	['','十','百','千'],
	['万','十','百','千'],
	['亿','十','百','千'],
	['万亿','十','百','千']
]
function num2zh (num) {

	if(isNaN(Number(num))) {
		return num;
	}
	num = parseInt(num);
	if(num === 0)
	{
		return '零';
	}
	let reverseNumArr = (num+'').split('').reverse();
	let numArr = [];
	reverseNumArr.map((val,index) => {
		index%4 === 0? numArr.push([]): ''
		numArr[numArr.length -1][index%4] = Number(val);
	})

	let subTrans = (reverseNumArr,i) => {
		// 去除四位数前边的0
		for(let j = 3; j>= 0; j--)
		{
			if(reverseNumArr[j] === 0){
				reverseNumArr.pop();
			}
			else{
				j = -1;
				break;
			}
		}
		// 四位数都为零返回空
		if(reverseNumArr.length === 0)
		{
			return '';
		}
		// 转换一个小于等于四位数的数字
		let zhStr = reverseNumArr.reduce((res,cur,index,reverseNumArr) => {
			let maxIndex = reverseNumArr.length - 1;
			if(cur == 0)
			{
				if(index == maxIndex || index === 0)
				{
					if(index == 0)
					{
						res = units[i][index]+ res;
					}
					return res;
				}
				else{
					if(reverseNumArr[index - 1] == 0)
					{
						return res;
					}
					else{
						return res = tiles[cur] + res;
					}
				}
				
			}
			else{
				return res = tiles[cur]+units[i][index] + res;
			}
		},'')
		return zhStr;
	}
	
	let result = (numArr.reduce((res,cur,i,numArr) => {
		let subRes = subTrans(cur,i);
		// 判断多个四位数中间是否需要‘零’连接
		if(i < numArr.length - 1  && subRes && (cur[3] === 0 || numArr[i + 1][0] === 0))
		{
			subRes = '零' + subRes;
		}
		return res = subRes + res
	},''))
	result = num >= 10 && num < 20? result.substring(1): result; // 处理10到二十之间的数
	return result;
}

console.log(num2zh('qewq23')) // qewq23
console.log(num2zh(0)) // 零
console.log(num2zh(13))  // 十三
console.log(num2zh(504)) // 五百零四
console.log(num2zh(9000)) // 九千
console.log(num2zh(12000001)) // 一千二百万零一
console.log(num2zh(120239011))  // 一亿二千零二十三万九千零一十一
console.log(num2zh(790000000001)) // 七千九百亿零一
console.log(num2zh(790001000001)) // 七千九百亿零一百万零一
console.log(num2zh(123456789123)) // 一千二百三十四亿五千六百七十八万九千一百二十三

```