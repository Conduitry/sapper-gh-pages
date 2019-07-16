# Sapper on GitHub Pages

Deploy an exported Sapper site to GitHub Pages

## Server changes

`src/server.js` needs to be modified to mount the Sapper middleware at `process.env.BASE_NAME || '/'` by adding that as the first argument to `.use`:

```js
	.use(
		process.env.BASE_NAME || '/',
		...
	)
```

## Deployment

The included `deploy.sh` script first needs to be edited so that the `BASE_NAME` is the path that the exported site will live at. If you are deploying to `username.github.io/reponame`, this is `reponame`. If you are deploying to the root path of some other domain, this is `/`.

`deploy.sh` will build and export the Sapper site to `__sapper__/export`. Then it will create a commit on the `gh-pages` branch off `HEAD` which checks in only the exported files, brought up to the root of the repository, so they will be served from the right paths. Then it force pushes the `gh-pages` branch to `origin`.
