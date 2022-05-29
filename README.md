# How to transfer your subscriptions to a fresh account

1. With your old account open https://old.reddit.com/subreddits/mine/ and run (copy paste + enter) the following function in the [browser console](https://support.optimizely.com/hc/en-us/articles/4410284097549-Open-the-developer-console). This will output urls of all your subs in chunks of 100 (url mustn't be too long). Best you copy (right click > copy link location) paste the urls into a text document and close the tab.

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


2. [Clear](https://addons.mozilla.org/en-US/firefox/addon/cookie-quick-manager/) all reddit cookies/storage and get a new IP (via your router interface or just power off the router). If you skip this reddit WILL connect your accounts (internally)


3. Log into your new account, go to each url logged by previous function and run the following function on each. You will get notified when you're subbed to all subreddits of the chunk.

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
