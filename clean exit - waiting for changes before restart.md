**Clean exit - waiting for changes before restart but nodemon wouldn't restart**

Nodemon wouldn't just restart on changes. Most article demonstrated nodemon with a server. However, it could be used with normal node script.

The problem here was two folds

1. WSL and nodemon do not seem to work together as nodemon could not detect changes.

solution: use native windows terminal- powershell or bash

2. The watch property in nodemon.json was overriding the terminal file to watch.

```
//A. nodemon.json
{
  "watch": ["src/index.ts"],
}

//B. terminal command... here the file to watch was directly indicate
nodemon --watch express.ts

And because this not indicated in nodemon.json, nodemon failed to watch the file and used the preference the watch preference in nodemon.json instead of //B which was implicitly stated. 
```


solution: add the appropriate file to watch

3. Powershell does not also recognize nodemon global so this have to installed locally and ran via npm run ....

solution: install nodemon locally and run it via npm. e.g npm run dev. where dev is -> nodemon index.ts
