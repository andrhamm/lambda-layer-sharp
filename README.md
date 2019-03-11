# lambda-layer-sharp

In order to use the [Sharp](https://github.com/lovell/sharp) package in a Lambda, it must be [compiled specially](http://sharp.pixelplumbing.com/en/stable/install/#aws-lambda) for the Lambda environment. We use a Lambda Layer to avoid conflicts with the node_modules for local development.

## Usage

Install Serverless framework globally

    npm install -g serverless

Deploy this layer as a standalone CloudFormation Stack

    serverless deploy

Then, in your other Serverless service's `serverless.yml`, reference this layer like so:

    ${cf:lambda-layer-dev.SharpLambdaLayer} # where dev is the stage

## Updating version of Sharp

Update the version in the `package.json`, delete the `layer/nodejs/node_modules` directory then, with Docker running, run:

    npm run build

Then

    serverlessd deploy
