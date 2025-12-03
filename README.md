# Lambda Web Adapter Functional Testing Demo

Demonstrates using `sam local` to run functional tests against a Lambda function that uses the [AWS Lambda Web Adapter](https://github.com/awslabs/aws-lambda-web-adapter).
Notably, this works *locally* and *on CI/CD* (github actions, here).

The key insight: you can test your Lambda-deployed web app locally using `sam local start-api`, which runs the actual Docker container with the Lambda runtime—giving you confidence the app works in Lambda before deploying.
This is in addition to being able to test the docker container of your application directly, one of the develop lifecycle benefits of using the web adapter + docker - which we also test here both locally and on ci/cd.

## Setup

```bash
uv sync
```

## Running Tests

```bash
# Build both Docker and SAM
docker build -t hello-world-lambda .
sam build

# Run all tests
uv run pytest tests/test_functional.py -v
```

The tests spin up:
1. **Docker container directly** — validates the app works as a web server
2. **SAM local** — validates the app works inside the Lambda runtime with the Web Adapter
