# Libraries Used

-   [Baileys](https://github.com/WhiskeySockets/Baileys)
-   [Express](https://github.com/expressjs/express)

# Installation

1. Download or clone this repo.
2. Enter to the project directory.
3. Execute `yarn install` to install the dependencies.
4. Copy `.env.example` to `.env` and set the environment variables.

# Docker Compose

1. Follow the [Installation](#installation) procedure.
2. Update `.env` and set

```
MONGODB_ENABLED=true
MONGODB_URL=mongodb://mongodb:27017/whatsapp_api
```

3. Set your `TOKEN=` to a random string.
4. Execute

```
docker-compose up -d
```

# Configuration

Edit environment variables on `.env`

```a
Important: You must set TOKEN= to a random string to protect the route.
```

```env
# ==================================
# SECURITY CONFIGURATION
# ==================================
TOKEN=RANDOM_STRING_HERE
```

# Usage

1. `DEVELOPMENT:` Execute `yarn dev`
2. `PRODUCTION:` Execute `yarn start`

## Generate basic instance using random key.

To generate an Instance Key  
Using the route:

```bash
curl --location --request GET 'localhost:3333/instance/init' \
--data-raw ''
```

Response:

```json
{
    "error": false,
    "message": "Initializing successfull",
    "key": "d7e2abff-3ac8-44a9-a738-1b28e0fca8a5"
}
```

## WEBHOOK_ALLOWED_EVENTS

You can set which events you want to send to webhook by setting the environment variable `WEBHOOK_ALLOWED_EVENTS`

Set a comma seperated list of events you want to get notified about.

Default value is `all` which will forward all events.

Allowed values:

-   `connection` - receive all connection events
-   `connection:open` - receive open connection events
-   `connection:close` - receive close connection events
-   `presense` - receive presence events
-   `messages` - receive all messages event
-   `call` - receive all events related to calls
-   `call:terminate` - receive call terminate events
-   `call:offer` - receive call terminate event
-   `groups` - receive all events related to groups
-   `group_participants` - receive all events related to group participants

You can also use the Baileys event format example: `messages.upsert`

## Generate custom instance with custom key and custom webhook.

To generate a Custom Instance  
Using the route:

```bash
curl --location --request GET 'localhost:3333/instance/init?key=CUSTOM_INSTANCE_KEY_HERE&webhook=true&webhookUrl=https://webhook.site/d7114704-97f6-4562-9a47-dcf66b07266d' \
--data-raw ''
```

Response:

```json
{
    "error": false,
    "message": "Initializing successfull",
    "key": "CUSTOM_INSTANCE_KEY_HERE"
}
```

# Using Key

Save the value of the `key` from response. Then use this value to call all the routes.

## QR Code

Visit [http://localhost:3333/instance/qr?key=INSTANCE_KEY_HERE](http://localhost:3333/instance/qr?key=INSTANCE_KEY_HERE) to view the QR Code and scan with your device. If you take too long to scan the QR Code, you will have to refresh the page.

## Send Message

```sh
# /message/text?key=INSTANCE_KEY_HERE&id=PHONE-NUMBER-WITH-COUNTRY-CODE&message=MESSAGE

curl --location --request POST 'localhost:3333/message/text?key=INSTANCE_KEY_HERE' \
--header 'Content-Type: application/x-www-form-urlencoded' \
--data-urlencode 'id=919999999999' \
--data-urlencode 'message=Hello World'
```
