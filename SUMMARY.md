# Table of contents

* [Prop-AI](README.md)
  * [API Reference](prop-ai/api-reference.md)
  * [Authentication](prop-ai/authentication.md)
  * [Connected Accounts](prop-ai/connected-accounts.md)
  * [Responses](prop-ai/responses/README.md)
    * [Handling Errors](prop-ai/responses/handling-errors.md)
    * [Expanding Responses](prop-ai/responses/expanding-responses.md)

## Core Resources

***

* ```yaml
  type: builtin:openapi
  props:
    models: true
  dependencies:
    spec:
      ref:
        kind: openapi
        spec: my-api
  ```
