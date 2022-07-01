# UA Local Development Experience

As money is at stake, we take security at Ultimate Tournament very seriously.
One consequence of this is that we're running your game inside a special environment that is more under 
our control. Only servers run that way are able to access our real API.

To make your lives easier when testing locally, this repo gives you an environment that fakes our
environment to some extent.

## How this works

This environment is based on Docker, which **you must install first and can download [here](https://www.docker.com/products/docker-desktop/)**.

You don't really need to understand the details of Docker to use it here. It's basically a way to run software in a standardized
way, so it's easy to put them onto (Linux) servers. The nice thing about it is that you can run exactly the same thing
locally as on the server and thus be pretty sure, that it will work there too.

After you've installed Docker, open a terminal inside this repository's directory and check if Docker was installed properly with
`docker-compose version`.

## Running your game

If, as part of your SDK integration, you haven't already selected created a Dockerfile for your backend, select one from the examples in this repo and copy it here as `Dockerfile.backend`.

Next, copy your frontend build into `game-bin/frontend/` and your backend build into `game-bin/backend/`.

Now run `docker-compose up` to run the environment and your game. If everything works as intended, you should be able to access your frontend
under http://localhost:8080

## Running the next session

We don't recycle servers to ensure our player's privacy. Therefore we stop everything and shut down the server after a game session has ended.

In this local environment, this doesn't quite work. So after your game has finished, just hit `CTRL-C` to shutdown the environment and start it again 
with `docker-compose up`. This should only take a few seconds.

If you're done you can also run `docker-compose kill` and `docker-compose rm` to cleanup any unused resources.

## Troubleshooting

### Haproxy fails to start

If you get a message saying `could not resolve address 'backend'`, then scroll up a bit. The actual issue is in a failed backend container.

### Backend fails with `... no such file or directory`

There could be multiple reasons for this error. But the fundamental issue is that the container only contains what we explicitely add to it.

For Unity, remember to build with the `IL2CPP` scripting backend. This gives you a very self-contained build.

If you can't figure out what is missing, just reach out and we'll help you fix the Dockerfile.
