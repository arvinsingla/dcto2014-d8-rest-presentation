## Presentation Notes

Demo TODO: prior to presentation

- Ensure PHP > 5.4
- import d8.sql.gz on desktop

Demo GET portion

1. Visit admin/modules page
1. Enable the following modules
   RESTful Web Services
   Serialization
   restui
1. Demonstrate how the yml configruation for rest services works and how restui module makes it easier to manage that configuration. (Enable get with JSON and Cookie authentication)
1. Add a content type (Article)
1. Add some fields on that content type.
1. Show node/1 on a drupal node
1. Open postman and use the following configuration to fetch the nodes json equivalent.

Accept: application/json
HTTP Method: GET
Path: /node/1

Demo POST/PATCH/DELETE portion

1. Enable the HAL module and authentication module
1. Update the restui config for all content types to include hal and auth options for GET/POST/PATCH/DELETE
1. Perform a get again instead using hal+json as the Accept header to demonstrate what is added with HAL
1. Adjust permissions to allow authenticated users to perform POST/PATCH/DELETE
1. Create a node using hal+json using the following details

Creating a node
Content-Type: application/hal+json
HTTP Method: POST
Path: /entity/node

{
    "_links": {
      "type": {
        "href":"http://d8-alpha11.dev/rest/type/node/article"
      }
    },
    "title": { 
        "value": "An awesome second node"
    },
    "body": {
        "value": "I really hope this works"
    }
}

GOTCHA: Articles posted are not associated with the UID that posted them. They are currently Anonymous 
GOTCHA: GET/PATCH/DELETE requests follow node/nid path structure, POST follow entity/node url structure (https://drupal.org/node/2019123)   
GOTCHA: Standard Drupal Create/Edit permissions are required in order for anon to create content.
GOTCHA: Session based authentication requires sending a CSRF token (rest/session/token) using the X-CSRF-Token header
GOTCHA: Currently POST does not return any information surrounding the entity you just created, no NID or UUID
GOTCHA: Entity reference fields use the UUID, not NID when creating a reference to another entity.
GOTCHA: Imagefield support currently doesn't exist (https://drupal.org/node/1927648)

1. Updated the node we just created

Update a node
Content-Type: application/hal+json
HTTP Method: PATCH
Path: /node/x

{
    "_links": {
      "type": {
        "href":"http://d8-alpha11.dev/rest/type/node/article"
      }
    },
    "title": { 
        "value": "An updated title"
    },
    "body": {
        "value": "This is a test"
    }
}

1. Delete the node we just updated

Delete a node
Content-Type: application/hal+json
HTTP Method: DELETE
Path: /node/x


