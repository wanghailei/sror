# Deploy



## Docker



****

## Kamal

Kamal offers zero-downtime deploys, rolling restarts, asset bridging, remote builds, accessory service management, and everything else you need to deploy and manage your web app in production with Docker. 

If you want to run on your own hardware, or even just have a clear migration path to do so in the future, you need to carefully consider how locked in you get to these commercial platforms.

Kamal seeks to bring the advance in ergonomics pioneered by these commercial offerings to deploying web apps anywhere.

This approach gives you enormous portability. When you’re not locked into a single provider from a tooling perspective, there are a lot of compelling options available.

Ultimately, Kamal is meant to compress the complexity of going to production using open source tooling that isn’t tied to any commercial offering. 

No need to ensure that the servers have just the right version of Ruby or other dependencies you need. That all lives in the Docker image now. You can boot a brand new Linux server, add it to the list of servers in Kamal, and it’ll be auto-provisioned with Docker, and run right away. And the images built for Kamal can be used for CI or later introspection.

Kubernetes is a beast. Running it yourself on your own hardware is not for the faint of heart. It’s a fine option if you want to run on someone else’s platform, either transparently [like Render](https://thenewstack.io/render-cloud-deployment-with-less-engineering/) or explicitly on AWS/GCP, but if you’d like the freedom to move between cloud and your own hardware, or even mix the two, Kamal is much simpler. You can see everything that’s going on, it’s just basic Docker commands being called.

Docker Swarm is much simpler than Kubernetes, but it’s still built on the same declarative model that uses state reconciliation. Kamal is intentionally designed around imperative commands, like Capistrano.
