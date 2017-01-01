# medium-yarn

## Notes

### Lockfiles

> **(1.)** In the Node ecosystem, dependencies get placed within a node_modules directory in your project. However, this file structure can differ from the actual dependency tree as duplicate dependencies are merged together. The npm client installs dependencies into the node_modules directory non-deterministically. This means that based on the order dependencies are installed, the structure of a node_modules directory could be different from one person to another. These differences can cause “works on my machine” bugs that take a long time to hunt down.

> Yarn resolves these issues around versioning and non-determinism by using lockfiles and an install algorithm that is deterministic and reliable. These lockfiles lock the installed dependencies to a specific version, and ensure that every install results in the exact same file structure in node_modules across all machines. The written lockfile uses a concise format with ordered keys to ensure that changes are minimal and review is simple.

### Compatibility

> **(1.)** Compatibility with both the npm and bower workflows and supports mixing registries.

## Speed

> **(5.)** "Yarn seems to already map its calls to the npm registry prior to fetching the packages, so it can allow itself to submit requests in parallel, speeding up the fetching process."

## Package caching

> **(5.)** "Yarn caches the packages it fetches from the registry, meaning that subsequent installations of those packages don't require a second request to fetch the same packages. On one hand, this improves installation performances when installing packages into a project, while on the other hand, it allows you to install packages into your project while you're not connected to the internet, if that package is saved in Yarn's package cache."

## Deterministric
> **(5.)** "Npm is inherently non-deterministic in the resulting `node_modules` folder package structure because your dependency tree is dependent on the installation order of your packages. The `yarn.lock` file produced when installing packages through Yarn is used as a manifest of the installation order of each package, along with which version has been installed. This allows for other environments setting up the same project to use this lock file as instructions as to what packages to install, to what version, and in what order." 

## Resources

1. [Yarn: A new package manager for JavaScript](https://code.facebook.com/posts/1840075619545360)

2. [NPM vs Yarn Cheat Sheet](https://shift.infinite.red/npm-vs-yarn-cheat-sheet-8755b092e5cc#.g0kr8shvb)

3. [Yarn Official Website](https://yarnpkg.com)

4. [Example Yarn Package](https://github.com/yarnpkg/example-yarn-package)

5. [Video: Facebook Yarn vs NPM](https://www.youtube.com/watch?v=hMk_9RjX5KE)
