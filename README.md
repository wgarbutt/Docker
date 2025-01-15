## Services

Alright, let's break down the containers in this setup:

### Media Stack
- **Plex**: My personal Netflix. All my media, streamed wherever I want.
- **Sonarr and Radarr**: These guys automatically hunt down and grab my TV shows and movies.
- **SABnzbd**: The reliable workhorse for downloading from Usenet.

### Development and Operations
- **Portainer**: Makes managing Docker containers a breeze with a nice web UI.
- **GitHub Runner**: My new CI/CD buddy (more on this later).

### Productivity and Personal Management
- **Dashy**: A slick dashboard to access all my services quickly.
- **Actual Budget**: Keeps my finances in check without relying on cloud services.
- **Tandoor**: Because even my recipes deserve a fancy management system.
- **Paperless-ngx**: Helping me pretend I'm organised by digitizing my documents.

### Monitoring and Backup
- **Uptime Kuma**: Keeps an eye on all my services and lets me know if something's acting up.
- **Duplicati**: Backs up my stuff so I don't lose my mind if something crashes.

### Database and Caching
- **PostgreSQL**: The sturdy database behind a bunch of my services.
- **Redis**: Speedy in-memory data store, mainly for Authentik but handy for other stuff too.

## Networking and Volumes

I've got a dedicated network called `reverse_proxy` for all these services to chat securely. For data storage, I'm using Docker volumes with bind mounts to my host system. Makes backups and migrations way less of a headache.

## Automated Deployment with GitHub Actions

Recently, I leveled up my game by swapping out Jenkins for a GitHub Actions workflow with a self-hosted runner. It's made deploying changes to my homelab setup smoother than ever. Here's what happens when I push changes to the `main` branch:

### GitHub Actions Workflow

The workflow kicks off automatically on every push to `main`, and it does a few key things:

1. **Gitleaks Scan**: Checks for any accidental commits of sensitive info.
2. **Linting Scan**: Makes sure my code doesn't look like a dumpster fire.
3. **Local Runner Deployment**: If all checks pass, it deploys the changes right on my homelab.
