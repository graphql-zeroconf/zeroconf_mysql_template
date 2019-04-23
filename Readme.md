### Zeroconf

The simplest way to start graphql with zero configuration .

Zeroconf supports to generate C.R.U.D API automatically. It has powerful where clauses for query and also has interface which called hook in each C.U.D mutations.

Lets say that we have user table on our mysql database. In this case zeroconf CRUD schema will be generated with its table name.

### Sequelize ORM

The Zeroconf also uses sequelize orm in its core and has operatorAliases for complex where clauses like below. so you can see that query manual for use it.

```
// The default contained operatorsAliases.

const operatorsAliases = {
  $eq: Op.eq,
  $ne: Op.ne,
  $gte: Op.gte,
  $gt: Op.gt,
  $lte: Op.lte,
  $lt: Op.lt,
  $not: Op.not,
  $in: Op.in,
  $notIn: Op.notIn,
  $is: Op.is,
  $like: Op.like,
  $notLike: Op.notLike,
  $iLike: Op.iLike,
  $notILike: Op.notILike,
  $regexp: Op.regexp,
  $notRegexp: Op.notRegexp,
  $iRegexp: Op.iRegexp,
  $notIRegexp: Op.notIRegexp,
  $between: Op.between,
  $notBetween: Op.notBetween,
  $overlap: Op.overlap,
  $contains: Op.contains,
  $contained: Op.contained,
  $adjacent: Op.adjacent,
  $strictLeft: Op.strictLeft,
  $strictRight: Op.strictRight,
  $noExtendRight: Op.noExtendRight,
  $noExtendLeft: Op.noExtendLeft,
  $and: Op.and,
  $or: Op.or,
  $any: Op.any,
  $all: Op.all,
  $values: Op.values,
  $col: Op.col
};
```

As of result, You can query to the graphql server like this.

```
query {
  users(
    where: {
      or: [{ user_id: 1, user_id: 2 }]
    }
  ) {
    user_id
    email
  }
}
```

### Support Generating C.R.U.D API

#### Object generation support:

- The zeroconf will generates object types and mutations, queries over the your table name.

  If you have a table which called **user_lesson**, zeroconf will generate these things.

  - type **UserLesson**
  - query { **userLesson**, **userLessons**, **numUserLesson** }
  - mutation { **createUserLesson**, **updateUserLessons**, **deleteUserLesson** }

#### Query generation support:

- generated singluar name Query field for fetching one row

  **user**(**where**: UserWhereInput!): User

- generated plural name Query field for fetching all row on some query condition:

  **users**(**limit**: Int, **start**: Int, **where**: JSON, **order**: UserOrderInput)

#### Mutation generation support:

- Creation

  **_createUser_**(input: UserCreationInput!): User

- Update:

  **_updateUser_**(where: UserWhereInput!, input: UserUpdateInput!): User

- Delete:

  **_deleteUser_**(input: UserCreationInput!): User

#### Child Relations

If table has the column id and it has foreign key which refers to the other tables.
zeroconf generates sub-fields for graph query.

```
# the lesson table
lesson
| lesson_id

# the user table
user
| user_id
| lesson_id -> foreign key refers to lesson table

# will be generated.
type User {
  user_id
  -> lesson # generated by checking foreign key
  -> lessons # generated by checking foreign key
}
```

### Installation

```
git clone https://github.com/jeongjuwon/zeroconf_template.git
npm install
```

Create your .env file

```
.env

MYSQL_HOST=localhost
MYSQL_PORT=3306
MYSQL_DATABASE=db
MYSQL_USER=user
MYSQL_PASSWORD=pwd
```

Generate models

```
$ node scripts/gen_model
```

Just Start

```
$ npm start
```
