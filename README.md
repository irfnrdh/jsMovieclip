JSMovieClip
=========

JS movieclip is a small javascript library to quickly and easily create, integrate, and control animations in an HTML page.

It is compatible with all browsers, from Internet Explorer 6 to latest smartphone (iOS, Android..). 

JS MovieClip uses "sprite", that is to say a large image containing all the frames of to animation. Then, It will allow to play and control the animation with ````stop()````, ````play()````, ````gotoAndPlay()```` ... like any Flashers does.

V1 stable
----------
###Creation###

First, you need a sprite, a big image containing each frame of your animation.
You have 3 options : 
<ul>
    <li>Horizontal sprite http://jsmovieclip.jeremypetrequin.fr/samples/basic/poulpe.png</li>
    <li>Vertical sprite http://jsmovieclip.jeremypetrequin.fr/samples/basic/poulpe_1.png</li>
    <li>Custom sprite http://jsmovieclip.jeremypetrequin.fr/samples/basic/poulpe_2.png</li>
</ul>

The only requirement is that each frame need to have the same size!

To simply create it : in Flash or After Effects, export your animation in a PNG sequences, and join it in a sprite with photoshop, GIMP, TexturePacker...


Then, you need a DOM element, div or whatever you want : 
````HTML
<div id="my-element"></div>
````

After, you need to apply to it the width and the height of a frame and the sprite as background :
````CSS
#my-element {
    width : 200px;
    height : 200px;
    background:url(sprite.png) no-repeat;
}
````

And now, instanciate a new JSMovieclip object : 
````javascript
var movieclip = new JSMovieclip(document.getElementById('my-element'), params);
````

First parameter can be a DOM element, an array of DOM elements, a jQuery (or Zepto..) object, a NodeList...

Second parameters are options, they can be : 
````javascript
{
    framerate : 25,
    stopCallback : fn,
    frames : [],
    direction : 'h' || 'v',
    frames_number : 0,
    width : 0,
    height : 0
}
````
So : 
<ul>
    <li>the framerate is the framerate of your animation, in Frame Per Second, the default is 25</li>
    <li>In stopCallback you can pass a function it'll call each time the movieclip stops</li>
</ul>

For the sprite, you have several options, so, 
<ul>
<li>if you have a horizontal sprite, you can simply specifie the direction : 'h' (horinzontal), the frames_number and the width of a frame
</li>
<li>
For a vertical sprite, set direction to 'v', the frames_number, and the height of a frame
</li>
<li>If you have a custom sprite, just set the frames array with each frame : [{x:0, y:0}, {x:200, y:0}, {x:400, 0}, {x:0, y:200}, {x:200, y:200}, {x:400, y:200} ,....] (you can also use this parameter for a vertical or a horizontal sprite)</li>
</ul>

###API###

There are some public methods :

play the animation from the frame where you are, boolean ````loop````` to specifie if you want to loop or not
````javascript
mc.play(loop : boolean); 
````

stop the animation (dispatch the stop callback)
````javascript
mc.stop();
````

play the animation from the frame ````frame````, boolean ````loop```` to specifie if you want to loop or not
````javascript
mc.gotoAndPlay(frame:int, loop:boolean); 
````

go and stop directly to a frame
````javascript
mc.gotoAndStop(frame:int);
````

block the animation between two specifics frames :     
````javascript
mc.loopBetween(frameStart:int, frameEnd:int);
````

all animation are now between frameStart and frameEnd animation 
````javascript
mc.loopBetween(1, 10).play(true); //play animation between first frame and 10's
````

If you call ````mc.loopBetween();```` you can call clearLoopBetween to reset first and lastFrame to the default
````javascript
mc.clearLoopBetween();
````

get current frame
````javascript
mc.currentFrame():int
````

go back to a frame
````javascript
mc.prevFrame();
````

go to the next frame
````javascript
mc.nextFrame();
````

if play : stop, if stop : play, boolean loop to specifie if we want to loop or not
````javascript
mc.toggle(loop:boolean);
````

Change the way of playing : 
````javascript
mc.changeWay(1); // play in the normal way
mc.changeWay(-1); // invert the playing
mc.changeWay(-1, true); //the second param, a boolean to stay a the same frame
````

Get current way of playing, return 1 or -1
````javascript
mc.getWay():int
````

All method are chainable (except currentFrame() and getWay() ), so you can do :
````javascript
mc.loopBetween(12, 14).gotoAndPlay(12)
````

V1 jQuery plugin version
----------
Instance :
````javascript
$('element(s)').JSMovieclip(params);
````

recover the movieclip object
````javascript
var mc = $('#element').data('JSMovieclip'); 
````

You can now apply all the public method on mc object
````javascript
mc.play();
mc.stop();
//....
````    

Samples & Usefull links
------------
###Sample###
<ul>
<li> Basic example : http://jsmovieclip.jeremypetrequin.fr/samples/basic/ </li>
<li> Multiple : http://jsmovieclip.jeremypetrequin.fr/samples/multiple/ </li>
<li> Control the animation : http://jsmovieclip.jeremypetrequin.fr/samples/controls/</li>
<li> Squirrel : http://jsmovieclip.jeremypetrequin.fr/samples/squirrel/</li>
</ul>

###Experiment###
<ul>
<li>
Little game experiment : http://jsmovieclip.jeremypetrequin.fr/samples/game/
</li></ul>

###Tools###
<ul>
<li>
Convert TexturePacker JSON Array export to Javascript Array : http://jsmovieclip.jeremypetrequin.fr/tools/convert/
</li></ul>
###Articles###
<ul>
<li>
Workflow Flash > Texture Packer > JSMovieclip : https://gist.github.com/14a77d4652c096a1fac7
</li></ul>
