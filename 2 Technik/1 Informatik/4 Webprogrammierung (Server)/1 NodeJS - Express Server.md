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

Express Middleware
```js
	req.session.username = req.body.username
	
	func test(req,res,done){
		if(X)
			done
		else
			redirect
```

SQL Query
```js
	mysql = mysql2
	util
	
	connection = mysql.createConnection({
		User: "root",
		Password: "root",
		Host: "localhost"
		Database: "test",
	})
	
	query = util.promisify(connection.query).bind(connection);
```
