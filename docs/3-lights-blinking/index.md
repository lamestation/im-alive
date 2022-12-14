# Lights Blinking

Let's get a little fancier. You'll stop paying attention to a solid green
light pretty quickly, but make it blink and you'll be entertained all day
(trust me, I am!).

## Repeating blocks of code with `REPEAT`

The `REPEAT` command does a lot more than waste time. It allows you to do all kinds of stuff.

First of all, you can put statements "inside" of it by indenting them. This will make Spin repeat them forever. A first guess at how to make the light turn on and off then would be this.

```spin
PUB Main
    dira[24]~~

    repeat
        outa[24]~
        outa[24]~~
```

If you try to run it though, you'll be disappointed to find that it looks like a solid green light, although slightly dimmer than before. Well, the LED _is_ blinking, but it's blinking way faster than you and I can actually see (that's eye-sight for you), so it just looks like it's not quite on.

If you really want to see the light **blink**, you have to slow the process _way_ down. `repeat` is helpful here again. Instead of repeating forever, you can tell it to repeat a specific number of times and then continue. Say, if you wanted it to repeat 1000 times, you could write `repeat 1000`.

How long that command actually takes to complete depends on how fast the Propeller is actually running, so you'd have to try some different numbers before you arrived at a good one. Let's look at the finished example.

```{.spin title="LightsBlinking.spin"}
PUB Main
    dira[24]~~

    repeat
        outa[24]~
        repeat 10000

        outa[24]~~
        repeat 10000
```

`repeat` is your go-to command for looping in Spin.

- Can be used as a `for` loop in other languages, but also as a
  `while` loop.
- Can contain statements in a "conditional".

Spin is indent-sensitive. The code:

!!! Note

    Spin is indent-sensitive.

    ```spin
    outa[24]~
    repeat 10000

    outa[24]~~
    repeat 10000
    ```

    is **NOT** the same as

    ```spin
        outa[24]~
    repeat 10000

        outa[24]~~
    repeat 10000
    ```

    Remember that!
