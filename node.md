
npmrc config files:  
- per-project config file (/path/to/my/project/.npmrc)  
- per-user config file (~/.npmrc)  
- global config file ($PREFIX/npmrc)  
- npm builtin config file (/path/to/npm/npmrc)

npm gets its config settings from the command line, environment variables, and npmrc files.

The npm config command can be used to update and edit the contents of the user and global npmrc files.

npm config list : list all npm config settings.

node -v : outputs current node version.

npm -v : outputs current npm version.

npm config get prefix -g : outputs global package installation path.

npm prefix : Print the local prefix to standard out. This is the closest parent directory to contain a package.json file unless
-g is also specified.

npm prefix -g : value of the global prefix.

npm cache clean

npm ls -g --depth 0 - lists global node modules installed in system
