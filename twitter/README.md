# Twitter

Key Components:
* Tweets
* Users

Key Features:
* Tweet Threads
* Tweet Feed
* User Profile View
* Search

Required Constraints:
* Quick tweet retrieval
* User Exploration (Profile Views and other things included)

## Schema

- Tweet
```clojure
type Tweet {
    id: ID!
    tweet: String!
    parent: ID!
    children: [ID!]!
    tweetBy: User!
    tweetAt: Int!
    mentionedUsers: [User!]!
    mentionedHastags: [String!]!
}
```

- User
```clojure
type User {
    id: ID!
    email: String!
    handle: String!
    name: String!
    createdAt: Int!
    tweetFeed(paginatedInput: { pageNo: Int!, pageSize: Int! }): [Tweet!]!
}
```

- Queries
```clojure
type Query {
    findUser(filter: { search: String! }, paginatedInput: { pageNo: Int!, pageSize: Int! }): [User!]! @authenticated
    findTweet(filter: { search: String! }, paginatedInput: { pageNo: Int!, pageSize: Int! }): [Tweet!]! @authenticated
    getTweet(id: ID!): Tweet!
    getUser(id: ID!): User!
}
```

- Mutations
```clojure
type Mutations {
    signup(userInput: { name: String!, email: String!, handle: String!, password: String! }): User!
    login(credentials: { username: String!, password: String! }): User!
}
```
