
# JavaScript Basics (Tasks 2-8)

Short notes and practical examples from JavaScript fundamentals.

---

# Task 2 - JavaScript Basics

## Variables

Variables store data values.

```javascript
var oldWay = "hello";
let name = "John";
const age = 25;
````

* `var` → function scoped
* `let` / `const` → block scoped

---

## Data Types

Common JS data types:

```javascript
let text = "Hello";     // String
let number = 100;       // Number
let status = true;      // Boolean
let empty = null;       // Null
let value;              // Undefined
let user = {};          // Object
```

---

## Functions

Reusable blocks of code:

```javascript
function greet(name) {
    console.log("Hello " + name);
}

greet("Bob");
```

---

## Loops

Repeat code multiple times:

```javascript
for (let i = 0; i < 5; i++) {
    console.log(i);
}
```

Other loops:

```javascript
while(condition) {
    // code
}

do {
    // code
} while(condition);
```

---

## Request-Response Cycle

Browser (Client) → Request → Web Server → Response → Browser

---

# Task 3 - First JavaScript Program

JavaScript is an interpreted language and runs directly in the browser.

Example:

```javascript
console.log("Hello, World!");

let age = 25;

if (age >= 18) {
    console.log("Adult");
} else {
    console.log("Minor");
}

function greet(name) {
    console.log("Hello " + name);
}

greet("Bob");
```

---

## Running JS in Chrome Console

1. Open Google Chrome
2. Press:

```
Ctrl + Shift + I
```

3. Open **Console** tab
4. Run JavaScript code directly

Example:

```javascript
let x = 5;
let y = 10;

let result = x + y;

console.log(result);
```

Output:

```
15
```

---

# Task 4 - JavaScript in HTML

There are two ways:

* Internal JavaScript
* External JavaScript

---

## Internal JavaScript

JS inside HTML using `<script>`:

```html
<!DOCTYPE html>
<html>

<body>

<h1>Addition</h1>

<p id="result"></p>

<script>

let x = 5;
let y = 10;

let result = x + y;

document.getElementById("result").innerHTML =
"The result is: " + result;

</script>

</body>
</html>
```

Run:

```
Double click HTML file → Open in Chrome
```

---

## External JavaScript

HTML:

```html
<script src="script.js"></script>
```

script.js:

```javascript
let x = 5;
let y = 10;

let result = x + y;

document.getElementById("result").innerHTML =
"The result is: " + result;
```

Advantages:

* Cleaner HTML
* Easier maintenance
* Reusable code

---

## Check JS Source Code

Chrome:

```
Right Click → View Page Source
```

Internal JS:

```html
<script>
    code here
</script>
```

External JS:

```html
<script src="file.js"></script>
```

---

# Task 5 - JavaScript Dialogs

## Alert

Shows a message:

```javascript
alert("Hello THM");
```

---

## Prompt

Gets user input:

```javascript
let name = prompt("Your name:");

alert("Hello " + name);
```

---

## Confirm

Returns true/false:

```javascript
confirm("Are you sure?");
```

Result:

```
OK     → true
Cancel → false
```

---

## Malicious JavaScript Example

`invoice.html`

```html
<script>

for(let i = 0; i < 3; i++) {
    alert("Hacked");
}

</script>
```

A malicious script can create annoying behavior or attacks.

Only run JS from trusted sources.

---

# Task 6 - Control Flow

## If / Else

Example:

```javascript
let age = prompt("Age:");

if(age >= 18) {

    console.log("Adult");

} else {

    console.log("Minor");

}
```

---

## Login Example

Client-side authentication is insecure:

```javascript
let username = "admin";
let password = "12345";

if(user == username && pass == password){

    alert("Login successful");

}
```

Sensitive logic should not be stored in client-side JS.

---

# Task 7 - Minification & Obfuscation

## Minification

Removes:

* Spaces
* Comments
* Extra characters

Purpose:

* Smaller files
* Faster loading

---

## Obfuscation

Makes JS harder to read:

Example:

Original:

```javascript
function hi(){
 alert("Welcome");
}

hi();
```

Obfuscated:

```javascript
(function(_0x1234){
...
})();
```

The browser can still execute it.

---

## Useful Tools

JS Obfuscator:

```
https://obfuscator.io/
```

Deobfuscation tools can restore readable code.

---

# Task 8 - JavaScript Security Best Practices

## 1. Do not trust Client-Side Validation

Bad:

```javascript
if(password == "12345"){
    login();
}
```

Always validate on the server.

---

## 2. Avoid Unknown Libraries

Bad:

```html
<script src="unknown-library.js"></script>
```

Use trusted sources only.

---

## 3. Do not Hardcode Secrets

Bad:

```javascript
const API_KEY = "pk_TryHackMe-1337";
```

Never store:

* API keys
* Passwords
* Tokens

inside frontend JS.

---

## 4. Minify and Obfuscate Production Code

Benefits:

* Smaller files
* Harder reverse engineering
* Better performance

---

# Useful Chrome Shortcuts

Open Developer Tools:

```
Ctrl + Shift + I
```

Open Console:

```
Developer Tools → Console
```

View Source:

```
Right Click → View Page Source
```

Inspect Element:

```
Right Click → Inspect
```

---

این نسخه برای README گیت‌هاب مناسب است چون:
- طولانی نیست.
- کدها قابل کپی هستند.
- دستورات Chrome و ابزارها حفظ شده‌اند.
- توضیحات تئوری به حداقل رسیده‌اند.
```
