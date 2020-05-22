# My Service

Hanami / gRPC fusion. This service does... what?

## System Architecture

- [30k ft view](https://drive.google.com/file/d/1cRxMR6YJ01uNnrpi4M1xT93CrC8Mn6dO/view)
- [Data model](https://dbdiagram.io/d/5d68c207ced98361d6de0cd6)

## Setup

This service makes heavy use of docker and docker compose. Setting up docker is beyond the scope of this readme.

```shell
mkdir ~/projects/cardbinder/
cd ~/projects/cardbinder/
git clone git@github.com:cardbinder/my_service.git
git clone git@github.com:cardbinder/protos.git

cd my_service
docker-compose up -d # you might have to kick this a few times...
docker-compose run --rm bundle exec hanami db prepare
docker-compose run --rm bundle exec rake seed:things
docker-compose run --rm bundle exec rake grpc:fetch_thing
```

How to build gRPC files (when you change applicable `.proto` files):

```shell
% docker-compose run --rm protoc
```

How to run various Hanami commands:

```shell
% docker-compose run --rm bundle exec hanami console
% docker-compose run --rm bundle exec hanami g model NewModel
```

How to prepare (create and migrate) DB for `development` and `test` environments:

```shell
% docker-compose run -e HANAMI_ENV=test --rm bundle exec hanami db prepare
% docker-compose run --rm rpsec
```

## Deployment

This should be done for you via CI/CD, but in case you need to manually push an image

```shell
docker build -t docker.pkg.github.com/cardbinder/my_service/my_service:0.1.0 .
docker push docker.pkg.github.com/cardbinder/my_service/my_service:0.1.0
```

## Reading

Explore Hanami [guides](https://guides.hanamirb.org/), [API docs](http://docs.hanamirb.org/1.3.3/), or jump in [chat](http://chat.hanamirb.org) for help. Enjoy! 🌸

Explore gRPC [guides](https://grpc.io/docs/tutorials/basic/ruby), or jump in [chat](https://gitter.im/grpc/grpc) for help.

Learn about [protobuf](https://developers.google.com/protocol-buffers/docs/proto3).

Learn about [Docker](https://docs.docker.com/compose/gettingstarted).

Learn about GitHub [Actions](https://help.github.com/en/actions/reference/workflow-syntax-for-github-actions).
