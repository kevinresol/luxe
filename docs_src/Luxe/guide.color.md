
[![Logo](http://luxeengine.com/images/logo.png)](index.html)

###[Back to feature guide](guide.html#color)
###[View all guides](guide.html)

---
## Manipulating color in luxe
---

Color is a very useful tool in games, and being able to smoothly transition colors is important.   

When dealing with **RGB** color as is the default color type, it tends to break when you try and animate between two colors.   

The solution to this, is different color models, such as **HSV** (Hue, Saturation, Value) and **HSL** (Hue, Saturation, Lightness).

luxe supports both HSL and HSV interchangeably with the default of RGB (and each support alpha as well).

## What is the difference?
---

HSV and HSL are cylindrical in nature, that means that they are _round_ and their color value works in degrees(º) rather than separate color components. 

Take a look at the image below, this is the color wheel (Hue only), mapped to degrees.

![color wheel](images/color_wheel.png)

### How this helps
---

Notice how if we want to transition from red (danger!) to orange (warning) on a flashing UI element, it's around 30º of movement?    

To animate that using Hue (the above color wheel) it is simple, we animate the hue value.

### Color classes have their own convenience tween function
---
One thing you will notice is that the color classes have their own tween function for convenience which acts a lot like the tweening from the [tween guide](guide.tween.html).
        
        //We create our red color using 0º Hue (red), 
        //the second and third argument are saturation and value, 
        //which we set to "maximum" right now.

    var color = new ColorHSV( 0, 1, 1);

        //Now we want to animate to orange, just change the hue
        //over two seconds, to orange

    color.tween( 2, { h:30 } );

By mapping the colors to a round cylinder it affords much smoother transitions between colors, much smoother than RGB can do.

## Saturation, Lightness and Value

Color can be quite a complex system, and has mathematical properties outside of the scope of this simple guide. If you want to get in depth details into the mechanics of color , [this article on wikipedia is quite thorough](http://en.wikipedia.org/wiki/HSL_and_HSV).

Now - for simplicity sake - we will define the terms in a less exact way. Take a solid color at hue 30º like above. 

- Value - The color approaches black when value is lowest
- Lightness - The color approaches white when the lightness is highest
- Saturation - The amount of color present (like draining the color away)

Have a look at these graphs [from Wikipedia](http://en.wikipedia.org/wiki/HSL_and_HSV) for a clearer view.

![HSL/HSV](images/color_hsvl.png)

## Creating and using the different types
---

Now that you hopefully understand the purpose and differences, we can look at how to work with them in luxe.

        //defaults for r g b and a are 1 (full white)
    var color : Color = new Color( r, g, b, a );

        //Defaults for h = 0, s = 0, v = 1, a = 1 (full white)
    var colorhsv : ColorHSV = new ColorHSV( h, s, v, a );

        //Defaults for h = 0, s = 1, l = 1, a = 1 (full white)
    var colorhsl : ColorHSL = new ColorHSL( h, s, l, a );

This is for creating, but how about switching between? 

## Changing color type   
All types are extended from the `Color` class, so they automatically work where `Color` is expected. For example, a sprite color is typed as `Color` but a `ColorHSL` or `ColorHSV` can be given in place - `sprite.color = colorhsl;`

**This makes all types interchangeable automatically**,    
but the following functions are exposed as well.
    
        // helpers on Color
    color.toColorHSL        //returns ColorHSL
    color.toColorHSV        //returns ColorHSV
    color.fromColorHSL      //changes color
    color.fromColorHSV      //changes color

        //helpers on ColorHSL
    colorhsl.toColor        //returns Color
    colorhsl.toColorHSV     //returns ColorHSV
    colorhsl.fromColor      //changes colorhsl
    colorhsl.fromColorHSV   //changes colorhsv

        //helpers on ColorHSV
    colorhsv.toColor        //returns Color
    colorhsv.toColorHSL     //returns ColorHSV
    colorhsv.fromColor      //changes colorhsv
    colorhsv.fromColorHSL   //changes colorhsv

---

&nbsp;   

###[Back to feature guide](guide.html#color)
###[View all guides](guide.html)

&nbsp;   
&nbsp;   
&nbsp;   