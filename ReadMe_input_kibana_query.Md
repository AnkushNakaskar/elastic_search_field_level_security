```
PUT /customer/_doc/1
{
  "name": "John Doe",
  "id" : 1,
  "address":"address for fist person",
  "title" : "Titles from doucment 1",
  "body" : "body of document 1"
}
GET /customer/_search
{
  "query": {"match_all": {}}
}

GET /_xpack/license
POST /_license/start_trial?acknowledge=true
DELETE  /customer/_doc/1

POST /_security/role/my_admin_role
{
  "cluster": ["all"],
  "indices": [
    {
      "names": [ "customer" ],
      "privileges": ["all"],
      "field_security" : { 
        "grant" : [ "title", "body" ]
      }
      }
  ],
  "applications": [
    {
      "application": "myapp",
      "privileges": [ "admin", "read" ],
      "resources": [ "*" ]
    }
  ],
  "run_as": [ "other_user" ], 
  "metadata" : {
    "version" : 1
  }
}



POST /_security/user/jacknich
{
  "password" : "j@rV1s",
  "roles" : [ "my_admin_role" ],
  "full_name" : "Jack Nicholson",
  "email" : "jacknich@example.com",
  "metadata" : {
    "intelligence" : 7
  }
}


```