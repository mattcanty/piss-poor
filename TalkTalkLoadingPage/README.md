# TalkTalk's Loading Page
I recently signed up to TalkTalk for Fibre broadband. Whilst I've had an entirely detestable router delivery experience, this is all about their 'Loading' page.

## Reproducible Steps
1. Sign up for a TalkTalk product.
2. Make sure you are logged out of `MyAccount`
3. Navigate to [MyAccount Login Page](https://myaccount.talktalk.co.uk/home/dashboard)
4. Enter your login details and click *Log in*

## The Shit Bit
After following the steps above you are taken through this fantastically crap bit of forced advertising. All based on the fictional requirement that it takes a little while to load your profile - what are they doing, pulling it out of a box by hand?

![Exhibit-A](exhibit-a.gif)

## How It Is Done

> "If they aren't pulling your data out of a filling cabinet in the 3rd floor basement, then what are they doing?"

Let us take a little look at the [source code](exhibit-b.html).

If you're quick - not that quick, you have about ten seconds - you can grab the source code before you are redirected to your account. Check out the full source code about if you wish, but the bit we are interested in is here:

```javascript
$(document).ready(function(){
    var timer = 5000;
    if (isiframe == false) {
    $('#outer-box').html('Checking your details...');
    $('#inner').animate({width: '100'}, (timer/3), function() {
        setTimeout(function() {
            $('#outer-box').html('Loading your account settings...');
            window.setInterval(function(){
                $('#outer-box').html('Fetching your bills and usage details...');
                window.setInterval(function(){
                    $('#outer-box').html('Loading your special offers...');
                    window.setInterval(function(){
                        $('#outer-box').html('Preparing your dashboard...');
                    }, 6000);
                }, 6000);
            }, 6000);
        $('#inner').animate({width: '50'}, (timer/1.5), function() {
           $('#inner').animate({width: '25'}, (timer/3), function() {
               $('#inner').animate({width: '10'}, (timer*4), function() {
                   $('#inner').hide();
               });
           });
       });
    }, 3000);
    });

       }
});
```

Oh look at that! It's just a bunch of bleedin' nested calls to `window.setInterval()`.