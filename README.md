# medium-yarn

## Notes

### Lockfiles

> **(1.)** In the Node ecosystem, dependencies get placed within a node_modules directory in your project. However, this file structure can differ from the actual dependency tree as duplicate dependencies are merged together. The npm client installs dependencies into the node_modules directory non-deterministically. This means that based on the order dependencies are installed, the structure of a node_modules directory could be different from one person to another. These differences can cause “works on my machine” bugs that take a long time to hunt down.

> Yarn resolves these issues around versioning and non-determinism by using lockfiles and an install algorithm that is deterministic and reliable. These lockfiles lock the installed dependencies to a specific version, and ensure that every install results in the exact same file structure in node_modules across all machines. The written lockfile uses a concise format with ordered keys to ensure that changes are minimal and review is simple.

### Compatibility

> **(1.)** Compatibility with both the npm and bower workflows and supports mixing registries.

## Resources

1. [Yarn: A new package manager for JavaScript](https://code.facebook.com/posts/1840075619545360)

2. [NPM vs Yarn Cheat Sheet](https://shift.infinite.red/npm-vs-yarn-cheat-sheet-8755b092e5cc#.g0kr8shvb)

3. [Yarn Official Website](https://yarnpkg.com)

4. [Example Yarn Package](https://github.com/yarnpkg/example-yarn-package)

5. [Difference between Brew, Yarn and NPM](http://stackoverflow.com/questions/40396611/what-is-the-difference-between-brew-yarn-and-npm)
