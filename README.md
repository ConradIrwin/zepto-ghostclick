zepto.ghostclick.js is a Zepto plugin to help avoid
[ghost clicks](https://developers.google.com/mobile/articles/fast_buttons#ghost) in your
touch-oriented web apps.

To use it, simply include it into your page just after `zepto.js`. Then `return false;` at
the end of your `'tap'` handlers to prevent duplicate `'click'` events.

```html
<!DOCTYPE html>
<html>
  <title>zepto.ghostclick.js example</title>
  <script src="http://zeptojs.com/zepto.js"></script>
  <script src="./zepto.ghostclick.min.js"></script>

  <a href="#fixed" class="fixed">Fixed</a>
  <a href="#not-fixed" class="not-fixed">Not fixed</a>

  <script>
    $('.not-fixed').on('tap click', function () {
        $('body').append('<div>This message will appear twice on mobile devices!</div>');
    });

    $('.fixed').on('tap click', function () {
        $('body').append('<div>This message will appear only once everywhere!</div>');
        return false;
    });
  </script>
</html>
```

Ghost clicks?
=============

When using zepto's builtin `'tap'` event in order to get better responsiveness from
user actions you have to be careful to disable the old `'click'` event, because it will
still fire (about 300ms after the `'tap'`).

These spurious clicks can cause extra events that you weren't expected. For example, if
you're listening on click events too so that you can test on your laptop, then your event
handler will fire twice. Also, if your 'tap' event handler changes the DOM, then the
'click' may end up on a completely different element (like a link) that now occupies that
part of the screen.

Bugs
====

Even though the click event doesn't fire, any link still appears "active" for a few tens
of milliseconds.

If an alert box is shown for over a second between the tap event and the click event, the
click event will still fire.

Meta-fu
=======

zepto.ghostclick.js is released under the MIT license (see LICENSE.MIT for details).

It was inspired by https://developers.google.com/mobile/articles/fast_buttons.

Contributions and bug-reports are most welcome.
