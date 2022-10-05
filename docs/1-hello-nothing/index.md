# Hello Nothing

Attempting to download an empty file to the LameStation will generate an error from PropellerIDE.

```{.spin title="An empty file"}

```

So here we see the bare minimum that constitutes a Spin program.

```{.spin title="HelloNothing.spin"}
PUB First
```

Well, that was easy!

This is called a `PUB` block, which is short for _public function_. Functions are areas where you write code that can _do stuff_. If your code is a sentence, then a function is the verb, the action. You can put as many `PUB` blocks as you want into a file, but when you run your code, the Propeller will start by running the first public function that appears in the file. From that function, you can call other functions.

```
PUB First
    Third

PUB Another

PUB Third
    Another
```

All Spin programs _must_ include at least one `PUB` block.

!!! Note

    Spin is **not** case-sensitive.

    ```spin
    PUB First
    ```

    is the same as

    ```spin
    pub first
    ```

    Remember that!

View the complete example at `/tutorials/Basics/HelloNothing.spin`.

## Bonus Round: Function Names!

Function names can contain letters, numbers, and underscores. However, the first character cannot be a number (_that's good; otherwise, they'd start looking like passwords_).

_Good:_

- `hello_chicken`
- `bacon123`
- `_supertime`

_Bad:_

- `123attack`
- `extreme#@$**`
