Hello Guys,
This is my first Repo.
I hope you like it.
The code file is given as .htm extension.
<!DOCTYPE html>
<html>
<head>
	<title>Game</title>
</head>
<body>
	<canvas id ="gameCanvas" width=screen.availWidth; height=window.innerHieght;></canvas>

<script type="text/javascript">

    var x = 100;
    var ballSpeedX = -2;
    var y = 100;
    var ballSpeedY = -2;
    var paddle2Y = 100;
    var paddleY;
    const PADDLE_HIEGHT = 70;
    const help = 10;
    var score1 = 0;
    var score2 = 0;
    var winScore = 20;
    var winScreen = false;

	var canvas;
	var canvasContext;
	window.onload = function(){
		canvas = document.getElementById("gameCanvas");
		canvasContext = canvas.getContext("2d");
		ballReset();
		drawNet();
		canvas.width *= 4.07;
		canvas.height *= 3.5;
	    setInterval(drawEverything,0.0001);

	    canvas.addEventListener('mousedown',handleMouseClick);

	    canvas.addEventListener('mousemove',
	    	function(evt){
			var mousepos = calculateMousePos(evt);
			paddleY = mousepos.y;
		    })
	}
	function drawEverything(){
		if(winScreen)
		{
			canvasContext.fillText("Click Here To Continue",canvas.width*0.4,canvas.height/2 + 100);
			winScreenFunction();
			return;
		}
		drawBackground();
		drawConsoles();
		drawBall();
		score();
	}
	function score()
	{
		           canvasContext.font="30px Verdana";
                   // Create gradient
                   var gradient=canvasContext.createLinearGradient(0,0,canvas.width,0);
                   gradient.addColorStop("0","magenta");
                   gradient.addColorStop("0.5","blue");
                   gradient.addColorStop("1.0","red");
                   // Fill with gradient
                   canvasContext.fillStyle=gradient;
		canvasContext.fillText(score1,canvas.width*0.1,100);
		canvasContext.fillText(score2,canvas.width*0.9,100);
		if(score2 == winScore || score1 == winScore)
		{
			winScreen = true;
		}
	}
	function drawBall()
	{
		canvasContext.fillStyle = "red";
			x = x + ballSpeedX;
			if (x >= canvas.width - 24) 
			{
				if(y > paddle2Y - help && y < paddle2Y + PADDLE_HIEGHT + help){
					score2 += 10;
				ballSpeedX = -ballSpeedX;	
				}
				else{
					ballReset();
					scoreReset();
				}
				//ballSpeedX = ballSpeedX - 0.2;
			}
			if (x < 24) 
			{
				if(y > paddleY - help && y < paddleY + PADDLE_HIEGHT + help){
					score1 += 10;
				ballSpeedX = -ballSpeedX;	
				}
				else{
					ballReset();
					scoreReset();
				}
				//ballSpeedX = ballSpeedX + 0.2;
			}
			y = y + ballSpeedY;
			if (y >= canvas.height) 
			{
				ballSpeedY = -ballSpeedY;
				//ballSpeedX = ballSpeedX - 0.2;
			}
			if (y < 0) 
			{
				ballSpeedY = -ballSpeedY;
				//ballSpeedX = ballSpeedX + 0.2;
			}
			canvasContext.beginPath();
            paddle2Y = y - 10;
			canvasContext.arc(x,y,10,0,Math.PI*2,true);
			canvasContext.fill();
	}
	function calculateMousePos(evt)
	{
		var rect = canvas.getBoundingClientRect();
		var root = document.documentElement;
		var mouseX = evt.clientX - rect.left - root.scrollLeft - 10;
		var mouseY = evt.clientY - rect.top - root.scrollTop;
		return{
			x : mouseX,
			y : mouseY
		};
	}
	function drawBackground()
	{
		canvasContext.fillStyle = "black";
		canvasContext.fillRect(0,0,canvas.width,canvas.height);
		drawNet();
	}
	function drawConsoles()
	{
		canvasContext.fillStyle = "white";
		canvasContext.fillRect(20,paddleY,3,PADDLE_HIEGHT);

		canvasContext.fillStyle = "white";
		canvasContext.fillRect(canvas.width-20,paddle2Y,3,PADDLE_HIEGHT);	
	}
	function scoreReset()
	{
		score1 = 0;
		score2 = 0;
	}
	function ballReset(){
		x = canvas.width/2;
		y = canvas.height/2;
	}

	function winScreenFunction()
	{
		if(score2 == winScore)
		{
			winScreen = true;
			machineWin();
			scoreReset();
		}
	    if (score1 == winScore) 
		{
			winScreen = true;
			playerWin();
			scoreReset();
		}
	}
	function machineWin()
	{
		           canvasContext.font="30px Verdana";
                   // Create gradient
                   var gradient=canvasContext.createLinearGradient(0,0,canvas.width,0);
                   gradient.addColorStop("0","magenta");
                   gradient.addColorStop("0.5","blue");
                   gradient.addColorStop("1.0","red");
                   // Fill with gradient
                   canvasContext.fillStyle=gradient;
		canvasContext.fillText("Machine WON!!!",canvas.width*0.4,canvas.height/2);
	}
	function playerWin()
	{
		           canvasContext.font="30px Verdana";
                   // Create gradient
                   var gradient=canvasContext.createLinearGradient(0,0,canvas.width,0);
                   gradient.addColorStop("0","magenta");
                   gradient.addColorStop("0.5","blue");
                   gradient.addColorStop("1.0","red");
                   // Fill with gradient
                   canvasContext.fillStyle=gradient;
		canvasContext.fillText("You WON :-)",canvas.width*0.4,canvas.height/2);
	}
	function handleMouseClick(evt)
	{
		if(winScreen)
		{
			scoreReset();
			winScreen = false;
		}
	}
	function drawNet()
	{
		for(var i=0; i < canvas.height; i+=40)
		{
			canvasContext.fillStyle = "white";
			canvasContext.fillRect(canvas.width/2-1,i,2,20);
		}
	}
</script>
</body>
</html>
