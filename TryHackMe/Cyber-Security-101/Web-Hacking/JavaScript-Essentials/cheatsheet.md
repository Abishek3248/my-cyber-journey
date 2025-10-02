# Cheatsheet - JavaScript Essentials

## Core Concepts

| Concept | Explanation | Example |
|---|---|---|
| Console Output | Used to print messages to the console. | `console.log("Hello, World!");` |
| Variables | Store values using `let` or `const`. | `let age = 25;` |
| Data Types | `string`, `number`, `boolean`, `null`, `undefined`, `object`. | `let name = "Bob";` |
| Functions | Reusable blocks of code. | `function greet(n){ console.log("Hi " + n); }` |
| Control Flow | Conditional logic with `if-else`. | `if (age >= 18) { ... } else { ... }` |
| Arithmetic | Basic operators: `+`, `-`, `*`, `/`. | `let result = 5 + 10;` |


## Running JS in Browser

| Action | How |
|---|---|
| Open Console | Chrome → `Ctrl + Shift + I` → Console tab |
| Run Code | Type/paste JS code in console → press Enter |
| Example | ```let x=5; let y=10; console.log(x+y);``` → **15** |


## Dialog Functions

| Function | Purpose | Example | Return Value |
|---|---|---|---|
| `alert()` | Shows a message box. | `alert("Hello!")` | `undefined` |
| `prompt()` | Asks user input. | `let n = prompt("Name?")` | `string` or `null` |
| `confirm()` | Yes/No question. | `confirm("Continue?")` | `true` / `false` |


## Control Flow (Bypassing Example)

| Statement | Purpose | Example |
|---|---|---|
| `if-else` | Run code based on condition. | ```if (age >= 18) { msg="Adult"; } else { msg="Minor"; }``` |
| Practical | Used in `age.html` for verifying input. | Prompt asks for age → Displays message |
| Bypassing | Login forms made in JS can be bypassed by editing client-side code in browser. | Example: change `if(user=="admin")` logic in DevTools |


## Best Practices

| Practice | Why Important |
|---|---|
| Don’t rely only on client-side validation | Users can disable/modify JS; always validate on server too |
| Avoid untrusted libraries | Malicious scripts may be disguised as legit ones |
| Never hardcode secrets | API keys/credentials in JS are visible in source |
| Minify & Obfuscate code | Improves performance & makes logic harder to reverse |


