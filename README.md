# Frameplay-TS-Assessment
This was an assignment given for a technical interview at Frameplay. The original brief can be found below.

# Running
Make sure required modules are installed and the project is built:
```
npm install
npm run build
```
Examples of convertToObject handling different types can be found at the bottom of `index.ts`. To run through the examples, run the following:
```
npm run start
```

# Notes
I liked the problem, but it was time consuming and difficult to solve. The main difficulties were:
1. Microsoft's documentation for the Compiler API is very limited and some of their examples didn't seem to work. It took a while to find [more thorough docs](https://writer.sh/posts/gentle-introduction-to-typescript-compiler-api/).
2. My approach was flawed - I was hoping to build the object literal as the `visit()` function traversed the AST but this proved to be very complicated and difficult to troubleshoot. The end result works but the code is difficult to follow. If I were to do this again, I'd break the program into smaller parts instead of trying to do everything all at once. That might result in a less efficient algorithm but it would be easier to understand.

It's worth noting that my solution differs a little from the sample output provided in the brief. The key difference is that I have chosen to represent literal types as strings wrapped in strings as to differentiate them from primitives like `string` and `number`.

# Brief
Using the [TypeScript compiler API](https://github.com/microsoft/TypeScript/wiki/Using-the-Compiler-API), write a function that inputs a string containing a TypeScript type, and outputs an object literal representing the type.

Requirements
- Must have a function called visit
- Must have a function called convertToObject that calls the specified visit function
- Must not use CommonJS in your source files (e.g. require())
- Must use the official version of https://github.com/microsoft/TypeScript/wiki/Using-the-Compiler-API
    - e.g. import * as ts from "typescript";
- We do not expect the convertToObject function to support all kinds of types, but at a bare minimum should work with the example input in the below code block (i.e. type Button...)
- (Optional) Provide comments in your source code as much as you want, but keeping it concise

```
const visit = (node: ts.Node) => {
// implement the visit function here
};

const convertToObject = (type: string) => {
// implement the convertToObject function here
// this function must use the visit function above
};

// example usage
convertToObject(`type Button = {
        variant: "solid" | "text";
    };`);

/*
 * outputs
 *
 * {
 *   button: {
 *       variants: ["solid", "text"],
 *   },
 * }
 *
 */
