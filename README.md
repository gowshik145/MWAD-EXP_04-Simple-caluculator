# MWAD-EXP_04-Simple-caluculator

## Name: GOWSHIK S
## Reg No: 212223220026
## Date:

## AIM
To  develop a Simple Calculator using React.js with clean and responsive design, ensuring a smooth user experience across different screen sizes.

## ALGORITHM
### STEP 1
Create a React App.

### STEP 2
Open a terminal and run:
  <ul><li>npx create-react-app simple-calculator</li>
  <li>cd simple-calculator</li>
  <li>npm start</li></ul>

### STEP 3
Inside the src/ folder, create a new file Calculator.js and define the basic structure.

### STEP 4
Plan the UI: Display screen, number buttons (0-9), operators (+, -, *, /), clear (C), and equal (=).

### STEP 5
Create a new file Calculator.css in src/ and add the styling.

### STEP 6
Open src/App.js and modify it.

### STEP 7
Start the development server.
  npm start

### STEP 8
Open http://localhost:3000/ in the browser.

### STEP 9
Test the calculator by entering numbers and operations.

### STEP 10
Fix styling issues and refine content placement.

### STEP 11
Deploy the website.

### STEP 12
Upload to GitHub Pages for free hosting.

## PROGRAM

# APP.JS
```
import React, { useState, useRef, useEffect } from 'react';

export default function App() {
  const [display, setDisplay] = useState('0');
  const [overwrite, setOverwrite] = useState(true);
  const lastInputRef = useRef(null);

  useEffect(() => {
    function onKey(e) {
      const key = e.key;
      if (/^[0-9]$/.test(key)) inputDigit(key);
      else if (key === '.') inputDot();
      else if (['+', '-', '*', '/'].includes(key)) inputOperator(normalizeOp(key));
      else if (key === 'Enter' || key === '=') inputEquals();
      else if (key === 'Backspace') backspace();
      else if (key.toLowerCase() === 'c') clearEntry();
      else if (key.toLowerCase() === 'a') allClear();
    }
    window.addEventListener('keydown', onKey);
    return () => window.removeEventListener('keydown', onKey);
  }, [display, overwrite]);

  function normalizeOp(k) {
    if (k === '*') return '×';
    if (k === '/') return '÷';
    return k;
  }

  function inputDigit(d) {
    setDisplay(prev => {
      if (overwrite || prev === '0') {
        setOverwrite(false);
        return d;
      }
      return prev + d;
    });
    lastInputRef.current = 'digit';
  }

  function inputDot() {
    setDisplay(prev => {
      if (overwrite) {
        setOverwrite(false);
        return '0.';
      }
      if (prev.includes('.')) return prev;
      return prev + '.';
    });
  }

  function inputOperator(op) {
    setDisplay(prev => {
      if (/[+\-×÷]$/.test(prev)) return prev.slice(0, -1) + op;
      return prev + op;
    });
    setOverwrite(false);
  }

  function allClear() {
    setDisplay('0');
    setOverwrite(true);
  }

  function clearEntry() {
    setDisplay('0');
    setOverwrite(true);
  }

  function backspace() {
    setDisplay(prev => {
      if (prev.length === 1) {
        setOverwrite(true);
        return '0';
      }
      const next = prev.slice(0, -1);
      return next === '' ? '0' : next;
    });
  }

  function inputEquals() {
    try {
      const expr = display.replace(/×/g, '*').replace(/÷/g, '/');
      if (!/^[-+0-9.×÷*/() ]+$/.test(expr)) return;
      // eslint-disable-next-line no-eval
      let result = eval(expr);
      if (!isFinite(result)) result = 'Error';
      else result = Number.isInteger(result) ? String(result) : String(Math.round(result * 1000000) / 1000000);
      setDisplay(String(result));
      setOverwrite(true);
    } catch {
      setDisplay('Error');
      setOverwrite(true);
    }
  }

  function handleButton(label) {
    if (label === 'AC') return allClear();
    if (label === 'C') return clearEntry();
    if (label === '⌫') return backspace();
    if (label === '=') return inputEquals();
    if (label === '.') return inputDot();
    if (['+', '-', '×', '÷'].includes(label)) return inputOperator(label);
    if (/^[0-9]$/.test(label)) return inputDigit(label);
  }

  const buttons = [
    ['AC', 'C', '⌫', '÷'],
    ['7', '8', '9', '×'],
    ['4', '5', '6', '-'],
    ['1', '2', '3', '+'],
    ['0', '.', '=']
  ];

  return (
    <div className='app-root'>
      <h1 className='title'> React Calculator By Gowshik S 212223220026</h1>
      <div className='calculator'>
        <div className='display'>{display}</div>
        <div className='buttons'>
          {buttons.flat().map((b, i) => (
            <button key={i} onClick={() => handleButton(b)} className={`calc-btn ${['+', '-', '×', '÷', '='].includes(b) ? 'op' : ''}`}>{b}</button>
          ))}
        </div>
      </div>
    </div>
  );
}

```
# index.html
```
<!doctype html>
<html lang="en">
  <head>
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width,initial-scale=1" />
    <title>Simple React Calculator</title>
  </head>
  <body>
    <div id="root"></div>
  </body>
</html>

```


## OUTPUT
<img width="1685" height="1029" alt="image" src="https://github.com/user-attachments/assets/43e353b9-ef10-408b-beae-2d6193bb79df" />
<img width="653" height="852" alt="image" src="https://github.com/user-attachments/assets/6183cf37-0123-4a3f-b851-99139dae2979" />


## RESULT
The program for developing a simple calculator in React.js is executed successfully.
