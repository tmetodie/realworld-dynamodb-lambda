```
DELETE /__TESTUTILS__/purge
```
```
200 OK

"Purged all data!"
```
# Article
```
POST /users

{
  "user": {
    "email": "author-dh163w@email.com",
    "username": "author-dh163w",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "author-dh163w@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6ImF1dGhvci1kaDE2M3ciLCJpYXQiOjE2MDMzMjc5NjIsImV4cCI6MTYwMzUwMDc2Mn0.oDvXBmfZ5aOLWPHOPiqZ1OZBgFbUrkt99TWAHBaGRQg",
    "username": "author-dh163w",
    "bio": "",
    "image": ""
  }
}
```
```
POST /users

{
  "user": {
    "email": "authoress-ampas3@email.com",
    "username": "authoress-ampas3",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "authoress-ampas3@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6ImF1dGhvcmVzcy1hbXBhczMiLCJpYXQiOjE2MDMzMjc5NjIsImV4cCI6MTYwMzUwMDc2Mn0.1FD79QSUJz_2IRH0GKcD8pByEdMnu2eIztvG1NeiRIM",
    "username": "authoress-ampas3",
    "bio": "",
    "image": ""
  }
}
```
```
POST /users

{
  "user": {
    "email": "non-author-bn1we9@email.com",
    "username": "non-author-bn1we9",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "non-author-bn1we9@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6Im5vbi1hdXRob3ItYm4xd2U5IiwiaWF0IjoxNjAzMzI3OTYyLCJleHAiOjE2MDM1MDA3NjJ9.FQy5rjTjbgNzkQraNINbtqnum6ZiFjzikWhxJz97p8g",
    "username": "non-author-bn1we9",
    "bio": "",
    "image": ""
  }
}
```
## Create
### should create article
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body"
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-72y758",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1603327962373,
    "updatedAt": 1603327962373,
    "author": {
      "username": "author-dh163w",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
### should create article with tags
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "tag_a",
      "tag_b"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-il6oic",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1603327962432,
    "updatedAt": 1603327962432,
    "author": {
      "username": "author-dh163w",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "tag_a",
      "tag_b"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
### should disallow unauthenticated user
```
POST /articles

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Must be logged in."
    ]
  }
}
```
### should enforce required fields
```
POST /articles

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article must be specified."
    ]
  }
}
```
```
POST /articles

{
  "article": {}
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "title must be specified."
    ]
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "description must be specified."
    ]
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "body must be specified."
    ]
  }
}
```
## Get
### should get article by slug
```
GET /articles/title-72y758
```
```
200 OK

{
  "article": {
    "createdAt": 1603327962373,
    "author": {
      "username": "author-dh163w",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "description",
    "title": "title",
    "body": "body",
    "slug": "title-72y758",
    "updatedAt": 1603327962373,
    "tagList": [],
    "favoritesCount": 0,
    "favorited": false
  }
}
```
### should get article with tags by slug
```
GET /articles/title-il6oic
```
```
200 OK

{
  "article": {
    "tagList": [
      "tag_a",
      "tag_b"
    ],
    "createdAt": 1603327962432,
    "author": {
      "username": "author-dh163w",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "description",
    "title": "title",
    "body": "body",
    "slug": "title-il6oic",
    "updatedAt": 1603327962432,
    "favoritesCount": 0,
    "favorited": false
  }
}
```
### should disallow unknown slug
```
GET /articles/bqwqbr
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article not found: [bqwqbr]"
    ]
  }
}
```
## Update
### should update article
```
PUT /articles/title-il6oic

{
  "article": {
    "title": "newtitle"
  }
}
```
```
200 OK

{
  "article": {
    "tagList": [
      "tag_a",
      "tag_b"
    ],
    "createdAt": 1603327962432,
    "author": {
      "username": "author-dh163w",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "description",
    "title": "newtitle",
    "body": "body",
    "slug": "title-il6oic",
    "updatedAt": 1603327962432,
    "favoritesCount": 0,
    "favorited": false
  }
}
```
```
PUT /articles/title-il6oic

{
  "article": {
    "description": "newdescription"
  }
}
```
```
200 OK

{
  "article": {
    "tagList": [
      "tag_a",
      "tag_b"
    ],
    "createdAt": 1603327962432,
    "author": {
      "username": "author-dh163w",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "newdescription",
    "title": "newtitle",
    "body": "body",
    "slug": "title-il6oic",
    "updatedAt": 1603327962432,
    "favoritesCount": 0,
    "favorited": false
  }
}
```
```
PUT /articles/title-il6oic

{
  "article": {
    "body": "newbody"
  }
}
```
```
200 OK

{
  "article": {
    "tagList": [
      "tag_a",
      "tag_b"
    ],
    "createdAt": 1603327962432,
    "author": {
      "username": "author-dh163w",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "newdescription",
    "title": "newtitle",
    "body": "newbody",
    "slug": "title-il6oic",
    "updatedAt": 1603327962432,
    "favoritesCount": 0,
    "favorited": false
  }
}
```
### should disallow missing mutation
```
PUT /articles/title-il6oic

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article mutation must be specified."
    ]
  }
}
```
### should disallow empty mutation
```
PUT /articles/title-il6oic

{
  "article": {}
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "At least one field must be specified: [title, description, article]."
    ]
  }
}
```
### should disallow unauthenticated update
```
PUT /articles/title-il6oic

{
  "article": {
    "title": "newtitle"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Must be logged in."
    ]
  }
}
```
### should disallow updating non-existent article
```
PUT /articles/foo-title-il6oic

{
  "article": {
    "title": "newtitle"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article not found: [foo-title-il6oic]"
    ]
  }
}
```
### should disallow non-author from updating
```
PUT /articles/title-il6oic

{
  "article": {
    "title": "newtitle"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article can only be updated by author: [author-dh163w]"
    ]
  }
}
```
## Favorite
### should favorite article
```
POST /articles/title-72y758/favorite

{}
```
```
200 OK

{
  "article": {
    "createdAt": 1603327962373,
    "author": {
      "username": "author-dh163w",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "description",
    "title": "title",
    "body": "body",
    "slug": "title-72y758",
    "updatedAt": 1603327962373,
    "favoritedBy": [
      "non-author-bn1we9"
    ],
    "favoritesCount": 1,
    "tagList": [],
    "favorited": true
  }
}
```
```
GET /articles/title-72y758
```
```
200 OK

{
  "article": {
    "createdAt": 1603327962373,
    "author": {
      "username": "author-dh163w",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "description",
    "title": "title",
    "body": "body",
    "favoritesCount": 1,
    "slug": "title-72y758",
    "updatedAt": 1603327962373,
    "tagList": [],
    "favorited": true
  }
}
```
### should disallow favoriting by unauthenticated user
```
POST /articles/title-72y758/favorite

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Must be logged in."
    ]
  }
}
```
### should disallow favoriting unknown article
```
POST /articles/title-72y758_foo/favorite

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article not found: [title-72y758_foo]"
    ]
  }
}
```
### should unfavorite article
```
DELETE /articles/title-72y758/favorite
```
```
200 OK

{
  "article": {
    "createdAt": 1603327962373,
    "author": {
      "username": "author-dh163w",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "description",
    "title": "title",
    "body": "body",
    "favoritesCount": 0,
    "slug": "title-72y758",
    "updatedAt": 1603327962373,
    "tagList": [],
    "favorited": false
  }
}
```
## Delete
### should delete article
```
DELETE /articles/title-72y758
```
```
200 OK

{}
```
```
GET /articles/title-72y758
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article not found: [title-72y758]"
    ]
  }
}
```
### should disallow deleting by unauthenticated user
```
DELETE /articles/foo
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Must be logged in."
    ]
  }
}
```
### should disallow deleting unknown article
```
DELETE /articles/foobar
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article not found: [foobar]"
    ]
  }
}
```
### should disallow deleting article by non-author
```
DELETE /articles/title-il6oic
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article can only be deleted by author: [author-dh163w]"
    ]
  }
}
```
## List
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "ow7zto",
      "tag_0",
      "tag_mod_2_0",
      "tag_mod_3_0"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-gz1cgd",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1603327963446,
    "updatedAt": 1603327963446,
    "author": {
      "username": "authoress-ampas3",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "ow7zto",
      "tag_0",
      "tag_mod_2_0",
      "tag_mod_3_0"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "90y5rm",
      "tag_1",
      "tag_mod_2_1",
      "tag_mod_3_1"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-rx9ax6",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1603327963471,
    "updatedAt": 1603327963471,
    "author": {
      "username": "author-dh163w",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "90y5rm",
      "tag_1",
      "tag_mod_2_1",
      "tag_mod_3_1"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "lv8gen",
      "tag_2",
      "tag_mod_2_0",
      "tag_mod_3_2"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-t2wr94",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1603327963509,
    "updatedAt": 1603327963509,
    "author": {
      "username": "authoress-ampas3",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "lv8gen",
      "tag_2",
      "tag_mod_2_0",
      "tag_mod_3_2"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "3vyebr",
      "tag_3",
      "tag_mod_2_1",
      "tag_mod_3_0"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-lub3nd",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1603327963535,
    "updatedAt": 1603327963535,
    "author": {
      "username": "author-dh163w",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "3vyebr",
      "tag_3",
      "tag_mod_2_1",
      "tag_mod_3_0"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "mc0ron",
      "tag_4",
      "tag_mod_2_0",
      "tag_mod_3_1"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-m6fzur",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1603327963575,
    "updatedAt": 1603327963575,
    "author": {
      "username": "authoress-ampas3",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "mc0ron",
      "tag_4",
      "tag_mod_2_0",
      "tag_mod_3_1"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "vfkq4l",
      "tag_5",
      "tag_mod_2_1",
      "tag_mod_3_2"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-6uyd91",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1603327963621,
    "updatedAt": 1603327963621,
    "author": {
      "username": "author-dh163w",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "vfkq4l",
      "tag_5",
      "tag_mod_2_1",
      "tag_mod_3_2"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "11gc7a",
      "tag_6",
      "tag_mod_2_0",
      "tag_mod_3_0"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-2rmbqn",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1603327963667,
    "updatedAt": 1603327963667,
    "author": {
      "username": "authoress-ampas3",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "11gc7a",
      "tag_6",
      "tag_mod_2_0",
      "tag_mod_3_0"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "33ld2w",
      "tag_7",
      "tag_mod_2_1",
      "tag_mod_3_1"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-15uyd7",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1603327963723,
    "updatedAt": 1603327963723,
    "author": {
      "username": "author-dh163w",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "33ld2w",
      "tag_7",
      "tag_mod_2_1",
      "tag_mod_3_1"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "poru3j",
      "tag_8",
      "tag_mod_2_0",
      "tag_mod_3_2"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-hi6h76",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1603327963770,
    "updatedAt": 1603327963770,
    "author": {
      "username": "authoress-ampas3",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "poru3j",
      "tag_8",
      "tag_mod_2_0",
      "tag_mod_3_2"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "wsq3cu",
      "tag_9",
      "tag_mod_2_1",
      "tag_mod_3_0"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-lvrnin",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1603327963803,
    "updatedAt": 1603327963803,
    "author": {
      "username": "author-dh163w",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "wsq3cu",
      "tag_9",
      "tag_mod_2_1",
      "tag_mod_3_0"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "im1369",
      "tag_10",
      "tag_mod_2_0",
      "tag_mod_3_1"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-ftm7qj",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1603327963839,
    "updatedAt": 1603327963839,
    "author": {
      "username": "authoress-ampas3",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "im1369",
      "tag_10",
      "tag_mod_2_0",
      "tag_mod_3_1"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "j2fpyt",
      "tag_11",
      "tag_mod_2_1",
      "tag_mod_3_2"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-sg8jm9",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1603327963865,
    "updatedAt": 1603327963865,
    "author": {
      "username": "author-dh163w",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "j2fpyt",
      "tag_11",
      "tag_mod_2_1",
      "tag_mod_3_2"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "3ltll2",
      "tag_12",
      "tag_mod_2_0",
      "tag_mod_3_0"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-cvg84b",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1603327963890,
    "updatedAt": 1603327963890,
    "author": {
      "username": "authoress-ampas3",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "3ltll2",
      "tag_12",
      "tag_mod_2_0",
      "tag_mod_3_0"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "mz6frb",
      "tag_13",
      "tag_mod_2_1",
      "tag_mod_3_1"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-jyh906",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1603327963919,
    "updatedAt": 1603327963919,
    "author": {
      "username": "author-dh163w",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "mz6frb",
      "tag_13",
      "tag_mod_2_1",
      "tag_mod_3_1"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "9j01da",
      "tag_14",
      "tag_mod_2_0",
      "tag_mod_3_2"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-9wau76",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1603327963944,
    "updatedAt": 1603327963944,
    "author": {
      "username": "authoress-ampas3",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "9j01da",
      "tag_14",
      "tag_mod_2_0",
      "tag_mod_3_2"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "15tkih",
      "tag_15",
      "tag_mod_2_1",
      "tag_mod_3_0"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-yc56tb",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1603327963968,
    "updatedAt": 1603327963968,
    "author": {
      "username": "author-dh163w",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "15tkih",
      "tag_15",
      "tag_mod_2_1",
      "tag_mod_3_0"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "s8i3r4",
      "tag_16",
      "tag_mod_2_0",
      "tag_mod_3_1"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-vb32az",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1603327963995,
    "updatedAt": 1603327963995,
    "author": {
      "username": "authoress-ampas3",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "s8i3r4",
      "tag_16",
      "tag_mod_2_0",
      "tag_mod_3_1"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "hu5y7x",
      "tag_17",
      "tag_mod_2_1",
      "tag_mod_3_2"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-v1j78m",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1603327964023,
    "updatedAt": 1603327964023,
    "author": {
      "username": "author-dh163w",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "hu5y7x",
      "tag_17",
      "tag_mod_2_1",
      "tag_mod_3_2"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "7p4ozm",
      "tag_18",
      "tag_mod_2_0",
      "tag_mod_3_0"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-voianx",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1603327964048,
    "updatedAt": 1603327964048,
    "author": {
      "username": "authoress-ampas3",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "7p4ozm",
      "tag_18",
      "tag_mod_2_0",
      "tag_mod_3_0"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "lehgsw",
      "tag_19",
      "tag_mod_2_1",
      "tag_mod_3_1"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-f1vhfw",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1603327964083,
    "updatedAt": 1603327964083,
    "author": {
      "username": "author-dh163w",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "lehgsw",
      "tag_19",
      "tag_mod_2_1",
      "tag_mod_3_1"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
### should list articles
```
GET /articles
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "lehgsw",
        "tag_19",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1603327964083,
      "author": {
        "username": "author-dh163w",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-f1vhfw",
      "updatedAt": 1603327964083,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "7p4ozm",
        "tag_18",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1603327964048,
      "author": {
        "username": "authoress-ampas3",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-voianx",
      "updatedAt": 1603327964048,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "hu5y7x",
        "tag_17",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1603327964023,
      "author": {
        "username": "author-dh163w",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-v1j78m",
      "updatedAt": 1603327964023,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "s8i3r4",
        "tag_16",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1603327963995,
      "author": {
        "username": "authoress-ampas3",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-vb32az",
      "updatedAt": 1603327963995,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "15tkih",
        "tag_15",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1603327963968,
      "author": {
        "username": "author-dh163w",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-yc56tb",
      "updatedAt": 1603327963968,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "9j01da",
        "tag_14",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1603327963944,
      "author": {
        "username": "authoress-ampas3",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-9wau76",
      "updatedAt": 1603327963944,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "mz6frb",
        "tag_13",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1603327963919,
      "author": {
        "username": "author-dh163w",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-jyh906",
      "updatedAt": 1603327963919,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "3ltll2",
        "tag_12",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1603327963890,
      "author": {
        "username": "authoress-ampas3",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-cvg84b",
      "updatedAt": 1603327963890,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "j2fpyt",
        "tag_11",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1603327963865,
      "author": {
        "username": "author-dh163w",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-sg8jm9",
      "updatedAt": 1603327963865,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "im1369",
        "tag_10",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1603327963839,
      "author": {
        "username": "authoress-ampas3",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-ftm7qj",
      "updatedAt": 1603327963839,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_9",
        "tag_mod_2_1",
        "tag_mod_3_0",
        "wsq3cu"
      ],
      "createdAt": 1603327963803,
      "author": {
        "username": "author-dh163w",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-lvrnin",
      "updatedAt": 1603327963803,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "poru3j",
        "tag_8",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1603327963770,
      "author": {
        "username": "authoress-ampas3",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-hi6h76",
      "updatedAt": 1603327963770,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "33ld2w",
        "tag_7",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1603327963723,
      "author": {
        "username": "author-dh163w",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-15uyd7",
      "updatedAt": 1603327963723,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "11gc7a",
        "tag_6",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1603327963667,
      "author": {
        "username": "authoress-ampas3",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-2rmbqn",
      "updatedAt": 1603327963667,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_5",
        "tag_mod_2_1",
        "tag_mod_3_2",
        "vfkq4l"
      ],
      "createdAt": 1603327963621,
      "author": {
        "username": "author-dh163w",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-6uyd91",
      "updatedAt": 1603327963621,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "mc0ron",
        "tag_4",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1603327963575,
      "author": {
        "username": "authoress-ampas3",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-m6fzur",
      "updatedAt": 1603327963575,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "3vyebr",
        "tag_3",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1603327963535,
      "author": {
        "username": "author-dh163w",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-lub3nd",
      "updatedAt": 1603327963535,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "lv8gen",
        "tag_2",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1603327963509,
      "author": {
        "username": "authoress-ampas3",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-t2wr94",
      "updatedAt": 1603327963509,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "90y5rm",
        "tag_1",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1603327963471,
      "author": {
        "username": "author-dh163w",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-rx9ax6",
      "updatedAt": 1603327963471,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "ow7zto",
        "tag_0",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1603327963446,
      "author": {
        "username": "authoress-ampas3",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-gz1cgd",
      "updatedAt": 1603327963446,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
### should list articles with tag
```
GET /articles?tag=tag_7
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "33ld2w",
        "tag_7",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1603327963723,
      "author": {
        "username": "author-dh163w",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-15uyd7",
      "updatedAt": 1603327963723,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
```
GET /articles?tag=tag_mod_3_2
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "hu5y7x",
        "tag_17",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1603327964023,
      "author": {
        "username": "author-dh163w",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-v1j78m",
      "updatedAt": 1603327964023,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "9j01da",
        "tag_14",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1603327963944,
      "author": {
        "username": "authoress-ampas3",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-9wau76",
      "updatedAt": 1603327963944,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "j2fpyt",
        "tag_11",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1603327963865,
      "author": {
        "username": "author-dh163w",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-sg8jm9",
      "updatedAt": 1603327963865,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "poru3j",
        "tag_8",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1603327963770,
      "author": {
        "username": "authoress-ampas3",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-hi6h76",
      "updatedAt": 1603327963770,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_5",
        "tag_mod_2_1",
        "tag_mod_3_2",
        "vfkq4l"
      ],
      "createdAt": 1603327963621,
      "author": {
        "username": "author-dh163w",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-6uyd91",
      "updatedAt": 1603327963621,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "lv8gen",
        "tag_2",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1603327963509,
      "author": {
        "username": "authoress-ampas3",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-t2wr94",
      "updatedAt": 1603327963509,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
### should list articles by author
```
GET /articles?author=authoress-ampas3
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "7p4ozm",
        "tag_18",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1603327964048,
      "author": {
        "username": "authoress-ampas3",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-voianx",
      "updatedAt": 1603327964048,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "s8i3r4",
        "tag_16",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1603327963995,
      "author": {
        "username": "authoress-ampas3",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-vb32az",
      "updatedAt": 1603327963995,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "9j01da",
        "tag_14",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1603327963944,
      "author": {
        "username": "authoress-ampas3",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-9wau76",
      "updatedAt": 1603327963944,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "3ltll2",
        "tag_12",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1603327963890,
      "author": {
        "username": "authoress-ampas3",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-cvg84b",
      "updatedAt": 1603327963890,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "im1369",
        "tag_10",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1603327963839,
      "author": {
        "username": "authoress-ampas3",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-ftm7qj",
      "updatedAt": 1603327963839,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "poru3j",
        "tag_8",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1603327963770,
      "author": {
        "username": "authoress-ampas3",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-hi6h76",
      "updatedAt": 1603327963770,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "11gc7a",
        "tag_6",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1603327963667,
      "author": {
        "username": "authoress-ampas3",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-2rmbqn",
      "updatedAt": 1603327963667,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "mc0ron",
        "tag_4",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1603327963575,
      "author": {
        "username": "authoress-ampas3",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-m6fzur",
      "updatedAt": 1603327963575,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "lv8gen",
        "tag_2",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1603327963509,
      "author": {
        "username": "authoress-ampas3",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-t2wr94",
      "updatedAt": 1603327963509,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "ow7zto",
        "tag_0",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1603327963446,
      "author": {
        "username": "authoress-ampas3",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-gz1cgd",
      "updatedAt": 1603327963446,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
### should list articles favorited by user
```
GET /articles?favorited=non-author-bn1we9
```
```
200 OK

{
  "articles": []
}
```
### should list articles by limit/offset
```
GET /articles?author=author-dh163w&limit=2
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "lehgsw",
        "tag_19",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1603327964083,
      "author": {
        "username": "author-dh163w",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-f1vhfw",
      "updatedAt": 1603327964083,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "hu5y7x",
        "tag_17",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1603327964023,
      "author": {
        "username": "author-dh163w",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-v1j78m",
      "updatedAt": 1603327964023,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
```
GET /articles?author=author-dh163w&limit=2&offset=2
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "15tkih",
        "tag_15",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1603327963968,
      "author": {
        "username": "author-dh163w",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-yc56tb",
      "updatedAt": 1603327963968,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "mz6frb",
        "tag_13",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1603327963919,
      "author": {
        "username": "author-dh163w",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-jyh906",
      "updatedAt": 1603327963919,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
### should list articles when authenticated
```
GET /articles
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "lehgsw",
        "tag_19",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1603327964083,
      "author": {
        "username": "author-dh163w",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-f1vhfw",
      "updatedAt": 1603327964083,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "7p4ozm",
        "tag_18",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1603327964048,
      "author": {
        "username": "authoress-ampas3",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-voianx",
      "updatedAt": 1603327964048,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "hu5y7x",
        "tag_17",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1603327964023,
      "author": {
        "username": "author-dh163w",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-v1j78m",
      "updatedAt": 1603327964023,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "s8i3r4",
        "tag_16",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1603327963995,
      "author": {
        "username": "authoress-ampas3",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-vb32az",
      "updatedAt": 1603327963995,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "15tkih",
        "tag_15",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1603327963968,
      "author": {
        "username": "author-dh163w",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-yc56tb",
      "updatedAt": 1603327963968,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "9j01da",
        "tag_14",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1603327963944,
      "author": {
        "username": "authoress-ampas3",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-9wau76",
      "updatedAt": 1603327963944,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "mz6frb",
        "tag_13",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1603327963919,
      "author": {
        "username": "author-dh163w",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-jyh906",
      "updatedAt": 1603327963919,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "3ltll2",
        "tag_12",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1603327963890,
      "author": {
        "username": "authoress-ampas3",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-cvg84b",
      "updatedAt": 1603327963890,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "j2fpyt",
        "tag_11",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1603327963865,
      "author": {
        "username": "author-dh163w",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-sg8jm9",
      "updatedAt": 1603327963865,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "im1369",
        "tag_10",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1603327963839,
      "author": {
        "username": "authoress-ampas3",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-ftm7qj",
      "updatedAt": 1603327963839,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_9",
        "tag_mod_2_1",
        "tag_mod_3_0",
        "wsq3cu"
      ],
      "createdAt": 1603327963803,
      "author": {
        "username": "author-dh163w",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-lvrnin",
      "updatedAt": 1603327963803,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "poru3j",
        "tag_8",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1603327963770,
      "author": {
        "username": "authoress-ampas3",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-hi6h76",
      "updatedAt": 1603327963770,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "33ld2w",
        "tag_7",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1603327963723,
      "author": {
        "username": "author-dh163w",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-15uyd7",
      "updatedAt": 1603327963723,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "11gc7a",
        "tag_6",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1603327963667,
      "author": {
        "username": "authoress-ampas3",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-2rmbqn",
      "updatedAt": 1603327963667,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_5",
        "tag_mod_2_1",
        "tag_mod_3_2",
        "vfkq4l"
      ],
      "createdAt": 1603327963621,
      "author": {
        "username": "author-dh163w",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-6uyd91",
      "updatedAt": 1603327963621,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "mc0ron",
        "tag_4",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1603327963575,
      "author": {
        "username": "authoress-ampas3",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-m6fzur",
      "updatedAt": 1603327963575,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "3vyebr",
        "tag_3",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1603327963535,
      "author": {
        "username": "author-dh163w",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-lub3nd",
      "updatedAt": 1603327963535,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "lv8gen",
        "tag_2",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1603327963509,
      "author": {
        "username": "authoress-ampas3",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-t2wr94",
      "updatedAt": 1603327963509,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "90y5rm",
        "tag_1",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1603327963471,
      "author": {
        "username": "author-dh163w",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-rx9ax6",
      "updatedAt": 1603327963471,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "ow7zto",
        "tag_0",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1603327963446,
      "author": {
        "username": "authoress-ampas3",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-gz1cgd",
      "updatedAt": 1603327963446,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
### should disallow multiple of author/tag/favorited
```
GET /articles?tag=foo&author=bar
```
```
GET /articles?author=foo&favorited=bar
```
```
GET /articles?favorited=foo&tag=bar
```
## Feed
### should get feed
```
GET /articles/feed
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Only one of these can be specified: [tag, author, favorited]"
    ]
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Only one of these can be specified: [tag, author, favorited]"
    ]
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Only one of these can be specified: [tag, author, favorited]"
    ]
  }
}
```
```
200 OK

{
  "articles": []
}
```
```
POST /profiles/authoress-ampas3/follow

{}
```
```
200 OK

{
  "profile": {
    "username": "authoress-ampas3",
    "bio": "",
    "image": "",
    "following": true
  }
}
```
```
GET /articles/feed
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "7p4ozm",
        "tag_18",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1603327964048,
      "author": {
        "username": "authoress-ampas3",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-voianx",
      "updatedAt": 1603327964048,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "s8i3r4",
        "tag_16",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1603327963995,
      "author": {
        "username": "authoress-ampas3",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-vb32az",
      "updatedAt": 1603327963995,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "9j01da",
        "tag_14",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1603327963944,
      "author": {
        "username": "authoress-ampas3",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-9wau76",
      "updatedAt": 1603327963944,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "3ltll2",
        "tag_12",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1603327963890,
      "author": {
        "username": "authoress-ampas3",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-cvg84b",
      "updatedAt": 1603327963890,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "im1369",
        "tag_10",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1603327963839,
      "author": {
        "username": "authoress-ampas3",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-ftm7qj",
      "updatedAt": 1603327963839,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "poru3j",
        "tag_8",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1603327963770,
      "author": {
        "username": "authoress-ampas3",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-hi6h76",
      "updatedAt": 1603327963770,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "11gc7a",
        "tag_6",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1603327963667,
      "author": {
        "username": "authoress-ampas3",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-2rmbqn",
      "updatedAt": 1603327963667,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "mc0ron",
        "tag_4",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1603327963575,
      "author": {
        "username": "authoress-ampas3",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-m6fzur",
      "updatedAt": 1603327963575,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "lv8gen",
        "tag_2",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1603327963509,
      "author": {
        "username": "authoress-ampas3",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-t2wr94",
      "updatedAt": 1603327963509,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "ow7zto",
        "tag_0",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1603327963446,
      "author": {
        "username": "authoress-ampas3",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-gz1cgd",
      "updatedAt": 1603327963446,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
```
POST /profiles/author-dh163w/follow

{}
```
```
200 OK

{
  "profile": {
    "username": "author-dh163w",
    "bio": "",
    "image": "",
    "following": true
  }
}
```
```
GET /articles/feed
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "lehgsw",
        "tag_19",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1603327964083,
      "author": {
        "username": "author-dh163w",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-f1vhfw",
      "updatedAt": 1603327964083,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "7p4ozm",
        "tag_18",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1603327964048,
      "author": {
        "username": "authoress-ampas3",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-voianx",
      "updatedAt": 1603327964048,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "hu5y7x",
        "tag_17",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1603327964023,
      "author": {
        "username": "author-dh163w",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-v1j78m",
      "updatedAt": 1603327964023,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "s8i3r4",
        "tag_16",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1603327963995,
      "author": {
        "username": "authoress-ampas3",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-vb32az",
      "updatedAt": 1603327963995,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "15tkih",
        "tag_15",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1603327963968,
      "author": {
        "username": "author-dh163w",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-yc56tb",
      "updatedAt": 1603327963968,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "9j01da",
        "tag_14",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1603327963944,
      "author": {
        "username": "authoress-ampas3",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-9wau76",
      "updatedAt": 1603327963944,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "mz6frb",
        "tag_13",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1603327963919,
      "author": {
        "username": "author-dh163w",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-jyh906",
      "updatedAt": 1603327963919,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "3ltll2",
        "tag_12",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1603327963890,
      "author": {
        "username": "authoress-ampas3",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-cvg84b",
      "updatedAt": 1603327963890,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "j2fpyt",
        "tag_11",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1603327963865,
      "author": {
        "username": "author-dh163w",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-sg8jm9",
      "updatedAt": 1603327963865,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "im1369",
        "tag_10",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1603327963839,
      "author": {
        "username": "authoress-ampas3",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-ftm7qj",
      "updatedAt": 1603327963839,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_9",
        "tag_mod_2_1",
        "tag_mod_3_0",
        "wsq3cu"
      ],
      "createdAt": 1603327963803,
      "author": {
        "username": "author-dh163w",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-lvrnin",
      "updatedAt": 1603327963803,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "poru3j",
        "tag_8",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1603327963770,
      "author": {
        "username": "authoress-ampas3",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-hi6h76",
      "updatedAt": 1603327963770,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "33ld2w",
        "tag_7",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1603327963723,
      "author": {
        "username": "author-dh163w",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-15uyd7",
      "updatedAt": 1603327963723,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "11gc7a",
        "tag_6",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1603327963667,
      "author": {
        "username": "authoress-ampas3",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-2rmbqn",
      "updatedAt": 1603327963667,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_5",
        "tag_mod_2_1",
        "tag_mod_3_2",
        "vfkq4l"
      ],
      "createdAt": 1603327963621,
      "author": {
        "username": "author-dh163w",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-6uyd91",
      "updatedAt": 1603327963621,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "mc0ron",
        "tag_4",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1603327963575,
      "author": {
        "username": "authoress-ampas3",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-m6fzur",
      "updatedAt": 1603327963575,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "3vyebr",
        "tag_3",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1603327963535,
      "author": {
        "username": "author-dh163w",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-lub3nd",
      "updatedAt": 1603327963535,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "lv8gen",
        "tag_2",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1603327963509,
      "author": {
        "username": "authoress-ampas3",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-t2wr94",
      "updatedAt": 1603327963509,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "90y5rm",
        "tag_1",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1603327963471,
      "author": {
        "username": "author-dh163w",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-rx9ax6",
      "updatedAt": 1603327963471,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "ow7zto",
        "tag_0",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1603327963446,
      "author": {
        "username": "authoress-ampas3",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-gz1cgd",
      "updatedAt": 1603327963446,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
### should disallow unauthenticated feed
```
GET /articles/feed
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Must be logged in."
    ]
  }
}
```
## Tags
### should get tags
```
GET /tags
```
```
200 OK

{
  "tags": [
    "hu5y7x",
    "tag_17",
    "tag_mod_2_1",
    "tag_mod_3_2",
    "3ltll2",
    "tag_12",
    "tag_mod_2_0",
    "tag_mod_3_0",
    "9j01da",
    "tag_14",
    "90y5rm",
    "tag_1",
    "tag_mod_3_1",
    "s8i3r4",
    "tag_16",
    "lehgsw",
    "tag_19",
    "11gc7a",
    "tag_6",
    "im1369",
    "tag_10",
    "7p4ozm",
    "tag_18",
    "3vyebr",
    "tag_3",
    "lv8gen",
    "tag_2",
    "j2fpyt",
    "tag_11",
    "mc0ron",
    "tag_4",
    "tag_9",
    "wsq3cu",
    "tag_a",
    "tag_b",
    "ow7zto",
    "tag_0",
    "poru3j",
    "tag_8",
    "tag_5",
    "vfkq4l",
    "mz6frb",
    "tag_13",
    "33ld2w",
    "tag_7",
    "15tkih",
    "tag_15"
  ]
}
```
# Comment
```
POST /users

{
  "user": {
    "email": "author-o1atfr@email.com",
    "username": "author-o1atfr",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "author-o1atfr@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6ImF1dGhvci1vMWF0ZnIiLCJpYXQiOjE2MDMzMjc5NjUsImV4cCI6MTYwMzUwMDc2NX0.GIUTG3FqRRr0uaIoG-mnR3yObAvi72EAMGqhlTQU2co",
    "username": "author-o1atfr",
    "bio": "",
    "image": ""
  }
}
```
```
POST /users

{
  "user": {
    "email": "commenter-708a3e@email.com",
    "username": "commenter-708a3e",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "commenter-708a3e@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6ImNvbW1lbnRlci03MDhhM2UiLCJpYXQiOjE2MDMzMjc5NjUsImV4cCI6MTYwMzUwMDc2NX0.7jCvdVOG5H2WAWDtlTv8bx7Uv9cm1PjY-8yAQ_F4vfk",
    "username": "commenter-708a3e",
    "bio": "",
    "image": ""
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body"
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-zg4q0g",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1603327965626,
    "updatedAt": 1603327965626,
    "author": {
      "username": "author-o1atfr",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
## Create
### should create comment
```
POST /articles/title-zg4q0g/comments

{
  "comment": {
    "body": "test comment lgykgl"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "3ff174c7-3daf-49a0-877c-a2e9f6bcd51b",
    "slug": "title-zg4q0g",
    "body": "test comment lgykgl",
    "createdAt": 1603327965657,
    "updatedAt": 1603327965657,
    "author": {
      "username": "commenter-708a3e",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-zg4q0g/comments

{
  "comment": {
    "body": "test comment v9e0wn"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "3002d48d-8412-4940-a0a9-958140747e98",
    "slug": "title-zg4q0g",
    "body": "test comment v9e0wn",
    "createdAt": 1603327965692,
    "updatedAt": 1603327965692,
    "author": {
      "username": "commenter-708a3e",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-zg4q0g/comments

{
  "comment": {
    "body": "test comment yt2566"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "e64cc4c5-0044-4522-8cca-2b0a75d2423b",
    "slug": "title-zg4q0g",
    "body": "test comment yt2566",
    "createdAt": 1603327965725,
    "updatedAt": 1603327965725,
    "author": {
      "username": "commenter-708a3e",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-zg4q0g/comments

{
  "comment": {
    "body": "test comment 2lh0z"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "b78fd819-3504-461a-a18a-7574c280c70d",
    "slug": "title-zg4q0g",
    "body": "test comment 2lh0z",
    "createdAt": 1603327965772,
    "updatedAt": 1603327965772,
    "author": {
      "username": "commenter-708a3e",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-zg4q0g/comments

{
  "comment": {
    "body": "test comment zfq165"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "28d22807-7a21-4b26-8b3d-2741e8978569",
    "slug": "title-zg4q0g",
    "body": "test comment zfq165",
    "createdAt": 1603327965801,
    "updatedAt": 1603327965801,
    "author": {
      "username": "commenter-708a3e",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-zg4q0g/comments

{
  "comment": {
    "body": "test comment w0oj4k"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "ef7af888-cbf9-4752-8172-87f0914cc4f2",
    "slug": "title-zg4q0g",
    "body": "test comment w0oj4k",
    "createdAt": 1603327965827,
    "updatedAt": 1603327965827,
    "author": {
      "username": "commenter-708a3e",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-zg4q0g/comments

{
  "comment": {
    "body": "test comment pwjn95"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "43e9ed60-5bb6-478e-a75e-5c2e3b1eb9ff",
    "slug": "title-zg4q0g",
    "body": "test comment pwjn95",
    "createdAt": 1603327965856,
    "updatedAt": 1603327965856,
    "author": {
      "username": "commenter-708a3e",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-zg4q0g/comments

{
  "comment": {
    "body": "test comment xehq9c"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "79f3a0a1-2490-4453-ac93-158a8ff8882c",
    "slug": "title-zg4q0g",
    "body": "test comment xehq9c",
    "createdAt": 1603327965883,
    "updatedAt": 1603327965883,
    "author": {
      "username": "commenter-708a3e",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-zg4q0g/comments

{
  "comment": {
    "body": "test comment vrpeq7"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "f92801e3-28e6-4666-917f-3b42a7c85212",
    "slug": "title-zg4q0g",
    "body": "test comment vrpeq7",
    "createdAt": 1603327965913,
    "updatedAt": 1603327965913,
    "author": {
      "username": "commenter-708a3e",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-zg4q0g/comments

{
  "comment": {
    "body": "test comment q0z5qw"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "1f252431-1439-4acf-b9d9-3282f02516b7",
    "slug": "title-zg4q0g",
    "body": "test comment q0z5qw",
    "createdAt": 1603327965938,
    "updatedAt": 1603327965938,
    "author": {
      "username": "commenter-708a3e",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
### should disallow unauthenticated user
```
POST /articles/title-zg4q0g/comments

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Must be logged in."
    ]
  }
}
```
### should enforce comment body
```
POST /articles/title-zg4q0g/comments

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Comment must be specified."
    ]
  }
}
```
### should disallow non-existent article
```
POST /articles/foobar/comments

{
  "comment": {
    "body": "test comment e9mh0z"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article not found: [foobar]"
    ]
  }
}
```
## Get
### should get all comments for article
```
GET /articles/title-zg4q0g/comments
```
```
200 OK

{
  "comments": [
    {
      "createdAt": 1603327965692,
      "id": "3002d48d-8412-4940-a0a9-958140747e98",
      "body": "test comment v9e0wn",
      "slug": "title-zg4q0g",
      "author": {
        "username": "commenter-708a3e",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1603327965692
    },
    {
      "createdAt": 1603327965913,
      "id": "f92801e3-28e6-4666-917f-3b42a7c85212",
      "body": "test comment vrpeq7",
      "slug": "title-zg4q0g",
      "author": {
        "username": "commenter-708a3e",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1603327965913
    },
    {
      "createdAt": 1603327965883,
      "id": "79f3a0a1-2490-4453-ac93-158a8ff8882c",
      "body": "test comment xehq9c",
      "slug": "title-zg4q0g",
      "author": {
        "username": "commenter-708a3e",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1603327965883
    },
    {
      "createdAt": 1603327965827,
      "id": "ef7af888-cbf9-4752-8172-87f0914cc4f2",
      "body": "test comment w0oj4k",
      "slug": "title-zg4q0g",
      "author": {
        "username": "commenter-708a3e",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1603327965827
    },
    {
      "createdAt": 1603327965657,
      "id": "3ff174c7-3daf-49a0-877c-a2e9f6bcd51b",
      "body": "test comment lgykgl",
      "slug": "title-zg4q0g",
      "author": {
        "username": "commenter-708a3e",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1603327965657
    },
    {
      "createdAt": 1603327965725,
      "id": "e64cc4c5-0044-4522-8cca-2b0a75d2423b",
      "body": "test comment yt2566",
      "slug": "title-zg4q0g",
      "author": {
        "username": "commenter-708a3e",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1603327965725
    },
    {
      "createdAt": 1603327965856,
      "id": "43e9ed60-5bb6-478e-a75e-5c2e3b1eb9ff",
      "body": "test comment pwjn95",
      "slug": "title-zg4q0g",
      "author": {
        "username": "commenter-708a3e",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1603327965856
    },
    {
      "createdAt": 1603327965772,
      "id": "b78fd819-3504-461a-a18a-7574c280c70d",
      "body": "test comment 2lh0z",
      "slug": "title-zg4q0g",
      "author": {
        "username": "commenter-708a3e",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1603327965772
    },
    {
      "createdAt": 1603327965938,
      "id": "1f252431-1439-4acf-b9d9-3282f02516b7",
      "body": "test comment q0z5qw",
      "slug": "title-zg4q0g",
      "author": {
        "username": "commenter-708a3e",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1603327965938
    },
    {
      "createdAt": 1603327965801,
      "id": "28d22807-7a21-4b26-8b3d-2741e8978569",
      "body": "test comment zfq165",
      "slug": "title-zg4q0g",
      "author": {
        "username": "commenter-708a3e",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1603327965801
    }
  ]
}
```
## Delete
### should delete comment
```
DELETE /articles/title-zg4q0g/comments/3ff174c7-3daf-49a0-877c-a2e9f6bcd51b
```
```
200 OK

{}
```
### only comment author should be able to delete comment
```
DELETE /articles/title-zg4q0g/comments/3002d48d-8412-4940-a0a9-958140747e98
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Only comment author can delete: [commenter-708a3e]"
    ]
  }
}
```
### should disallow unauthenticated user
```
DELETE /articles/title-zg4q0g/comments/3002d48d-8412-4940-a0a9-958140747e98
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Must be logged in."
    ]
  }
}
```
### should disallow deleting unknown comment
```
DELETE /articles/title-zg4q0g/comments/foobar_id
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Comment ID not found: [foobar_id]"
    ]
  }
}
```
# User
## Create
### should create user
```
POST /users

{
  "user": {
    "email": "user1-0.scgfothjxg@email.com",
    "username": "user1-0.scgfothjxg",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "user1-0.scgfothjxg@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIxLTAuc2NnZm90aGp4ZyIsImlhdCI6MTYwMzMyNzk2NiwiZXhwIjoxNjAzNTAwNzY2fQ.AfLpjlrq32fbjV3aWud-kOuWXQ3zJXKPk2c_o2GVaok",
    "username": "user1-0.scgfothjxg",
    "bio": "",
    "image": ""
  }
}
```
### should disallow same username
```
POST /users

{
  "user": {
    "email": "user1-0.scgfothjxg@email.com",
    "username": "user1-0.scgfothjxg",
    "password": "password"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Username already taken: [user1-0.scgfothjxg]"
    ]
  }
}
```
### should disallow same email
```
POST /users

{
  "user": {
    "username": "user2",
    "email": "user1-0.scgfothjxg@email.com",
    "password": "password"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Email already taken: [user1-0.scgfothjxg@email.com]"
    ]
  }
}
```
### should enforce required fields
```
POST /users

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "User must be specified."
    ]
  }
}
```
```
POST /users

{
  "user": {
    "foo": 1
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Username must be specified."
    ]
  }
}
```
```
POST /users

{
  "user": {
    "username": 1
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Email must be specified."
    ]
  }
}
```
```
POST /users

{
  "user": {
    "username": 1,
    "email": 2
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Password must be specified."
    ]
  }
}
```
## Login
### should login
```
POST /users/login

{
  "user": {
    "email": "user1-0.scgfothjxg@email.com",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "user1-0.scgfothjxg@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIxLTAuc2NnZm90aGp4ZyIsImlhdCI6MTYwMzMyNzk2NiwiZXhwIjoxNjAzNTAwNzY2fQ.AfLpjlrq32fbjV3aWud-kOuWXQ3zJXKPk2c_o2GVaok",
    "username": "user1-0.scgfothjxg",
    "bio": "",
    "image": ""
  }
}
```
### should disallow unknown email
```
POST /users/login

{
  "user": {
    "email": "0.kp8ksq3qi6a",
    "password": "somepassword"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Email not found: [0.kp8ksq3qi6a]"
    ]
  }
}
```
### should disallow wrong password
```
POST /users/login

{
  "user": {
    "email": "user1-0.scgfothjxg@email.com",
    "password": "0.v7575zc2oud"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Wrong password."
    ]
  }
}
```
### should enforce required fields
```
POST /users/login

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "User must be specified."
    ]
  }
}
```
```
POST /users/login

{
  "user": {}
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Email must be specified."
    ]
  }
}
```
```
POST /users/login

{
  "user": {
    "email": "someemail"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Password must be specified."
    ]
  }
}
```
## Get
### should get current user
```
GET /user
```
```
200 OK

{
  "user": {
    "email": "user1-0.scgfothjxg@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIxLTAuc2NnZm90aGp4ZyIsImlhdCI6MTYwMzMyNzk2NiwiZXhwIjoxNjAzNTAwNzY2fQ.AfLpjlrq32fbjV3aWud-kOuWXQ3zJXKPk2c_o2GVaok",
    "username": "user1-0.scgfothjxg",
    "bio": "",
    "image": ""
  }
}
```
### should disallow bad tokens
```
GET /user
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Token not present or invalid."
    ]
  }
}
```
```
GET /user
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Token not present or invalid."
    ]
  }
}
```
```
GET /user
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Token not present or invalid."
    ]
  }
}
```
```
GET /user
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Token not present or invalid."
    ]
  }
}
```
## Profile
### should get profile
```
GET /profiles/user1-0.scgfothjxg
```
```
200 OK

{
  "profile": {
    "username": "user1-0.scgfothjxg",
    "bio": "",
    "image": "",
    "following": false
  }
}
```
### should disallow unknown username
```
GET /profiles/foo_0.cr0v6mwqrzq
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "User not found: [foo_0.cr0v6mwqrzq]"
    ]
  }
}
```
### should follow/unfollow user
```
POST /users

{
  "user": {
    "username": "followed_user",
    "email": "followed_user@mail.com",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "followed_user@mail.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6ImZvbGxvd2VkX3VzZXIiLCJpYXQiOjE2MDMzMjc5NjYsImV4cCI6MTYwMzUwMDc2Nn0.ZUV5Trsbu5UGrUlw4MI5O2yG3aIrfR684-TJshElL-Q",
    "username": "followed_user",
    "bio": "",
    "image": ""
  }
}
```
```
POST /profiles/followed_user/follow
```
```
200 OK

{
  "profile": {
    "username": "followed_user",
    "bio": "",
    "image": "",
    "following": true
  }
}
```
```
POST /profiles/followed_user/follow
```
```
200 OK

{
  "profile": {
    "username": "followed_user",
    "bio": "",
    "image": "",
    "following": true
  }
}
```
```
GET /profiles/followed_user
```
```
200 OK

{
  "profile": {
    "username": "followed_user",
    "bio": "",
    "image": "",
    "following": true
  }
}
```
```
GET /profiles/followed_user
```
```
200 OK

{
  "profile": {
    "username": "followed_user",
    "bio": "",
    "image": "",
    "following": false
  }
}
```
```
POST /users

{
  "user": {
    "username": "user2-0.fl16gk7xrsu",
    "email": "user2-0.fl16gk7xrsu@mail.com",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "user2-0.fl16gk7xrsu@mail.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIyLTAuZmwxNmdrN3hyc3UiLCJpYXQiOjE2MDMzMjc5NjYsImV4cCI6MTYwMzUwMDc2Nn0.yqVTlrZFV8scjxvuMozWx_IeNbpb99fJMrCpKGHhnyw",
    "username": "user2-0.fl16gk7xrsu",
    "bio": "",
    "image": ""
  }
}
```
```
POST /profiles/followed_user/follow
```
```
200 OK

{
  "profile": {
    "username": "followed_user",
    "bio": "",
    "image": "",
    "following": true
  }
}
```
```
DELETE /profiles/followed_user/follow
```
```
200 OK

{
  "profile": {
    "username": "followed_user",
    "bio": "",
    "image": "",
    "following": false
  }
}
```
```
DELETE /profiles/followed_user/follow
```
```
200 OK

{
  "profile": {
    "username": "followed_user",
    "bio": "",
    "image": "",
    "following": false
  }
}
```
```
DELETE /profiles/followed_user/follow
```
```
200 OK

{
  "profile": {
    "username": "followed_user",
    "bio": "",
    "image": "",
    "following": false
  }
}
```
### should disallow following with bad token
```
POST /profiles/followed_user/follow
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Token not present or invalid."
    ]
  }
}
```
## Update
### should update user
```
PUT /user

