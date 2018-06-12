---
layout:     screensaver
title:      "canvas实现动态多边形屏保效果"
subtitle:   ""
date:       2017-03-20 12:00:00
author:     "the Little Prince"
header-img: "img/post-bg.jpg"
catalog: true
navbarClass: ""
tags:
    - js
---

### 代码实现

```
function rnd(n,m){
		return parseInt(Math.random()*(m-n)+n);
	}
	window.onload=function(){
		let oC = document.querySelector('#c1');
		let gc = oC.getContext('2d'); 
		let winW = document.querySelector('.main-content').clientWidth;
		let winH = 500;
		oC.width = winW;
		oC.height = winH;
		const N = 5;
		const M = 10;
		let aPoint = [];
		for(let i = 0;i < N;i++){
			aPoint[i] = {
				x:rnd(0,winW),
				y:rnd(0,winH),
				speedX:rnd(-10,10),
				speedY:rnd(-10,10)
			};
		}
		
		//画点
		for(let i = 0;i < N;i++){
			drawPoint(aPoint[i]);
		}
		let oldArr = [];
		setInterval(() => {
			gc.clearRect(0,0,winW,winH);
			let newStroke = [];
			for(let i = 0; i < N; i++){
				aPoint[i].x += aPoint[i].speedX;
				aPoint[i].y += aPoint[i].speedY;
				if(aPoint[i].x > winW)
				{
					aPoint[i].x = winW;
					aPoint[i].speedX *= -1;
				}
				if(aPoint[i].x < 0)
				{
					aPoint[i].x = 0;
					aPoint[i].speedX *= -1;
				}
				if(aPoint[i].y > winH)
				{
					aPoint[i].y = winH;
					aPoint[i].speedY *= -1;
				}
				if(aPoint[i].y < 0)
				{
					aPoint[i].y = 0;
					aPoint[i].speedY *= -1;
				}
				gc.fillRect(aPoint[i].x,aPoint[i].y,1,1);
				newStroke.push({x:aPoint[i].x,y:aPoint[i].y})
			}
			
			if(oldArr.length > M){
				oldArr.shift();
			}else{
				oldArr.push(newStroke);
			}
			for(let i = 0; i < oldArr.length; i++)
			{
				drawStroke(oldArr[i]);
			}
		}, 16)
		function drawPoint(point){
			gc.fillStyle='#fff';
			gc.fillRect(point.x,point.y,1,1);
		}
		function drawStroke(aPoint){
			gc.beginPath();
			gc.strokeStyle='#fff';
			gc.moveTo(aPoint[0].x,aPoint[0].y);
			let N = aPoint.length;
			for(let i = 1; i < N; i++)
			{
				gc.lineTo(aPoint[i].x,aPoint[i].y);
			}
			gc.closePath();
			gc.stroke();
		}
	};

```



