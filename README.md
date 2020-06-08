
# reddit_subscriber

to transfer your subscriptions to a fresh account

1. open the console and run the following function on https://www.reddit.com/subreddits/mine/  
this will create urls of all your subs in chunks of 100 (url musn't be too long)

	    (function () {
	        var multiredditElement = document.querySelector(".subscription-box ul>a");
	        if ( multiredditElement ) {

	            var href = multiredditElement.getAttribute("href");
	            var subreddits = href && href.split("/r/");
	            if ( subreddits && typeof subreddits[1] !== "undefined" ) {
	                var a_subreddits = subreddits[1].split("+");
	                while ( a_subreddits.length ) {
	                    var hundred = a_subreddits.splice(0, 100);

	                    console.log( "https://www.reddit.com/r/" + hundred.join("+") );
	                }
	            }
	        }
	    })();


2. log into your new account
if you don't get a new IP/clear ALL site cookies before switching accounts reddit WILL link them


3. goto each url logged by previous function and run the following on each:

	    (function () {
	        var a = document.querySelectorAll(".subscribe-button a.add.active");
	        var i = 0;
	        var int = 0;
	        int = setInterval(function () {
	            var el = a[i++];
	            if (!el) {
	                alert("done subscribing to " +(--i)+ " subs");
	                clearInterval(int);
	            } else {
	                var sub = el.parentNode.getAttribute("data-sr_name");
	                console.log("subscribed to " + sub);
	                $(el).click();
	            }
	        }, 500);
	    })();


4.  success!

