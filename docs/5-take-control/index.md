# Take Control

Now that we've learned how to include objects, let's take a look inside the LameStation SDK. In this example, we control the LED using the buttons and joystick.

Introducing **LameControl**, a small library for getting user input. Setting it up is straight forward⁠—just include it.

```spin
OBJ
    ctrl : "LameControl"
```

`ctrl.Update` saves the current state of all the
controls, so you can use them. Without calling `ctrl.Update`, LameControl
does nothing, so make sure you do. At the beginning of your loop is a good place for it.

```spin
    repeat
        ctrl.Update
```

## Conditionally Yours

Before you'll be able to see anything interesting, you need a way to test if a button has been pressed.

Well, the `IF` keyword does just that. It allows you to run code if a condition is true. Then, you can use the `ELSE` to run code if it is false.

```spin
    if condition
        ' runs if condition is true
    else
        ' runs if condition is false
```

So let's start small. Here's how to test if the `A` button is pressed. We use the `ctrl.A` function.

```spin
        if ctrl.A
            outa[LED_PIN]~~
        else
            outa[LED_PIN]~
```

The light turns off when pressed, if it has, or stays on when not.

You can see all the functions in LameControl by clicking it in the project view on the left-hand side, or looking at the [SDK reference](https://www.lamestation.com/reference/library/ctrl/).

Spin allows us to make more complex conditions using the `and`, `or` and `not` keywords. Some examples:

- `if ctrl.A and ctrl.B` - True only if both buttons are pressed.
- `if ctrl.A and not ctrl.B` - True if `A` is pressed but `B` is not pressed.
- `if ctrl.A or ctrl.B` - True if either `A` or `B` are pressed, or both.

So let's take all the LameControl commands and combine them into one, so that the light is off if any controls are touched at all.

```spin
        if ctrl.A or ctrl.B or ctrl.Up or ctrl.Down or ctrl.Left or ctrl.Right
            outa[LED_PIN]~~
        else
            outa[LED_PIN]~
```

Let's take the completed example for a _spin!_

```{.spin title="TakeControl.spin"}
OBJ
    ctrl : "LameControl"
    pin  : "LamePinout"

CON
    LED_PIN = pin#LED

PUB Main

    dira[LED_PIN]~~

    repeat
        ctrl.Update

        if ctrl.A or ctrl.B or ctrl.Up or ctrl.Down or ctrl.Left or ctrl.Right
            outa[LED_PIN]~~
        else
            outa[LED_PIN]~
```
