__Clean exit - waiting for changes before restart but nodemon wouldn't restart__

Nodemon wouldn't just restart on changes. Most article demonstrated nodemon with a server. However, it could be used with normal node script. 

The problem here was two folds
1. WSL and nodemon do not seem to work together as nodemon could not detect changes.

solution: use poweshell

2. The watch property in nodemon.json was overriding the terminal file to watch.

solution: add the appropriate file to watch

3. Powershell does not also recognize nodemon global so this have to installed locally and ran via npm run .... 

solution: install nodemon locally and run it via npm. e.g npm run dev. where dev is -> nodemon index.ts 