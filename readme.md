# across-tabs

Client-side messaging channel for sending data from one browser tab to another with the same origin. Think of it as a PubSub module that can send messages across multiple browser tabs.

To see a demo, open [this page](https://hermes.arnelle.me/) in multiple browser tabs.

## Usage

Install it in your project:


```bash
yarn add https://github.com/httpiago/across-tabs
// or
npm i https://github.com/httpiago/across-tabs --save
```

Import the package and use it:

```js
const acrossTabs = require('across-tabs')

acrossTabs.on('handshake', data => {
  acrossTabs.send('handshake back', data)
})

acrossTabs.send('handshake', 'hi')

```

## API

- **`send(topic, data, [includeSelf=false])`**: Send data to other browser tabs subscribed to a specified topic.
  - `topic` {string}: The name of the topic in which the data will be sent to.
  - `data` {Object|string}: The data to be sent. This needs to be a JSON-serializable object.
  - `includeSelf` {boolean} (optional, default=false): A boolean indicating whether the data should also be sent to the current tab.

  ```js
  hermes.send('some-topic', 'hello world');
  hermes.send('some-topic', { title: 'awesome' });
  hermes.send('some-topic', { title: 'awesome' }, true);
  ```

- **`on(topic, callback)`**: Add a callback function for a specified topic.
  - `topic` {string}: The name of the topic to subscribe to.
  - `callback` {Function}: The callback function, which accepts a single argument representing the data that was sent originally.

  ```js
  hermes.on('some-topic', function(data) {
    
  });
  ```

- **`off(topic, [callback])`**: Remove a callback function for a specified topic.
  - `topic` {string}: The name of the topic to unsubscribe from.
  - `callback` {Function} (optional): The callback function to remove, or don't provide in order to remove all callback functions for the `topic` topic.

  ```js
  hermes.off('some-topic', callbackFunction);
  hermes.off('some-topic');
  ```


## License

MIT License
