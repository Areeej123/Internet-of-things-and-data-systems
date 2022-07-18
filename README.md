<!DOCTYPE html>
<html>
<head>
  <head>
	<title>Speech to text Converter</title>
	<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/4.7.0/css/font-awesome.min.css">
</head>
<body>

</body>
	<h2 align="center">Speech to text converter JavaScript</h2>
	<div id="result"></div>
	<button onclick="startConverting();"><i class="fa fa-microphone btn btn-danger" aria-hidden="true"></i></button>


	<script>
  var result = document.getElementById('result');

		function startConverting () {

		if('webkitSpeechRecognition' in window) {
			var speechRecognizer = new webkitSpeechRecognition();
			speechRecognizer.continuous = true;
			speechRecognizer.interimResults = true;
			speechRecognizer.lang = 'SA-US';
      speechRecognizer.lang = 'US-SA';

			speechRecognizer.start();

			var finalTranscripts = '';

			speechRecognizer.onresult = function(event) {
				var interimTranscripts = '';
				for(var i = event.resultIndex; i < event.results.length; i++){
					var transcript = event.results[i][0].transcript;
					transcript.replace("\n", "<br>");
					if(event.results[i].isFinal) {
						finalTranscripts += transcript;
					}else{
						interimTranscripts += transcript;
					}
				}
				result.innerHTML = finalTranscripts + '<span style="color: #999">' + interimTranscripts + '</span>';
			};
			speechRecognizer.onerror = function (event) {

			};
		}else {
			result.innerHTML = 'Your browser is not supported. Please download Google chrome or Update your Google chrome!!';
		}
		}
  	</script>
</body>
</html>