{
  "user": {
    "email": "updated-user1-0.scgfothjxg@email.com"
  }
}
```
```
200 OK

{
  "user": {
    "username": "user1-0.scgfothjxg",
    "email": "updated-user1-0.scgfothjxg@email.com",
    "image": "",
    "bio": "",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIxLTAuc2NnZm90aGp4ZyIsImlhdCI6MTYwMzMyNzk2NiwiZXhwIjoxNjAzNTAwNzY2fQ.AfLpjlrq32fbjV3aWud-kOuWXQ3zJXKPk2c_o2GVaok"
  }
}
```
```
PUT /user

{
  "user": {
    "password": "newpassword"
  }
}
```
```
200 OK

{
  "user": {
    "username": "user1-0.scgfothjxg",
    "email": "updated-user1-0.scgfothjxg@email.com",
    "image": "",
    "bio": "",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIxLTAuc2NnZm90aGp4ZyIsImlhdCI6MTYwMzMyNzk2NiwiZXhwIjoxNjAzNTAwNzY2fQ.AfLpjlrq32fbjV3aWud-kOuWXQ3zJXKPk2c_o2GVaok"
  }
}
```
```
PUT /user

{
  "user": {
    "bio": "newbio"
  }
}
```
```
200 OK

{
  "user": {
    "username": "user1-0.scgfothjxg",
    "bio": "newbio",
    "image": "",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIxLTAuc2NnZm90aGp4ZyIsImlhdCI6MTYwMzMyNzk2NiwiZXhwIjoxNjAzNTAwNzY2fQ.AfLpjlrq32fbjV3aWud-kOuWXQ3zJXKPk2c_o2GVaok"
  }
}
```
```
PUT /user

