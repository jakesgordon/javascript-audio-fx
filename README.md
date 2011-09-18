Javascript AudioFX (v0.2.0)
===========================

Simple HTML5 `<audio>` support.

 * Easily `play()` and `stop()` any audio track.
 * Add support for audio **pools** for short, repeating, overlapping sounds.
 * Add support for `loop` in browsers that don't natively support it.
 * Load appropriate audio format based on current browser support.
 * Callback when audio has loaded and `canplay`

Download
========

You can download [audio-fx.js](https://github.com/jakesgordon/javascript-audio-fx/raw/master/audio-fx.js), or
get the minified version [here](https://github.com/jakesgordon/javascript-audio-fx/raw/master/audio-fx.min.js)

Alternatively:

    git clone git@github.com:jakesgordon/javascript-audio-fx

 * All code is in audio-fx.js
 * Minified version available in audio-fx.min.js
 * Less than 1.2K (minified)
 * No 3rd party library is required
 * Demo can be found in /index.html

Usage
=====

Include `audio-fx.js` in your application.

In its simplest form, load music by constructing an `AudioFX` object:

    var music = AudioFX('sounds/music.mp3');

The `AudioFX` instance has the simplest possible API:

    music.play();     // play the audio
    music.stop();     // stop the audio
    music.audio;      // the underlying <audio> tag

**However**, different browsers support different formats so you should provide at
least `ogg` and `mp3` formats if you want to support a broad range of browsers:

    var music = AudioFX('sounds/music', { formats: ['ogg', 'mp3'] });

Other options include `volume`, `loop` and `autoplay`:

    var music = AudioFX('sounds/music', {
                          formats: ['ogg', 'mp3', 'wav'],
                          volume:   0.5,
                          loop:     true,
                          autoplay: true });

Audio Pools
===========

If you want to play a short sound effect multiple overlapping times (e.g. game explosions and effects) then
you need multiple `<audio>` tags.

The AudioFX library provides this functionality by accepting a `pool` option:

    var shoot = AudioFX('sounds/shoot', { formats: ['ogg', 'mp3'], pool: 10 });

The `AudioFX` instance has the exact same API as above:

    music.play();     // play the first available audio
    music.stop();     // stop the audio
    music.audio;      // an ARRAY containing the pool of underlying <audio> tag

Waiting for Sounds to Load
==========================

The `AudioFX` method accepts an optional 3rd parameter that can contain a function that will be
called when the `<audio>` tag has loaded:

    var name    = 'sounds/music';
    var options = { formats: ['ogg', 'mp3'] };
    var onload  = function() { alert('music is ready'); }

    var music = AudioFX(name, options, onload);

BrowserSupport
==============

If necessary, you can examine the `AudioFX.supported` property to find out what kind of `<audio>` support
is provided by your browser.

It will be `false` if there is no support at all, otherwise it will contain:

    AudioFx.supported.ogg;  // (true|false)
    AudioFx.supported.mp3;  // (true|false)
    AudioFx.supported.wav;  // (true|false)
    AudioFx.supported.loop; // (true|false) - some browsers dont (yet) support the loop option


NOTES
=====

After starting this project, I discovered the [buzz](http://buzz.jaysalvat.com/) library which also
abstracts HTML5 `<audio>` functionality... and does it much more thoroughly than `javascript-audio-fx`
but does not have support for creating an `<audio>` **pool**.

... I should probably just be forking buzz and trying to add pooling support to it, but I haven't
had the time yet. If you have any thoughts let me know ! 

Also note that browser support for HTML5 audio is still pretty messed up. This library works pretty
well in most modern desktop browsers, IE9, Chrome13, FF5, Opera11, but Safari continues to have delays
that make short sounds unusable. Also mobile browsers are very limited in their support for HTML5 Audio.

You can find an example rant [here](http://www.phoboslab.org/log/2011/03/the-state-of-html5-audio).

So... Very Early experimentation. YMMV

License
=======

[WTFPL](http://en.wikipedia.org/wiki/WTFPL)

Sample Sounds
=============

NOTE: the sample sounds included in this project are royalty free sounds licensed from
[Lucky Lion Studios](http://luckylionstudios.com/) and [Premium Beat](http://www.premiumbeat.com/). They
are licensed ONLY for use in this project. If you fork this code you must provide your own sample sounds.

Thanks for your honesty!

Contact
=======

If you have any ideas, feedback, requests or bug reports, you can reach me at
[jake@codeincomplete.com](mailto:jake@codeincomplete.com), or via
my website: [Code inComplete](http://codeincomplete.com/)





