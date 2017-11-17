[Back to the main page](/../../)

# Examples

## User service in both modes

A simple user service that shows how to build the same application using both modes:
* [User service in function mode](https://github.com/modofunjs/modofun/tree/master/examples/function-mode)
* [User service in request/response mode](https://github.com/modofunjs/modofun/tree/master/examples/reqres-mode)

This example includes middleware to require authentication on certain requests, using JWT tokens. It also uses an Express server to mimic a serverless execution environment locally without having to install an emulator. Try it out:

```bash
git clone https://github.com/modofunjs/modofun.git

cd modofun/examples/function-mode
npm install
npm start

curl -d '{"credentials": "X"}' -H "Content-Type: application/json" -X POST http://localhost:3000/authenticate
```

## Google Cloud Functions deployment and testing

[An example TODO service that includes scripts to run on Google Cloud Functions, or in the emulator](https://github.com/modofunjs/modofun/tree/master/examples/google-cloud-functions). Install it like this:

```bash
git clone https://github.com/modofunjs/modofun.git

cd modofun/examples/google-cloud-functions
npm install
```

To try it out on Google Cloud, first [follow Google's instructions](https://cloud.google.com/functions/docs/quickstart) to enable the Cloud Functions API, and install the SDK and components..

Create a stage bucket on Cloud Storage. For the script to work without changes, use the bucket name: _modofun-example-src_.

```bash
gsutil mb -p [PROJECT_ID] gs://modofun-example-src
```

Afterwards, when you're ready to deploy the function, use the deploy script:

```bash
npm run deploy

curl https://us-central1-[PROJECT_ID].cloudfunctions.net/myModofunExample/addTodo/joe?todo=Do+the+dishes

curl https://us-central1-[PROJECT_ID].cloudfunctions.net/myModofunExample/getTodos/joe
```

Or try it out using the [local emulator for Google Cloud Functions](https://cloud.google.com/functions/docs/emulator):

```bash
npm run start-emulator

npm run deploy-to-emulator

curl http://localhost:8010/[PROJECT_ID]/us-central1/myModofunExample/addTodo/joe?todo=Do+the+dishes

curl http://localhost:8010/[PROJECT_ID]/us-central1/myModofunExample/getTodos/joe
```

## AWS Lambda deployment and testing

_Coming soon..._

## Real-world application

There’s also a [real-world example](https://github.com/fptavares/record-scrobbler) that includes:
* [A GraphQL endpoint deployed on Google Cloud Functions](https://github.com/fptavares/record-scrobbler/tree/master/web-api)
* [An AWS Lambda deployment using the default function mode](https://github.com/fptavares/record-scrobbler/tree/master/discogs-service)
* [A Google Cloud Functions deployment using the request/response mode](https://github.com/fptavares/record-scrobbler/tree/master/lastfm-service)

All using modofun, combined with Gulp, Babel and other cool technology.