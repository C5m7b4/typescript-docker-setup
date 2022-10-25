# typescript and docker template

first we need to initialize a package

```js
npm init -y
```

then we need to install typescript

```js
npm install --save-dev typescript
```

then we need a typescript config file

```js
npx tsc --init
```

next let's make a few changes to the config file

```js
"target": "esnext", 
"moduleResolution": "node",
"baseUrl": "./src",
```

then we are going to create a gitignore

```js
npx gitignore node
```

now we have to have prettier

```js
npm install --save-dev prettier
```

then create the .prettierrc file and make the contents look like this

```js
{}
```

next up, we definately want eslint working for us so

```js
npm install --save-dev eslint @typescript-eslint/parser @typescript-eslint/eslint-plugin
```

then we need our config file

```js
{
  "root":true,
  "parser":"@typescript-eslint/parser",
  "plugins":[
    "@typescript-eslint"
  ],
  "extends":[
    "eslint:recommended",
    "plugin:@typescript-eslint/eslint-recommended",
    "plugin:@typescript-eslint/recommended"
  ]
}
```

now we will probably want an ignore file so create a .eslintignore file that looks lik this:

```js
node_modules
dist
```

then we are going to add a script to the package.json for linting our files

```js
"lint":"eslint . --ext .ts"
```

now we should have a src folder with an index.ts with these contents

```js
console.log('whats up doc')
```

now if we add some rules, we can test everything out and make sure its working. now our .eslintrc file should look like this:

```js
{
  "root":true,
  "parser":"@typescript-eslint/parser",
  "plugins":[
    "@typescript-eslint"
  ],
  "extends":[
    "eslint:recommended",
    "plugin:@typescript-eslint/eslint-recommended",
    "plugin:@typescript-eslint/recommended"
  ],
  "rules":{
    "no-console": 2
  }
}
```

if linting isn't working for you automatically, you can try ctrl-shift-p and type reload. you can also run npm run lint and you should get an error. Now try changing the rule to a 1 and the file should turn yellow and then change it to a zero and the file should no long have any color indicating an issue with this file.

now we will get a little devlish and disallow for and while loops:

```js
npm install --save-dev eslint-plugin-no-loops
```

now add this rule to your .eslintrc file

```js
"no-loops/no-loops": 2
```

now this file should look like this after we also include the no-loops plugin:

```js
{
  "root":true,
  "parser":"@typescript-eslint/parser",
  "plugins":[
    "@typescript-eslint",
    "no-loops"
  ],
  "extends":[
    "eslint:recommended",
    "plugin:@typescript-eslint/eslint-recommended",
    "plugin:@typescript-eslint/recommended"
  ],
  "rules":{
    "no-console": 0,
    "no-loops/no-loops": 2
  }
}
```

we can also add a prettier script to our package.json file

```js
"prettier-format": "prettier --config .prettierrc 'src/**/*.ts' --write"
```

now to get them both working nicely together

```js
npm install --save-dev eslint-config-prettier eslint-plugin-prettier
```

now our .eslintrc file should look like this:

```js
{
  "root":true,
  "parser":"@typescript-eslint/parser",
  "plugins":[
    "@typescript-eslint",
    "no-loops",
    "prettier"
  ],
  "extends":[
    "eslint:recommended",
    "plugin:@typescript-eslint/eslint-recommended",
    "plugin:@typescript-eslint/recommended",
    "prettier"
  ],
  "rules":{
    "no-console": 0,
    "no-loops/no-loops": 2,
    "prettier/prettier": 2
  }
}
```

and let's add one line to our .prettierrc file

```js
{
  "endOfLine": "auto"
}
```

you may have to reload after this so vscode knows whats up

