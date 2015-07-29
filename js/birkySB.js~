// Rachael Birky
// CMSC 433
// Javascript: Shoutbox

$(function() {
    $( "#format" ).buttonset();
});

var emotes = {"0:-)":'<img src="img/face-angel.png" alt="angel" />',
	      ":'(":'<img src="img/face-crying.png" alt="crying" />',
	      ">:-)":'<img src="img/face-devilish.png" alt="devilish" />',
	      "B-)":'<img src="img/face-glasses.png" alt="glasses" />',
	      ":D":'<img src="img/face-grin.png" alt="grin" />',
	      ":~*":'<img src="img/face-kiss.png" alt="kiss" />',
	      ":-(|)":'<img src="img/face-monkey.png" alt="monkey" />',
	      ":-|":'<img src="img/face-plain.png" alt="plain" />',
	      ":-(":'<img src="img/face-sad.png" alt="sad" />',
	      ":-D":'<img src="img/face-smile-big.png" alt="smile-big" />',
	      ":-)":'<img src="img/face-smile.png" alt="smile" />',
	      ":-0":'<img src="img/face-surprise.png" alt="surprise" />',
	      ";-)":'<img src="img/face-wink.png" alt="wink" />'
	     };

function parseMsg(msg){
    for (emote in emotes) {
	msg = msg.replace(emote, emotes[emote]);
    }
    return msg;
}

// AJAX GET
function ajaxGET(){
    $('#messages').html("");
    $.get("server/shout.php", function(data){
	var msgString = "";
	var arr = data.data;
	for (var i=arr.length-1; i>=0; i--){
	    var obj = arr[i];
	    var newMessage = parseMsg(obj.message);
	    msgString += "<div class='shout'><span class='timestamp'>["+obj.time+"]</span><span class='name'> "+obj.name+"</span>:<span style=message'> "+newMessage+"</span></div>";	    
	}
	$('#messages').append(msgString);
    div = document.getElementById("messages");
    div.scrollTop = div.scrollHeight;
    })
	.fail(function(){
	    alert("There was an error contacting the server");
	});

}

function clearMsg(){
    var message = document.getElementById("message");
    message.value = "";
    message.focus();
}

function sendMsg(){
    var name = document.getElementById("name");
    var message = document.getElementById("message");
    if (message.value == "" || name.value == ""){
	alert("Please enter a name and message");
    } else {
	var expireDate = new Date();
	expireDate.setDate(expireDate.getDate() + (365 * 10));
	var date = new Date();
	var time = date.toDateString() +" "+ date.toLocaleTimeString();
	$.cookie("name2", name.value, { expires: expireDate });
	var jsonObj = {"name":name.value, "message":message.value, "time":time};
	$.ajax({
	    type: "POST",
	    url: "server/shout.php",
	    data: jsonObj
	})
	    .done(ajaxGET)
	    .fail(function() {
		alert( "There was an error sending your message" );
	    });
	message.value="";
	message.focus();
    }
}



// Button variables
var clearButton = document.getElementById("clearButton");
var sendButton = document.getElementById("sendButton");

// Button event handlers
clearButton.onclick = clearMsg;
sendButton.onclick = sendMsg;

// Check for Cookie
var val = $.cookie("name2");

if (val) {
    document.getElementById("name").value = $.cookie("name2");
} else {
    document.getElementById("name").value = "";
}

ajaxGET();
// Update div periodically
setInterval(ajaxGET,15000);

// Emoticons
$('img[alt="angel"]').click(function(){
    $('#message').val($('#message').val() + " 0:-) ");
    $('#message').focus();
})
$('img[alt="crying"]').click(function(){
    $('#message').val($('#message').val() + " :'( ");
    $('#message').focus();
})
$('img[alt="devilish"]').click(function(){
    $('#message').val($('#message').val() + " >:-) ");
    $('#message').focus();
})
$('img[alt="glasses"]').click(function(){
    $('#message').val($('#message').val() + " B-) ");
    $('#message').focus();
})
$('img[alt="grin"]').click(function(){
    $('#message').val($('#message').val() + " :D ");
    $('#message').focus();
})
$('img[alt="kiss"]').click(function(){
    $('#message').val($('#message').val() + " :~* ");
    $('#message').focus();
})
$('img[alt="monkey"]').click(function(){
    $('#message').val($('#message').val() + " :-(|) ");
    $('#message').focus();
})
$('img[alt="plain"]').click(function(){
    $('#message').val($('#message').val() + " :-| ");
    $('#message').focus();
})
$('img[alt="sad"]').click(function(){
    $('#message').val($('#message').val() + " :-( ");
    $('#message').focus();
})
$('img[alt="smile-big"]').click(function(){
    $('#message').val($('#message').val() + " :-D ");
    $('#message').focus();
})
$('img[alt="smile"]').click(function(){
    $('#message').val($('#message').val() + " :-) ");
    $('#message').focus();
})
$('img[alt="surprise"]').click(function(){
    $('#message').val($('#message').val() + " :-0 ");
    $('#message').focus();
})
$('img[alt="wink"]').click(function(){
    $('#message').val($('#message').val() + " ;-) ");
    $('#message').focus();
})

$('#bold').click(function(event){
event.preventDefault();
    var msg = $('#message').val();
    var selec = $('#message').selection();
    var repl = "<b>" + $('#message').selection() + "</b>";
    var fin = msg.replace(selec,repl);
    $('#message').val(fin);
    $('#message').focus();
});

$('#italic').click(function(event){
event.preventDefault();
    var msg = $('#message').val();
    var selec = $('#message').selection();
    var repl = "<i>" + $('#message').selection() + "</i>";
    var fin = msg.replace(selec,repl);
    $('#message').val(fin);
    $('#message').focus();
});

$('#underline').click(function(event){
event.preventDefault();
    var msg = $('#message').val();
    var selec = $('#message').selection();
    var repl = "<u>" + $('#message').selection() + "</u>";
    var fin = msg.replace(selec,repl);
    $('#message').val(fin);
    $('#message').focus();
});

$(document).keypress(function(e) {
    if(e.which == 13) {
    e.preventDefault();
        sendMsg();
    }
});