{
  "user": {
    "image": "newimage"
  }
}
```
```
200 OK

{
  "user": {
    "username": "user1-0.scgfothjxg",
    "image": "newimage",
    "bio": "newbio",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIxLTAuc2NnZm90aGp4ZyIsImlhdCI6MTYwMzMyNzk2NiwiZXhwIjoxNjAzNTAwNzY2fQ.AfLpjlrq32fbjV3aWud-kOuWXQ3zJXKPk2c_o2GVaok"
  }
}
```
### should disallow missing token/email in update
```
PUT /user
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Token not present or invalid."
    ]
  }
}
```
```
PUT /user

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "User must be specified."
    ]
  }
}
```
### should disallow reusing email
```
POST /users

{
  "user": {
    "email": "user2-0.e9x32o10lof@email.com",
    "username": "user2-0.e9x32o10lof",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "user2-0.e9x32o10lof@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIyLTAuZTl4MzJvMTBsb2YiLCJpYXQiOjE2MDMzMjc5NjYsImV4cCI6MTYwMzUwMDc2Nn0.FoGquP9WImzs2G2rKpVxClBw6xblNCRqJG9jqlvO5YI",
    "username": "user2-0.e9x32o10lof",
    "bio": "",
    "image": ""
  }
}
```
```
PUT /user

{
  "user": {
    "email": "user2-0.e9x32o10lof@email.com"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Email already taken: [user2-0.e9x32o10lof@email.com]"
    ]
  }
}
```
# Util
## Ping
### should ping
```
GET /ping
```
```
200 OK

{
  "pong": "2020-10-22T00:52:46.944Z",
  "AWS_REGION": "us-east-1",
  "DYNAMODB_NAMESPACE": "dev"
}
```
