# node-postgraphile-example
Node-api that runs postgraphile api with simple-collection and omit-list-suffix enabled.

When you run './up.ps1' the postgres database container was build with initial schema contained in 00-database.sql and run it.
After runs albiberto/node-postgraphile container to query database via postgraphile.

The api responde to POST call at http://localhost:8080/graphql endpoint. Below some query examples: 

### GetAll
##### Query
```
{
    lights {
            id,
            lightType,
    		price,
			enabled
    }
}
```

##### Response
```
{
    "data": {
        "lights": [
            {
                "id": "21c2a49a-5d76-48bd-9673-44d455cf7394",
                "lightType": "Roald",
                "price": "5",
                "enabled": true
            }
        ]
    }
}
```

### GetById
##### Query
```
query GetLightById($id: UUID!) {
				  light(id: $id) {
					  id,
					  lightType,
					  price
    }
}
```
##### Variables
```
{
	"id": "21c2a49a-5d76-48bd-9673-44d455cf7394"
}
```
##### Response
```
{
    "data": {
        "light": {
            "id": "21c2a49a-5d76-48bd-9673-44d455cf7394",
            "lightType": "Alberto",
            "price": "5"
        }
    }
}
```

### Create
##### Query
```
mutation CreateLight($input: CreateLightInput!){
  createLight(input: $input) {
   light {
       lightType,
       price,
       enabled
  }
  }
}
```
##### Variables:
```
{
	"input" : {
			"light": {
			"id": "21c2a49a-5d76-48bd-9673-44d455cf7394",
		
			"lightType": "Roald",
			"price": 5,
			"enabled": true
		}
}
}
```
##### Response
```
{
    "data": {
        "createLight": {
            "light": {
                "lightType": "Roald",
                "price": "5",
                "enabled": true
            }
        }
    }
}
```
### Update
##### Query
```
mutation UpdateLight($input: UpdateLightInput!) {
				  updateLight(input: $input) {
					light {
			            id,
					    lightType,
					    price
					}
				  }
				}
```
##### Variables
```
{
	"input" : {
			"id": "21c2a49a-5d76-48bd-9673-44d455cf7394",
			"patch": {
			"lightType": "Alberto",
			"price": 5,
			"enabled": true
		}
}
}
```
##### Response 
```
{
    "data": {
        "updateLight": {
            "light": {
                "id": "21c2a49a-5d76-48bd-9673-44d455cf7394",
                "lightType": "Alberto",
                "price": "5"
            }
        }
    }
}
```

