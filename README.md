<!DOCTYPE html>
<html>
	
	<head>
		<meta charset="utf-8">
		<title>Greek mythology quizz</title>
	</head>
		
	<body>
			<section>
			</section>
			<input id="textInput" type="text">
			<button id="click">submit</button>
			
			<p id="yesNo"></p>
			
		<script>
		const section = document.querySelector('section');
		var requestURL= 'http://192.168.1.62/quizz/greek_myth_data.json';
		var request = new XMLHttpRequest();
		var score = 0
		var button = document.getElementById("click")
		var yesOrNo = document.getElementById("yesNo")
		
		request.open('GET', requestURL);
		request.responseType = 'json';
		request.send();
		
		function randomNumFunc(maxi) {
			return Math.floor(Math.random() * maxi)
		}
		
		request.onload = function() {
			var caracters = request.response;
			populateSection(caracters);
		}
		function populateSection(jsonObj) {
			var randomCaracter = randomNumFunc(jsonObj['caracters'].length);
			caracter = Object.getOwnPropertyNames(jsonObj['caracters'][randomCaracter])
			var randomRelation = caracter[randomNumFunc(caracter.length)];
			
			if(randomRelation === "name") {
				while(randomRelation === "name") {
					var randomRelation = caracter[randomNumFunc(caracter.length)];
					
				}
			}
			
			var answer = jsonObj['caracters'][randomCaracter][randomRelation];
			var myPara = document.createElement('p');
			myPara.textContent = "Who is the " + randomRelation + " of " + jsonObj['caracters'][randomCaracter].name + "?";
			section.appendChild(myPara);
			function myFunc() {
				var txtBox = document.getElementById("textInput").value;
				if(txtBox === answer) {
					score ++
					yesOrNo.textContent = "Bravo! Score: " +score
				} else {
					yesOrNo.textContent = "Try again!  It was " + answer + ". Score: " + score
				}
				randomCaracter = randomNumFunc(jsonObj['caracters'].length);
				caracter = Object.getOwnPropertyNames(jsonObj['caracters'][randomCaracter])
				randomRelation = caracter[randomNumFunc(caracter.length)];
				
				if(randomRelation === "name") {
					while(randomRelation === "name") {
						var randomRelation = caracter[randomNumFunc(caracter.length)];
						
					}
				}
				answer = jsonObj['caracters'][randomCaracter][randomRelation];
				
				oldPara = document.querySelector('p')
				var myPara = document.createElement('p');
				myPara.textContent = "Who is the " + randomRelation + " of " + jsonObj['caracters'][randomCaracter].name + "?";
				section.replaceChild(myPara, oldPara);
				console.log(answer)
			}
			button.addEventListener("click", myFunc);
		}
	</script>

		</body>
</html>
