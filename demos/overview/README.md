# Overview Demo

This is intended to be basic introduction to Spin and Fermyon Cloud. This demo includes some slides to explain concepts. There is also a video of this entire demo and talk track in this directory which is also intended to be used at conference booths (with the audio off). At a conference it's intended that someone working the booth could provide the commentary when necessary, that it can be watched without audio and still get the concepts across.

## Prerequisites

* Install [Rust](https://www.rust-lang.org/tools/install)
  
## Talk Track

[open slides](https://fermyontech-my.sharepoint.com/:p:/g/personal/chris_matteson_fermyon_com/EbXVi_Hr-m9KjoRo1kMBLLoBUgiAmn6YG8viBpAPIvjcxA?e=bEMBk7)

Fermyon orginated from the gap between containers and existing serverless solutions. We are a Functions as a service solution powered by WebAssembly. Spin combines the best of serverless, with infinite scale and a cost effective model with the fast response times and ease of development of containers.

```
next slide
```

Fermyon accomplishes this by using WebAssembly under the hood to provide unique advantages. Our typical app image is two orders of magnitude smaller than a container.

```
next slide
```

Our cold start times are <1ms, elimninating the performance penalties which makes requires certain workloads to run on dedicated infrastructure regardless of how intermittant they are.

```
next slide
```

The outcome of these technical advantages is that Spin can easily scale down to zero, is secure by default, and can provide better performance for less money.

```
next slide
```

Finally, Spin can use any language which can compile to WebAssembly, which includes all popular languages.

Let's see a demo of this working.

```
switch to VSCode
```

As you can see, we already have Spin installed. Here you can see the various commands available

```
spin
```
Spin includes a bunch of templates to make getting started faster and easier. As you can see we already have numerous templates installed by default. These include functions triggered via http and redis events, as well as a few special emplates that utilize prebuilt WebAssembly components that provide common use cases for redirection and hosting static files. 

```
spin templates list
```

Let's create a new Spin app using the http-rust template. We'll then provide a description and accept defaults for base and path.

```
spin new http-rust hello
Description: Hello Fermyon
Enter twice (accept defaults for Base and Path)
cd hello
```

Here we can see the spin.toml file which is the starting point for all spin applications. We have basic information of the app at the top and components, of which there can be multiple. For this example you can see the path to the webassembly component which Spin uses. Since we are building our own component and not using a prebuilt one like Redirect, we also need to tell Spin how to build the webassembly component for this language. Here the template has already provided this command for us with Rust. 

```
Open hello/spin.toml in VSCode
Highlight path to wasm file
Highlight build command
```

Here we see the actual rust library which the template has pre-populated for us. You can see the spin sdk which we import and allows us to write our function. Each spin function accepts the http request and returns a response. This is a basic hello world example, so we'll just modify what is returned slightly.

```
Open hello/src/lib.rs
Highlight "use spin_sdk"
Highlight "fn handle_hello(req: Request..."
Change text to "Hello from the Fermyon Booth"
Save changes
```

Our next step is to build the application using the Spin Build command. How long this takes varies by language with interpreted languages python being almost instantaneous while the optimization of rust compilation takes longer. At the end we will have created our wasm component.

```
spin build
ls target/wasm32-wasi/release
Highlight "hello.wasm"
```

Now we can run the application locally using Spin up.

```
spin up
Click link to http://localhost:3000
ctrl-c to kill spin app when done
```

Next let's deploy to the cloud where we can share this application with the world. We can use Spin login to authenticate this terminal using a one time code. 

```
spin login
Copy one-time code and click link to authorize
Authorize terminal and return to VScode
```

And let's deploy. This takes maybe twenty seconds to bundle the application up and send it to Fermyon Cloud. This isn't the only way to deploy Spin applications in production, we also can be run as a service via something like systemd or in Kubernetes, including cloud hosted clusters like AKS. <Pause for completion> Now that our application is deployed, we can follow the link and see everything is working.

```
spin deploy
Click link to deployed application 
```

Spin apps are very fast with <1 ms cold start times. We can see when hitting this in the cloud the response returns in a fraction of a second which mostly comes from the roundtrip. We can run the same app locally and it's even less.

```
time curl <spin app url>
spin up &
time curl http://localhost:3000
fg
ctrl-c to kill spin app when done
```

Todo: Load test dialogue 

```
Todo: Load test commands
```

Next we can login to the Fermyon Cloud dashboard and see our application along with requests and logs.

```
Login to https://cloud.fermyon.com
Click on hello application
```

Thanks for watching this demo! We encourage you to take Spin for a spin yourself! Use our quickstarts to get working with Spin and Fermyon Cloud, then join our Discord community to become part of the conversation!

## Key Takeaways

* Spin is easy to use
* Spin lets you build applications very quickly
* Spin can be deployed in production to lots of places, including Fermyon Cloud
* Spin is very performant
