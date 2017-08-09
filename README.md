var a = "";
var b = "";
var c = "";
var key = "bc382dda3db928e28b90e736a3731201";
var step = 0;


function toDataURL(src, callback, outputFormat) {
  var img = new Image();
  img.crossOrigin = 'Anonymous';
  img.onload = function() {
    var canvas = document.createElement('CANVAS');
    var ctx = canvas.getContext('2d');
    var dataURL;
    canvas.height = this.naturalHeight;
    canvas.width = this.naturalWidth;
    ctx.drawImage(this, 0, 0);
    dataURL = canvas.toDataURL(outputFormat);
    callback(dataURL);
  };
  img.src = src;
  if (img.complete || img.complete === undefined) {
    img.src = "data:image/png;base64,R0lGODlhAQABAIAAAAAAAP///ywAAAAAAQABAAACAUwAOw==";
    img.src = src;
  }
}



function sendCap(url){
  var xhr = new XMLHttpRequest();
  xhr.open("POST", 'https://2captcha.com/in.php', true);

  //Send the proper header information along with the request
  xhr.setRequestHeader("Content-type", "application/x-www-form-urlencoded");

  xhr.onreadystatechange = function() {//Call a function when the state changes.
      if(xhr.readyState == XMLHttpRequest.DONE && xhr.status == 200) {
          b = xhr.responseText;
      }
  }
  xhr.responseType = 'blob';
  xhr.send("file="+url+"&key="+key+"&header_acao=1"+"&method=base64");
}
setInterval(function(){
  	if(a==""){
    	if(step==0){
			a = document.getElementById("captchasnet_free_play_captcha").getElementsByTagName("img")[0].src;
    	}
	}else{
    	
    	if(step==0){
        	toDataURL(a,function(dataUrl) {c = dataUrl;})
        	//sendCap(a);
            step = 1;
        }
    	if(step == 1 ){
        	toDataURL(
  'https://captchas.freebitco.in/cgi-bin/captcha_generator?client=freebitcoin&random=biIG5YJATPx1GzrUXzT13zoWNEfdddkk.png',
  function(dataUrl) {

    console.log('RESULT:', dataUrl)
  }
)
        }
    }
},1000);
