Integrating a Linux terminal into an HTML page to run Linux commands directly from a web browser is a complex task that typically involves the use of a technology called a "web-based terminal emulator." This allows you to provide a terminal-like interface within your HTML page.

One popular tool for achieving this is called "xterm.js." It's a JavaScript library that provides a terminal emulation in the browser. Here's how you can integrate it into your HTML page:

**1. Include xterm.js and xterm.css in your HTML:**

```html
<!DOCTYPE html>
<html>
<head>
    <title>Web Terminal</title>
    <link rel="stylesheet" href="xterm.css">
</head>
<body>
    <div id="terminal-container"></div>
    <script src="xterm.js"></script>
    <script>
        // Your JavaScript code for setting up and using xterm.js
    </script>
</body>
</html>
```

**2. Set up xterm.js in JavaScript:**

In the `<script>` section of your HTML, you'll need to set up xterm.js. Here's a basic example:

```javascript
const { Terminal } = require('xterm');
const { FitAddon } = require('xterm-addon-fit');

const terminal = new Terminal();
const fitAddon = new FitAddon();

// Attach the terminal to a DOM element
terminal.open(document.getElementById('terminal-container'));
terminal.loadAddon(fitAddon);

// Fit the terminal to the container size
fitAddon.fit();

// Create a pseudo-terminal (PTY) for shell access
const pty = new Pty(); // You'll need a library for this, e.g., node-pty

// Connect the terminal to the PTY
terminal.attach(pty);

// Handle input and output between the terminal and PTY
terminal.onData(data => {
    pty.write(data);
});

pty.on('data', data => {
    terminal.write(data);
});
```

**3. Node.js Backend:**

To provide actual Linux functionality, you'll need a backend server, often implemented in Node.js, that can execute Linux commands and provide responses to the terminal.

Please note that setting up a fully functional web-based terminal with xterm.js involves more detailed configurations and potentially additional libraries for running commands securely on the server-side. It's also important to implement security measures to prevent malicious use.

This is a simplified example, and the actual implementation can be quite complex. If you're not experienced with web-based terminals and server-side security, it may be helpful to consult with a web development expert or consider using pre-built solutions designed for this purpose.