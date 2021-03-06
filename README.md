# React-based Chatroom Component for Rasa Stack

[![CircleCI](https://circleci.com/gh/scalableminds/chatroom.svg?style=svg)](https://circleci.com/gh/scalableminds/chatroom)

<a href="https://npm-scalableminds.s3.eu-central-1.amazonaws.com/@scalableminds/chatroom@master/demo.html"><img src="https://npm-scalableminds.s3.amazonaws.com/%40scalableminds/chatroom/demo.gif" alt="Demo" width="409" height="645" /></a>

[Watch a demo of our Chatroom in action](https://npm-scalableminds.s3.eu-central-1.amazonaws.com/@scalableminds/chatroom@master/demo.html)

[Try a live chatbot](https://scalableminds.com/)

## Features

* React-based component
* Markdown, Images, Buttons
* Customizable with SASS variables
* Generates a unique session id and keeps it in `sessionStorage`
* Queues consecutive bot messages for better readability
* Demo mode included (ideal for scripted screencasts)
* Hosted on S3 for easy use
* Includes a `BotServerChannel` for use with [Rasa Core](https://github.com/rasahq/rasa_core) (under `rasa_utils`)

## Usage

```html
<head>
  <link rel="stylesheet" href="https://npm-scalableminds.s3.eu-central-1.amazonaws.com/@scalableminds/chatroom@master/dist/Chatroom.css" />
</head>
<body>
  <div class="chat-container"></div>

  <script src="https://npm-scalableminds.s3.eu-central-1.amazonaws.com/@scalableminds/chatroom@master/dist/Chatroom.js"/></script>
  <script type="text/javascript">
    var chatroom = window.Chatroom({
      host: "http://localhost:5002",
      title: "Chat with Mike",
      container: document.querySelector(".chat-container"),
      welcomeMessage: "Hi, I am Mike. How may I help you?"
    });
    chatroom.openChat();
  </script>
</body>
```

### Basic usage

* Clone repository
* Install frontend dependencies `yarn install`
* Build frontend files `yarn build`
* Create an HTML page for your Chatroom (see usage example above or modify [index.html](./index.html))
* Make sure to adjust the `host` option. Use `http://localhost:5002` when testing locally
* Run `yarn serve` to launch a web server with your Chatroom on `http://localhost:8080`
* Integrate with a Rasa Core project (see standard or custom project below)

### Usage with a standard Rasa Core project

* Copy `rasa_utils` to your project
* Install the Python dependencies from `rasa_utils/requirements.txt`
* Run your bot with `python -m rasa_utils.bot -d models/current/dialogue -u models/current/nlu`
* The bot server will be available at `0.0.0.0:5002`


### Usage with a custom Rasa Core project

* Copy the `rasa_utils/bot_server_channel.py` to your project
* Install the Python dependencies from `rasa_utils/requirements.txt`
* Register the `BotServerInputChannel` with your Rasa Core `Agent` (see below)
* Run your bot. By default the bot server will be available at `0.0.0.0:5002`

```python
from bot_server_channel import BotServerInputChannel

# Creating the Interpreter and Agent
def load_agent(): ...

# Creating the server
def main_server():
    agent = load_agent()
    channel = BotServerInputChannel(agent)
    agent.handle_channel(channel)

main_server()
```

## Development

### Install dependencies

```
yarn install
```

### Continuously build the Chatroom component

```
yarn watch
yarn serve
```

Open `http://localhost:8080/demo.html` in your browser.

## Build

```
yarn build
```

Distributable files will be created in folder `dist`.

## License

AGPL v3

Made by [scalable minds](https://scalableminds.com)
