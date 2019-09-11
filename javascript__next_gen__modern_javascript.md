# Modern Javascript: ES6, NPM, Babel and WebPack

## Node and NPM

Node and NPM manage the packages needed for Javascript developement and to create a workflow.

It is made up of libraries that the application will use and development tools to assemble and compile the files needed for the app to work.

All the files for Node and NPM are store in a folder in the project called node_modules. A manifest of the files is listed in package.json.

### Common Commands

- `npm init` -- initializes a Node project
- `npm install` -- installs a package in the node project
- `npm install -g` -- installs a package globally for all users
- `npm install <packagename> --save` -- installs a package into a project and updates the package.json. This is used for package needed for the package to function on a server
- `npm install <packagename> --save-dev` -- Installed development packages that are only needed while developing the project. They are not copied to the server
- `npm uninstall <packagename> --save or --save-dev` -- uninstall a package and updates the package.json

### Recommened Packages

- live-server -- `sudo npm install -g live-server`

## WebPack

Webpack is used to combine multiple javascript files into a single file, since most browsers do not support modules yet.

To use webpack you first install webpack via npm, then create a webpack.config.js file.

This file can contain the following parts:

- `entry:` -- The location of the main javascript file that import all of the other files in the project
- `output` -- The location where to put the packed file. It is an object with two members.
  - `path` -- The path where the output file should go
  - `filename` -- The target filename for the packed file
- `mode` -- The mode that controls haw much the file is compressesed (development, production normally directly in the npm script)
- `plugins` -- Plugin that can extend functionality
  - `html-webpack-plugin`
- `loaders` --

## Babel

Babel convert ES6 and later to ES5
