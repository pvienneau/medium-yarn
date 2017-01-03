# medium-yarn

## Notes

### Lockfiles

> **(1.)** "In the Node ecosystem, dependencies get placed within a node_modules directory in your project. However, this file structure can differ from the actual dependency tree as duplicate dependencies are merged together. The npm client installs dependencies into the node_modules directory non-deterministically. This means that based on the order dependencies are installed, the structure of a node_modules directory could be different from one person to another. These differences can cause “works on my machine” bugs that take a long time to hunt down.

> Yarn resolves these issues around versioning and non-determinism by using lockfiles and an install algorithm that is deterministic and reliable. These lockfiles lock the installed dependencies to a specific version, and ensure that every install results in the exact same file structure in node_modules across all machines. The written lockfile uses a concise format with ordered keys to ensure that changes are minimal and review is simple."

> **(1.)** "We also had to work around issues with npm's shrinkwrap feature, which we used to lock down dependency versions. Shrinkwrap files aren't generated by default and will fall out of sync if engineers forget to generate them, so we wrote a tool to verify that the contents of the shrinkwrap file matches what's in node_modules."

> **(11.)** The `yarn.lock` is similar to the composer.lock file that PHP developers are familiar with. The yarn.lock file locks down the exact versions of the packages that have been installed and all their dependencies. With this file, you can be certain that every member of your engineering team have the exact package versions installed and deployments can easily be reproduced without unexpected bugs.

#### Package Version Confidence

> **(12.)** In an ideal world of [semantic versioning](http://semver.org/), patched releases won’t include any breaking changes. This, unfortunately, is not always true. The strategy employed by npm may result into two machines with the same package.json file, having different versions of a package installed, possibly introducing bugs.

> To avoid package version mis-matches, an exact installed version is pinned down in a lock file. Every time a module is added, Yarn creates (or updates) a yarn.lock file. This way you can guarantee another machine installs the exact same package, while still having a range of allowed versions defined in package.json.

> In npm, the npm shrinkwrap command generates a lock file as well, and npm install reads that file before reading package.json, much like how Yarn reads yarn.lock first. The important difference here is that Yarn always creates and updates yarn.lock, while npm doesn’t create one by default and only updates npm-shrinkwrap.json when it exists.

### Compatibility

> **(1.)** "Compatibility with both the npm and bower workflows and supports mixing registries."

> **(5.)** Yarn supports installing packages from both `package.json` and `bower.json`. As of October 2016, it does not support installation of packages from both source files at the same time, and the bower installation is still somewhat buggy, but it seems that the goal here is to be able to serve both package managers.

> **(6.)** "**Important note**: As it stands right now there still seem to be some issues regarding Bower support. We are however confident that with the help of the community, these issues will be solved quickly as Yarn steps towards 1.0 in upcoming months."

#### Install from Multiple Registries

> **(11.)** Yarn offers you the ability to install JavaScript packages from multiple registries, such as npm, bower, your git repository, and even your local file system.

> This is particularly helpful for developers who constantly publish JavaScript packages. You can use this to test your packages before publishing them to a registry.

> _See **(11.)** for installation examples._

### Speed

> **(5.)** Yarn seems to already map its calls to the npm registry prior to fetching the packages, so it can allow itself to submit requests in parallel, speeding up the fetching process.

> **(11.)** Yarn efficiently queues up requests and avoids request waterfalls to maximize network utilization. It starts by making requests to the registry and recursively looking up each dependency. Next, it looks in a global cache directory to see whether the package has been downloaded before. If it hasn't, Yarn fetches the tarball package and places it in the global cache to enable it to work offline and eliminate the need to re-download.

> During install, Yarn parallelizes operations, which makes the install process faster.

> **(12.)** Whenever npm or Yarn needs to install a package, it carries out a series of tasks. In npm, these tasks are executed per package and sequentially, meaning it will wait for a package to be fully installed before moving on to the next. Yarn executes these tasks in parallel, increasing performance.

### Package caching

> **(5.)** Yarn caches the packages it fetches from the registry, meaning that subsequent installations of those packages don't require a second request to fetch the same packages. On one hand, this improves installation performances when installing packages into a project, while on the other hand, it allows you to install packages into your project while you're not connected to the internet, if that package is saved in Yarn's package cache.

### Determinism
> **(5.)** Npm is inherently non-deterministic in the resulting `node_modules` folder package structure because your dependency tree is dependent on the installation order of your packages. The `yarn.lock` file produced when installing packages through Yarn is used as a manifest of the installation order of each package, along with which version has been installed. This allows for other environments setting up the same project to use this lock file as instructions as to what packages to install, to what version, and in what order.

### Community Support

> **(10.)** Has already been adopted by Laravel community.

> **(6.)** Celebrated by Bower.

## Things to look up

+ Flat dependencies
+ post-pull commands through `package.json`? (Automatically running `yarn install` when we pull from the repository)

>This: https://gist.github.com/sindresorhus/6465739

## Resources

1. [Yarn: A new package manager for JavaScript](https://code.facebook.com/posts/1840075619545360)

2. [NPM vs Yarn Cheat Sheet](https://shift.infinite.red/npm-vs-yarn-cheat-sheet-8755b092e5cc#.g0kr8shvb)

3. [Yarn Official Website](https://yarnpkg.com)

4. [Example Yarn Package](https://github.com/yarnpkg/example-yarn-package)

5. [Video: Facebook Yarn vs NPM](https://www.youtube.com/watch?v=hMk_9RjX5KE)

6. [Using Bower with Yarn](https://bower.io/blog/2016/using-bower-with-yarn/)

7. [npm3 Non-determinism](https://docs.npmjs.com/how-npm-works/npm3-nondet)

8. [npm3 Dependency Resolution](https://docs.npmjs.com/how-npm-works/npm3)

9. [Video: Intro to Yarn Package Manager](https://www.youtube.com/watch?v=7n467QmiANM)

10. [Video: In Depth Learning YARN by Facebook](https://www.youtube.com/watch?v=9ZxwISnnBOU)

11. [5 Things You can do with Yarn](https://auth0.com/blog/five-things-you-can-do-with-yarn/)

12. [Yarn vs npm: Everything You Need to Know](https://www.sitepoint.com/yarn-vs-npm/)

13. [Semantic Versioning 2.0.0](http://semver.org/)

14. [npm-shrinkwrap](https://docs.npmjs.com/cli/shrinkwrap)
