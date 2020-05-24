
# Stonk Ticker

Price ticker from Robinhood for React apps

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
        setInterval(() => {
            const nextPriceDiff = Math.random() * 10 - 5;

            setValue(({ price: prevPrice }) => ({
                price: prevPrice + nextPriceDiff,
                movement: nextPriceDiff <= 0 ? "down" : "up",
            }));
        }, 1000);
    });

    return (
        <Ticker
            value={ toMoneyString(value.price) }
            movement={ value.movement }
        />
    );
}
```

## Props

|Prop|Type||
|---|---|---|
|`value`|`string | number`||
|`direction`|`"up" | "down"`|Determines text color for text that changes|
|`dictionary`|`string[]`|The set of characters the ticker cycles through. Default dictionary covers characters for USD money representation|
|`constants`|`string[]`|Characters that stay constant, but left-relative to the string ($) for example in a USD string.|
|`colors`|`string[]`|First element is the color of text for an `up` movement, and the second element is the `down` color|
