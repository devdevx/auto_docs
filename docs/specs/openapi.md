# OpenAPI

## Spec

https://www.openapis.org/

## Reusable definition

```
components:
  schemas:
    id:
      type: string
    resource_id:
      type: object
      properties:
        id:
          $ref: '#/components/schemas/id'
    resource_properties:
      type: object
      properties:
        required_prop:
          type: string
        optional_prop:
          type: string
    resource_required_properties:
      type: object
      required:
        - required_prop
    resource:
      allOf:
        - $ref: '#/components/schemas/resource_id'
        - $ref: '#/components/schemas/resource_properties'
        - $ref: '#/components/schemas/resource_required_properties'
      
  requestBodies:
    create_update_resource:
      description: Create a new resource
      content:
        application/json:
          schema:
            allOf:
              - $ref: '#/components/schemas/resource_properties'
              - $ref: '#/components/schemas/resource_required_properties'
    partial_update_resource:
      content:
        application/json:
          schema:
            allOf:
              - $ref: '#/components/schemas/resource_properties'
              - type: object
                properties:
                  optional_prop:
                    nullable: true
```

**Note**: `partial_update_resource` definition follows [JSON Merge Patch](https://datatracker.ietf.org/doc/html/rfc7386) rules.

