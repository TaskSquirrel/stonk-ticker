# Stonk Ticker [![npm](https://img.shields.io/npm/v/stonk-ticker)](https://npmjs.com/package/stonk-ticker)

Price ticker from Robinhood for React apps

[See it in action](https://tasksquirrel.github.io/stonk-ticker/)

## Install

```sh
npm install stonk-ticker
```

## Example

```jsx
import React, { useState } from "react";
import Ticker, { toMoneyString } from "stonk-ticker";

function App() {
    const [value, setValue] = useState({
        price: 1000,
        movement: "up",
    });

    useEffect(() => {
        const int = setInterval(() => {
            const nextPriceDiff = Math.random() * 10;

            setValue(({ price: prevPrice }) => ({
                price: prevPrice + nextPriceDiff,
                movement: nextPriceDiff <= 0 ? "down" : "up",
            }));
        }, 1000);

        return () => clearInterval(int);
    });

    return (
        <Ticker
            value={ toMoneyString(value.price) }
            constantKeys={ ["-", "$", "."] }
            movement={ value.movement }
        />
    );
}
```

## Props

| Prop         | Type              |                                                                                                                    |
| ------------ | ----------------- | ------------------------------------------------------------------------------------------------------------------ |
| `value`      | `string` or `number` | Display value                                                                                                      |
| `direction`  | `"up"` or `"down"`   | Determines text color for text that changes                                                                        |
| `dictionary` | `string[]`        | The set of characters the ticker cycles through. Default dictionary covers characters for USD money representation |
| `constantKeys`  | `string[]`        | Characters that should not animate between states. ($) for example for money. |
| `colors`     | `string[]`        | `colors[0]` is the color of text for an `up` movement, and the `colors[1]` is the `down` color                |
