# How Next.js Impacts Front‐End Work
**9/26/2023 • Mya Schroder**

Next.js (really React) discourages [DOM-manipulation](https://www.scaler.com/topics/javascript-dom-manipulation/#). DOM-manipulation means giving html elements IDs and manipulating the layout using these IDs. Instead Next.js uses a functioned approach. This means you put your html components in functions as passed parameters into the function that affects that component.

> Here is example of tradition DOM-manipulation in javascript (generated with the help of chatGPT):
```js
<!-- index.html -->
<body>
    <div id="app"></div>

    <script>
        const buttonComponent = document.createElement('button');
        buttonComponent.textContent = 'Click Me';

        const output = document.createElement('p');
        output.textContent = 'This text will change when you click the button.';

        buttonComponent.addEventListener('click', () => {
            output.textContent = 'Button was clicked!';
        });

        const app = document.getElementById('app');
        app.appendChild(buttonComponent);
        app.appendChild(output);
    </script>
</body>
```

> This is how that same thing is done in Next.js:

```js
// components/Button.js
import React from 'react';

const Button = ({ onClick }) => {
  return <button onClick={onClick}>Click Me</button>;
};

export default Button;
```

```js
// app/page.js
import React, { useState } from 'react';
import Button from '../components/Button';

const HomePage = () => {
  const [outputText, setOutputText] = useState('This text will change when you click the button.');

  const handleClick = () => {
    setOutputText('Button was clicked!');
  };

  return (
    <div>
      <Button onClick={handleClick} />
      <p>{outputText}</p>
    </div>
  );
};

export default HomePage;
```