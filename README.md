# superheroes

## Getting started
To clone the the repository on your own machine run:

    git@github.com:Jeffy2k/superheroes.git

## setting up 
- Download the required dependencies by running:

        bundle install
- Set up the tables by running the following commands:

        rails db:migrate db:seed

- To start the server run

        rails s

## Endpoints

**GET /heroes**

Returns JSON data in the format below:

```json
[  

{ "id": 1, "name": "Kamala Khan", "super_name": "Ms. Marvel" },  

{ "id": 2, "name": "Doreen Green", "super_name": "Squirrel Girl" },  

{ "id": 3, "name": "Gwen Stacy", "super_name": "Spider-Gwen" }

]
```

**GET /heroes/:id**

If the `Hero` exists, JSON data in the format below is returned:

```json
{
  "id": 1,
  "name": "Kamala Khan",
  "super_name": "Ms. Marvel",
  "powers": [
    {
      "id": 1,
      "name": "super strength",
      "description": "gives the wielder super-human strengths"
    },
    {
      "id": 2,
      "name": "flight",
      "description": "gives the wielder the ability to fly through the skies at supersonic speed"
    }
  ]
}
```

If the `Hero` does not exist, the following JSON data, along with
the appropriate HTTP status code is returned:

```json
{   "error": "Hero not found" }

```

**GET /powers**

Returns JSON data in the format below:


```json
[
  {
    "id": 1,
    "name": "super strength",
    "description": "gives the wielder super-human strengths"
  },
  {
    "id": 1,
    "name": "flight",
    "description": "gives the wielder the ability to fly through the skies at supersonic speed"
  }
]
```

**GET /powers/:id**

If the `Power` exists, JSON data in the format below is returned:

```json
{
  "id": 1,
  "name": "super strength",
  "description": "gives the wielder super-human strengths"
}
```

If it doesn't exist the json data below is returned;

```json
{
  "error": "Power not found"
}
```
**PATCH /powers/:id**

This route updates an existing power. It accepts the properties below;

```json
{
  "description": "Updated description"
}
```
If power exists and is updated successfully, JSON data in the format below is returned;

```json
{
  "id": 1,
  "name": "super strength",
  "description": "Updated description"
}
```

If it doesn't exist return :

```json
{
  "error": "Power not found"
}
```
if it is not successfully updated return :

```json
{
  "errors": ["validation errors"]
}
```

**POST /hero_powers**

This route  creates a new `HeroPower` that is associated with an
existing `Power` and `Hero`. It accepts an object with the following
properties in the body of the request:

```json
{
  "strength": "Average",
  "power_id": 1,
  "hero_id": 3
}
```

If the `HeroPower` is created successfully, a response with the data
related to the `Hero` is  sent back:

```json
{
  "id": 1,
  "name": "Kamala Khan",
  "super_name": "Ms. Marvel",
  "powers": [
    {
      "id": 1,
      "name": "super strength",
      "description": "gives the wielder super-human strengths"
    },
    {
      "id": 2,
      "name": "flight",
      "description": "gives the wielder the ability to fly through the skies at supersonic speed"
    }
  ]
}
```

If the `HeroPower` is **not** created successfully, the following
JSON data, along with the appropriate HTTP status code is returned:

```json
{
  "errors": ["validation errors"]
}
```