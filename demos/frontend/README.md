# Running front-end applications with Spin

This demo showcases how to build and front-end applications with Spin.

## Prerequisites

- [NPM](https://docs.npmjs.com/downloading-and-installing-node-js-and-npm)
  
## Talk Track

With Spin and Fermyon Cloud, you can run fullstack serverless applications. Part of that is being able to run front-end applications. In this example, we will see how to build a Next.js application, run it anywhere with Spin, then deploy it to Fermyon Cloud.

First, let's create a new application with Spin based on the `nextjs-frontend` template:

```
$ spin new nextjs-frontend my-nextjs-app --allow-defaults
# your new application has been created in the my-nextjs-app directory
```

Next, we need to install the dependencies, then build the application:

```
$ npm install && spin build
Successfully ran the build command for the Spin components.
```

We can now run the application locally — a full Next.js application:

```
$ spin up
Serving http://127.0.0.1:3000
Available Routes:
  my-nextjs-app: http://127.0.0.1:3000 (wildcard)
```

How does this work? Looking at `spin.toml`, it serves the `out/` directory, which contains the exported Next.js app. For every request, a new Wasm instance is created that handles the incoming request, then it is terminated.

Let's deploy the application to Fermyon Cloud:

```
$ spin deploy
```

## Key Takeaways

* Spin can serve any statically exported front-end or single page application
