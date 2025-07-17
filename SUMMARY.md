# Table of contents

* [Introduction](README.md)
  * [API Reference](introduction/api-reference.md)
  * [Authentication](introduction/authentication.md)
  * [Connected Accounts](introduction/connected-accounts.md)
  * [Responses](introduction/responses/README.md)
    * [Handling Errors](introduction/responses/handling-errors.md)
    * [Expanding Responses](introduction/responses/expanding-responses.md)
* [Core Resources](core-resources/README.md)
  * ```yaml
    type: builtin:openapi
    props:
      models: true
    dependencies:
      spec:
        ref:
          kind: openapi
          spec: prop-ai-api
    ```
