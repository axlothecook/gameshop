# Game Shop
A full-stack demo online gaming store. Browse games, sort, filter and search them, create, view, edit or delete games, genres and developers with image uploads. The project is split across three repositories:

### [Front end](https://github.com/axlothecook/Gaming-shop-frontend)	
The public site whose UI is built with SvelteKit and is rendered on the server. 

### [Back end](https://github.com/axlothecook/Gaming-Shop)	
A REST API built with Node.js, Express and MongoDB. Images are stored on Cloudflare R2.

### [Deploy](https://github.com/axlothecook/gaming-shop-deploy)	
Holds the config files that run the whole project on my Raspberry Pi: the Docker Compose stack and the Cloudflare Tunnel setup.
<br />


## How it fits together
I made a graph that shows how the repos connect at runtime. Basically the Cloudflare Tunnel sends visitors straight to the frontend; the frontend talks to the backend server-to-server inside the Docker network. The data is stored in MongoDB as documents, along with links to the R2 images. The backend and the database have no public address.

![image](https://github.com/user-attachments/files/30160010/lana-segovic-cv.pdf)

<br />

## Deployment 
The project is deployed via my [CI/CD pipeline](https://github.com/axlothecook/homelab-ci-cd):
(1) a push to the frontend runs its tests, 
(2) CI builds the arm64 image, 
(3) the Pi pulls it and restarts the stack

The backend image is build-only, so a backend change goes live with the next stack restart.
<br />

## Tech stack
Front end: [SvelteKit](https://svelte.dev/docs/kit), [TypeScript](https://www.typescriptlang.org), [Vite](https://vite.dev), [Vitest](https://vitest.dev), [Sass](https://sass-lang.com) + my own [sass library](https://github.com/axlothecook/axlothecook-sass-library) <br />
Back end: [Node.js](https://nodejs.org), [Express 5](https://expressjs.com), [MongoDB](https://www.mongodb.com), [multer](https://github.com/expressjs/multer), [express-validator](https://express-validator.github.io), [Cloudflare R2](https://developers.cloudflare.com/r2/) <br />
Deploy: [Docker Compose](https://docs.docker.com/compose/), [GitHub Actions](https://github.com/features/actions) (GHCR, arm64), [Tailscale](https://tailscale.com) (CI to Pi), [Cloudflare Tunnel](https://developers.cloudflare.com/cloudflare-tunnel/)
