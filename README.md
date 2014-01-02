# Evented Forever

[Forever][0] extended with an `--eventFile` option to catch events (stop, restart...) through a file with listeners.

## Installation

``` bash
  $ [sudo] npm install evented-forever -g
```

## Example

``` bash
  $ forever start --eventFile sendMeMailOnRestart.js yourApp.js
```

Then create a file `sendMailOnRestart.js` with listeners:

``` js
  //file sendMailOnRestart.js
  var email = require('emailjs');

  //define a listener for the "restart" event
  exports.restart = function() {
    email.server.connect({
      user: 'crash', 
      password: 'password', 
      host: 'smtp.gmail.com'
    }).send({
      from: 'crash@gmail.com',
      to: 'you@gmail.com',
      subject: 'Your app has crashed',
      text: 'Go fix your app!'
		});
  }
```

Available events: "error", "start", "stop", "restart", "exit", "stdout", "stderr". (more details [here][1]).

[0]: http://github.com/nodejitsu/forever
[1]: https://github.com/nodejitsu/forever-monitor#events-available-when-using-an-instance-of-forever-in-nodejs
