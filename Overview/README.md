# Overview Demo
This is intended to be basic introduction to Spin and Fermyon Cloud. This demo includes some slides to explain concepts. There is also a video of this entire demo and talk track in this directory which is also intended to be used at conference booths (with the audio off). At a conference it's intended that someone working the booth could provide the commentary when necessary, that it can be watched without audio and still get the concepts across.

## Prerequisites
* Install [Rust](https://www.rust-lang.org/tools/install)
  
## Talk Track
    |                       Steps                          |                    Dialogue                      |
    |------------------------------------------------------|--------------------------------------------------|
    | Todo: Introduction Slides                            | Todo: Dialogue for introduction slides           |
    |------------------------------------------------------|--------------------------------------------------|
    | * Open VSCode to a blank directory                   | As you can see, we already have Spin installed.  |
    | * `spin`                                             | Here you can see the various commands available  |
    |------------------------------------------------------|--------------------------------------------------|
    | * `spin templates list`                              | Spin includes a bunch of templates to make       |
    |                                                      | getting started faster and easier. As you can see|
    |                                                      | we already have numerous templates installed by  |
    |                                                      | default. These include functions triggered via   |
    |                                                      | http and redis events, as well as a few special  |
    |                                                      | templates that utilize prebuilt WebAssembly      |
    |                                                      | components that provide common use cases for     |
    |                                                      | redirection and hosting static files.            |
    |------------------------------------------------------|--------------------------------------------------|
    | * `spin new http-rust hello`                         | Let's create a new Spin app using the http-rust  |
    | * `Description: Hello Fermyon`                       | template. We'll then provide a description and   |
    | * Enter twice (accept defaults for Base and Path)    | accept defaults for base and path.               |
    | * `cd hello`                                         |                                                  |
    |------------------------------------------------------|--------------------------------------------------|
    | * Open hello/spin.toml in VSCode                     | Here we can see the spin.toml file which is the  |
    | * Highlight path to wasm file                        | starting point for all spin applications. We have|
    | * Highlight build command                            | basic information of the app at the top and      |
    |                                                      | components, of which there can be multiple. For  |
    |                                                      | this example you can see the path to the         |
    |                                                      | webassembly component which Spin uses. Since we  |
    |                                                      | are building our own component and not using a   |
    |                                                      | prebuilt one like Redirect, we also need to tell |
    |                                                      | Spin how to build the webassembly component for  |
    |                                                      | this language. Here the template has already     |
    |                                                      | provided this command for us with Rust.          |
    |------------------------------------------------------|--------------------------------------------------|
    | * Open hello/src/lib.rs                              | Here we see the actual rust library which the    |
    | * Highlight "use spin_sdk"                           | template has prepopulated for us. You can see the|
    | * Highlight "fn handle_hello(req: Request..."        | spin sdk which we import and allows us to write  |
    | * Change text to "Hello from the Fermyon Booth"      | our function. Each spin function accepts the     |
    | * Save changes                                       | http request and returns a response. This is a   |
    |                                                      | basic hello world example, so we'll just modify  |
    |                                                      | what is returned slightly.                       |
    |------------------------------------------------------|--------------------------------------------------|
    | * `spin build`                                       | Our next step is to build the application using  |
    | * `ls target/wasm32-wasi/release`                    | the Spin Build command. How long this takes      |
    | * Highlight "hello.wasm"                             | varies by language with interpreted languages    |
    |                                                      | python being almost instantious while the        |
    |                                                      | optimization of rust compliation takes longer. At|
    |                                                      | the end we will have created our wasm component. |
    |------------------------------------------------------|--------------------------------------------------|
    | * `spin up`                                          | Now we can run the application locally using Spin|
    | * Click link to http://localhost:3000                | up.                                              |
    | * ctrl-c to kill spin app when done                  |                                                  |
    |------------------------------------------------------|--------------------------------------------------|
    | * `spin login`                                       | Next let's deploy to the cloud where we can share|
    | * Copy one-time code and click link to authorize     | this application with the world. We can use Spin |
    | * Authorize terminal and return to VScode            | login to authenticate this terminal useing a one |
    |                                                      | time code.                                       |
    |------------------------------------------------------|--------------------------------------------------|
    | * `spin deploy`                                      | And let's deploy. This takes maybe twenty seconds|
    | * Click link to deployed application                 | to bundle the application up and send it to      |
    |                                                      | Fermyon Cloud. This isn't the only way to deploy |
    |                                                      | Spin applications in production, we also can be  |
    |                                                      | run as a service via something like systemd or in|
    |                                                      | Kubernetes, including cloud hosted clusters like |
    |                                                      | AKS. <Pause for completion> Now that our         |
    |                                                      | application is deployed, we can follow the link  |
    |                                                      | and see everything is working.                   |
    |------------------------------------------------------|--------------------------------------------------|
    | * `time curl <spin app url>`                         | Spin apps are very fast with <1 ms cold start    |
    | * spin up &                                          | times. We can see when hitting this in the cloud |
    | * `time curl http://localhost:3000`                  | the response returns in a fraction of a second   |
    | * `fg`                                               | which mostly comes from the roundtrip. We can run|
    | * ctrl-c to kill spin app when done                  | the same app locally and it's even less          |
    |------------------------------------------------------|--------------------------------------------------|
    | * Todo: Loadtest                                     | Todo: Loadtest dialogue                          |
    |------------------------------------------------------|--------------------------------------------------|
    | * Login to https://cloud.fermyon.com                 | Next we can login to the Fermyon Cloud dashboard |
    | * Click on hello application                         | and see our application along with requests and  |
    |                                                      | logs.                                            |
    |------------------------------------------------------|--------------------------------------------------|
    | Todo: Concluding Slides                              | Todo: Dialogue for concluding slides             |
    |------------------------------------------------------|--------------------------------------------------|

## Key Takeaways
* Spin is easy to use
* Spin lets you build applications very quickly
* Spin can be deployed in production to lots of places, including Fermyon Cloud
* Spin is very performant
