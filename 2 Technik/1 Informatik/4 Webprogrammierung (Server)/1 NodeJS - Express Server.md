```
Start npm project
> npm init -y
Install dependencies
> npm i express
> npm i body-parser
```

```js
const express = require('express');
const bodyParser = require('body-parser');

const app = express();

app.get('/', (req, res) => {
	res.end('Hello World');
});

app.listen(80, ()=> {
	console.log('Server started on port 80');
});
```