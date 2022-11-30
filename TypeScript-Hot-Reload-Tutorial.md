![](https://i.imgur.com/NmcFUxq.png)

# Typescript Hot Reloading
## Quick Set Up
1. You'll want to tsc transpiler downloaded globaly. 
`npm install -g typescript`

create a new typescript workspace folder. This is where all of your TS files will live.

make a new directory in your TS workspace and open VSCode  (`code .`)

2. run `git init` and `npm init`

3. run `npm install`

4. run `npm install --save-dev lite-server`


5.  run `npm start`

#### edit the following in  `package.json`

 > inside of "scripts" shell, add `{"start": "lite-server",  ...}`
-- set your path: `"main": app.js`
 - Inside index.html, add this line.
`<script src="app.js" defer></script>`

6. create `app.ts`. write TS code, and compile using the command `$tsc app.ts`



## Hot reload compilation

1. run `$tsc --init` 

2. run `$tsc --watch`

3.  include or exclude files in your newly created `tsconfig` shell.
### example script : tsconfig
 ```
 "exclude" : [
    "types/analytics.ts",
    "node_modules" //would be the default
  ], 
  "include": [
    "types/app.ts" //include - exclude ( default )
  ], 
  "files": [
    "types/basics.ts"
  ]
```
---------------------- 

4. Organize your files; change your `outDir: "dist"` and `rootDir: "src"` in your tsconfig.json file.


