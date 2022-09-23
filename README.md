# img-qing
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8" />
		<title>简单画布</title>
	</head>
	<body>
		<!-- <center></center>表示将标签内所有的内容居中 -->
		<center>
			<canvas id="cavsElem" >你的游览器不支持canvas，请升级游览器！</canvas><br>
			画笔颜色：<input type="color" id="col" />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
			画笔粗细：<input type="range" min="1" id="rag" max="20" />
		</center>
		<script>
			//函数或者方法的自我调用
			(function(){
				//获得画布
				var canvas=document.getElementById('cavsElem');
				//准备画笔（获取上下文对象）
				var context=canvas.getContext('2d');
				//设置标签的宽度和边框
				canvas.width=900;
				canvas.height=600;
				canvas.style.border="1px solid #000";
				//笔触颜色、粗细对象化，运用全局变量
				c=document.getElementById('col');
				r=document.getElementById('rag');
				/*当鼠标按下触发onmousedown事件时，定义一个函数获取鼠标起始坐标，
				具体方法为鼠标当前在游览器的坐标减去画布所在原点相对于游览器当前的位置坐标，以获得在画布内的坐标，下同*/
				canvas.onmousedown=function(event){
					var x=event.clientX-canvas.getBoundingClientRect().left;
					var y=event.clientY-canvas.getBoundingClientRect().top;
					context.beginPath();//开始规划路径
					context.moveTo(x,y);//移动的起点
					//当鼠标移动触发onmousemove事件时，定义一个函数获取绘制线条的坐标
					canvas.onmousemove=function(event){
						var x=event.clientX-canvas.getBoundingClientRect().left;
						var y=event.clientY-canvas.getBoundingClientRect().top;
						context.lineTo(x,y);//绘制线条
						context.strokeStyle=c.value;//设置画笔颜色
						context.lineWidth=r.value;//设置画笔粗细
						context.stroke();//绘制描边
					};
					canvas.onmouseup=function(event){
						canvas.onmousemove=null;
					};
				};
			})();
		</script>
	</body>
</html>
