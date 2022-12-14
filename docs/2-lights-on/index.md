# Lights On

If we look at the LameStation's board layout, we'll find that there's a single LED we can toggle. This was designed into the board as an easy way for the LameStation to do _something_. As you might have gathered putting it together, getting a board to do _something_ can be half the battle.

All we have to do to turn on this light is toggle the microcontroller pin it is connected to. On this board, it's connected to pin 24. To turn on a pin, two steps are required:

1. Use the `DIRA` command to enable the pin as an output.
2. Use the `OUTA` command to set the pin to 0V.

So here's how you do it:

```spin
PUB Main
    dira[24]~~
    outa[24]~
```

The `~` and `~~` characters set the pin to high and low, respectively.

One thing you'll notice: if you run it as is, you'll never see the light come on. This is because as soon as your commands are finished, the Propeller has no more code to run so it decides to shut down. If you want your Propeller to stay awake, you have to keep it busy.

Use the `REPEAT` command to keep the LameStation in an infinite loop.

```{.spin title="LightsOn.spin"}
PUB Main
    dira[24]~~
    outa[24]~

    repeat
```

Now both LEDs on the LameStation should be active.
