# HomeLab
A repository meant to work as a backup as well as showcase my learning in setting up self-hosted services

The repository is subdivided into directories with the name of the service it deploys. 

The main branch mimics the docker compose only setup I currently have with the default ports for each service as they appear in their respective repositories. Each directory has a README file explaining any nuances or additional information I consider useful given my specific installation hoping it can help someone if they run into the probles I had. the plan is to have a branch translating this into maybe ansible for easier management but that is entirely down the road and not set in stone. 

This is a list to all services currently living in this repository.

- Stalwart Mail Server
- Traefik
- Crowdsec
- NPM Plus (Nginx Proxy Manager)

In addition to my homelab I stretched out to use a VPS for some Self-Hosted services Like Stalwart behind the Traefik Reversee Proxy along with Komodo for VPS management. I am adding them as folder and writing the details of the setup in my blog at [blog.monchoplus.com](blog.monchoplus.com)

Now we are hosted on forgejo
