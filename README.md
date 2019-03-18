# yarn-workspace-nohoist-issue

To reproduce, run `yarn` from root (clean install.)  You should see something like `error An unexpected error occurred: "ENOENT: no such file or directory, lstat '/yarn-workspace-nohoist-issue/packages/b/node_modules/css-loader'".`

Notes:
- Narrowed down from our real-life dependencies to `css-loader` in package b using half splitting.  However, the actual file/directory that was missing changed throughout the process -- from `/packages/b/node_modules/json5` to `/packages/b/node_modules` to finally `/packages/b/node_modules/css-loader`, for example.
- Cannot reproduce when major versions of `css-loader` are the same (e.g. both package a and b have `"css-loader": "^1.0.0"` specified.)
- Cannot reproduce when package a does not reference package b in `dependencies`/`devDependencies`.
- Cannot reproduce with `"nohoist": ["css-*"]` or `"nohoist": ["css-loader"]`.
