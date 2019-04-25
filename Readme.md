# Get Started

### Clone the repository

```
git clone https://github.com/graphql-zeroconf/zeroconf_mysql_template.git
```

### Install the packages

```
cd zeroconf_mysql_template
npm install
```

### Create your .env file on your project root

```
cat <<EOF >.env
MYSQL_HOST=
MYSQL_PORT=3306
MYSQL_DATABASE=
MYSQL_USER=
MYSQL_PASSWORD=
GRAPHQL_HOST=localhost
GRAPHQL_PORT=4000
EOF
```

### Start with graphql

```
$ npm start
```

or

```
$ npm run graphql
```

### Start with apollo

```
$ npm run apollo
```