# Flying Circus Nodejs USB Serial Connection

Flying Circus is a MicroPython IDE. It has a [browser](https://github.com/murilopolese/flying-circus-web) and an [electron app](https://github.com/murilopolese/flying-circus-electron) version.

This repository contains a connection class for Flying Circus to interact with a MicroPython REPL via USB Serial. This will only work on a NodeJS environment (if it ever works).

# Usage

First install the dependencies by running `yarn install`.

Then require it to your project:

```javascript
var SerialConnection = require('flying-circus-connection-serial')
```

# Methods

The connection class implements the following methods:

```javascript
class Connection extends EventEmitter {
    constructor() {
        super()
    }
    /**
    * List all available serial ports (with vendor id)
    * @return {Promise} Resolves with an array of port objects
    */
    static listAvailable() {}
    /**
    * Opens a connection given an ip address and a password.
    * @param {String} ip Ip address without protocols or ports
    * @param {String} password MicroPython's WebREPL password
    */
    open(ip, password) {}
    /**
    * Closes current connection.
    */
    close() {}
    /**
    * Executes code in a string format. This code can contain multiple lines.
    * @param {String} code String of code to be executed. Line breaks must be `\n`
    */
    execute(code) {}
    /**
    * Evaluate a command/expression.
    * @param {String} command Command/expression to be evaluated
    */
    evaluate(command) {}
    /**
    * Send a "stop" command in order to interrupt any running code. For serial
    * REPL this command is "CTRL-C".
    */
    stop() {}
    /**
    * Send a command to "soft reset".
    */
    softReset() {}
    /**
    * Prints on console the existing files on file system.
    */
    listFiles() {}
    /**
    * Prints on console the content of a given file.
    * @param {String} path File's path
    */
    loadFile(path) {}
    /**
    * Writes a given content to a file in the file system.
    * @param {String} path File's path
    * @param {String} content File's content
    */
    writeFile(path, content) {}
    /**
    * Removes file on a given path
    * @param {String} path File's path
    */
    removeFile(path) {}
}
```

# Events

This class will fire the following events:

- `connected`: When connection is opened **and** authenticated
- `disconnected`: When connection is closed
- `output`: Whatever console output the board sends
- `execution-started`: Whenever "raw REPL" is started
- `execution-finished`: Whenever "raw REPL" is finished
