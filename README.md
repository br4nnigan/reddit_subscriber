# reddit_subscriber

to transfer your subscriptions to a fresh account

1. run following function on https://old.reddit.com/subreddits/mine/
this will create urls or all your subs in chunks of 100 (url mustn't be too long)

        (function () {
            var multiredditElement = document.querySelector(".subscription-box ul>a");
            if ( multiredditElement ) {

                var href = multiredditElement.getAttribute("href");
                var subreddits = href && href.split("/r/");
                if ( subreddits && typeof subreddits[1] !== "undefined" ) {
                    var a_subreddits = subreddits[1].split("+");
                    while ( a_subreddits.length ) {
                        var hundred = a_subreddits.splice(0, 100);

                        console.log( "https://old.reddit.com/r/" + hundred.join("+") );
                    }
                }
            }
        })();


2. log into your new account. If you don't get a new IP/clear ALL site cookies before switching accounts reddit WILL link them


3. goto each url logged by previous function and run the following on each. You will get notified when you're subbed to all subs of the chunk.

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
