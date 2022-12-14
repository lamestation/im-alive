# I'm Alive!

Having to write out specific values every time you need them is starting to become a problem. In the previous example, you had to write `24` three times and `10000` twice. Unless those values stay the same forever (which they might not, especially for the "10000", a value you may want to adjust), you'll have to update them everywhere they are used. Not only that, but you'll always have to remember what they mean, which is next to impossible if your code is more than a few lines long.

Luckily, there's a way around this problem.

## Introducing `CON` blocks

`PUB` isn't the only kind of block available. `CON` blocks allow you to set _constant_ values, that don't change, allowing you to call them by name.

Setting a constant is easy. Constant names can contain letters, numbers, and underscores (`_`), but must start with a letter or underscore.

Let's set constants for the LED pin and the count of times `repeat` will run before continuing. You can set as many as you want, but they must be inside a `CON` block.

```spin
CON
    LED_PIN = 24
    COUNT   = 1000
```

There can also be as many `CON` blocks as you like too.

```spin
CON
    LED_PIN = 24
CON
    COUNT   = 1000
```

It works exactly the same, but now if we need to change the values, we only need to change them in one place.

```spin
CON
    LED_PIN = 24
    COUNT   = 1000

PUB Main
    dira[LED_PIN]~~

    repeat
        outa[LED_PIN]~
        repeat COUNT

        outa[LED_PIN]~~
        repeat COUNT
```

!!! Tip

    **Style is important**

    You may have noticed that all the constants are in capital letters when Spin is case-insensitive.

    Why? It makes it easier to remember that it's a constant value.

## Introducing `OBJ` blocks

Sometimes it's helpful to put code into a separate file. That way, if you have a nice piece of code that does something useful, you don't have to keep rewriting it for every project you work on. Instead, you can use it from where it is. Spin allows us to do this using the `OBJ` block. `OBJ` is short for _object_, because code files are called "objects" in Spin lingo.

To include an object in your code, you will need to provide the name of the file in quotes, and a short name under which you'd like to use the object. In our case, we'd like to add the file `LamePinout.spin` which contains pin assignments for the LameStation board. You can include the `.spin` extension or not, but the include file _must_ be a Spin file.

```spin
OBJ
    pin : "LamePinout"
```

Now that you have the object included, you will be able to use the functions and constants inside of it.

To call a function in another object, prefix the short name of the included object, separating it with a period (`.`).

```spin
PUB Main
    pin.Null
```

To get the value of a constant in another object, add the short name and the hash symbol (`#`). Here's us grabbing the pin assignment for the LED from `LamePinout.spin`.

```spin
CON
    VALUE = pin#LED
```

So now let's set `LED_PIN` to `pin#LED` instead of having to remember what the pin is ourselves.

```{.spin title="ImAlive.spin"}
OBJ
    pin : "LamePinout"

CON
    LED_PIN = pin#LED
    COUNT   = 10000

PUB Main
    dira[LED_PIN]~~
    repeat
        outa[LED_PIN]~
        repeat COUNT

        outa[LED_PIN]~~

        repeat COUNT
```

!!! Tip

    **Fun Fact**

    This happens to be the example that comes pre-loaded on every LameStation unit!
