

Please see [PlottingFuture] for the central list of plotting goals.

## Plot Interaction

It would be good if one could call at any time onto the plot object things like p.set_axis_visible(False), p.get_viewpoint() or p.save_image() or maybe in another syntax:
p.set('axis_visible',True) and so on. *Properties are perfect for this, see my comment below ;-)*

This is a list of all settings I can think of:

  * camera position
  * camera viewdirection or viewpoint
  * camera mode (perspective, ortho)
  * something handy to set the details of the perspective view, otherwise just in the OpenGL manner(nearPlane, farPlane, fovy, aspect)

  * axes visible
  * axes color
  * axes thickness
  * axes interval
  * axes ticks

  * function interval
  * function color
  * function grid visible
  * function grid size (that would set the amount of vertices drawn)

and of course there should be:

  * show
  * save_image

Feel free to add other settings to this list!

Many of them are already implemented, but it would be nice to have a consistent way of using the plot object.

#### Brian's Comment

We should make a goal to encapsulate all user-accessible member variables with properties. For example:
```
class PlotObject(object):
    ...
    def _set_visible(self, visible):
        self._visible = visible
    def _get_visible(self):
        return self._visible
    visible = property(_get_visible, _set_visible)
```
You can see some of these I've already done towards the bottom of plot_mode_base.py, but there are many that are only available directly. A sub-goal of this should be adding the underscore prefix to all member variables, and have the only legitimate access be through properties.

I totally agree that these should be accessible from Plot.whatever and p`[`n`]`.whatever. Also I think we should keep a hierarchy, i.e. it should be p.axes.visible rather than p.axes_visible, etc.

## Camera

What will need a little work are the camera settings, because the camera is now not instantiated until the interactive window is opened.

#### Brian's Comment

This is made slightly more complicated by the camera's reliance on OpenGL matrix calls (which need a GL context, in our case a pyglet window, to function). We could always replace this stuff with our own matrix transform maths, or store camera transformations a different way and apply them to the model matrix each frame when a context is available.

*update:* another thing, you have to be careful of [http://en.wikipedia.org/wiki/Gimbal_lock gimbal lock], which results from the fact that euler rotations are performed on non-independent axes.

#### Basti Comment

A solution would be to have two camera objects. One that is accessible for the user through p.camera and where just the things are stored a user would like to set. When the window is initialized the render_camera would have to take the variables from the plot.camera and calculate whatever is necessary. But then we must be aware of data inconsistencies, because on one side the plot.camera can be changed through a running script and on the other side the render_camera will be changed interactively. We would have to implement a function called in the _main_loop_ that tells if something was changed and if so, resets the render_camera.
 

## Image Capture Resolution Independence

This really is not easy to achieve, if the image gets bigger then the screen, because I couldn't find a way to render in the offset. There are some ways described in the net, but as I see it there is always a big platform dependency.

I tried a little workaround with moving the window (of course invisible) over the desktop and get screenshot pieces that can finally put together. But I now get at different places of the code "invalid pointer" exceptions I can't trace back. Maybe someone wants to look at it [http://bastikr.ba.funpic.de/offset_rendering.py here]

Anyway it should be possible to render to two windows at the same time. This would allow the user to interactively choose his view and save an image in any size smaller than his desktop without having to close the interactive window.

#### Brian's Comment

The reason I've avoided an offscreen rendering approach is that it requires the use of GL extensions, which (as you said) are mostly platform dependent. Some available options are discussed [http://www.mesa3d.org/brianp/sig97/offscrn.htm here].

## Some other features that crossed my mind

  * Rotating with keys doesn't feel natural to me. I would like a mode where the rotations are going around the axes of the ploted object, not around the screen axes. *I prefer the way it is, but it is actually really easy to do it the way you've described. How about CAPSLOCK toggle or asdw for "my way" and jkli for "your way"? Also, note that z,c and 1,3 currently provide the functionality you describe for the Z axis --Brian* _it seems very natural to me, once you realize, that it is like if you were walking in some 3D shooting game and instead of going around enemy, you saw the plot. :) --Ondrej_


  * Just a matter of style ist the following: why isn't it possible to call p`[`0`]`? The indices have to be greater than 0! It would be more pythonic if it would behave like an ordinary list, although of course it is a dictionary. But nobody has to know;) *I originally did it that way because I was mimicing a graphing calculator like the ti89, which starts at 1. If it started at 0 I guess it would work for people who expected either convention. Let's do it your way. --Brian* _let's start counting from 0, we are in Python... --Ondrej_ *Ok, ok. Tell Guido I'm sorry, but it's fixed now. --Brian*

  * Another feature that sometimes would be nice, is to split a window up and display in each part a different view of the plot-object. *You are welcome to implement this :-P [http://nehe.gamedev.net/data/lessons/lesson.asp?lesson=42 Here] is a tutorial covering multiple viewports in a single window, but I'm not sure how this would mix with pyglet. --Brian*

  * I would also like to set single functions invisible, through scripting as well as interactively. Maybe with the keys 1-9. *Another great idea. --Brian*

  * What would also be useful, is a string representation of the whole plot object, so the state of the plot can be saved. Consiquently another function is necessary to create or set a plot object with this string.

  * What about animations? That would also be fantastic to have! The user could activate it with something like p.set_time_variable(t) and p.animate(). (Therefor the camera would have to accept a function so it can be moved easily.)

  * It would be nice to pass sympy.geometry objects like Circles, Lines, etc. to the plot object!

  * At the moment the axes are always absolutely visible. This looks strange for some plots. Maybe it would be better to let them be lightly covered by the plot objects.