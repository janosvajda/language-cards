# Language Card app

## Set up

Clone this project, then run

`docker-compose run app npm install`

Copy `.env.example` to `.env`, generate a unique string that will be used for JWT encoding and decoding and set it as the `JWT_SECRET` variable.

Start the app in watch and debug mode with

`docker-compose up`

Create database tables while docker-compose is up

`docker exec -it app npm run typeorm schema:sync`

Seed some data

`docker exec -it app node scripts/seed.js`

## Test

To execute tests, run

`docker exec -it app npm run test`

## Debug

With `docker-compose up` the app starts with debug mode. So you can just run the `Attach to docker` task and debug the app. This task is defined in `.vscode/launch.json` as well as some other debugging tasks.

## Ard

The `ard` script gives you an environment to tinker with your app and it gives you top-level await. It registers the app instance, repositories, entity classes and the factory function globally so you can easily access and use it. There is a js version and a ts version.

The js version needs the app to be compiled first with `tsc` or `nest build`, but then you can run it without waiting for typescript compilation. Run it with `npm run ard` or:

`docker exec -it app npm run ard`

It uses the code from `dist` folder.

The ts version allows you to run ard without compiling typescript beforehand. It uses the code from `src`. There are two ways to run it. The `npm run ts-ard` script allows you to write typescript code in the REPL. The `npm run ard-from-src` script does not give you typescript in REPL but allows top-level await like regular `npm run ard`.

The `ts-ard` is not working correctly because TypeScript does not see the registered global variables. Maybe there is a way around this.

## Env variables

There is one important environment variable that impacts the app setup - `NODE_ENV`. Default value is `"develop"`. Running tests will set NODE_ENV to `"test"`. The only difference at the moment is that test env will use `.env.test` instead of `.env`.