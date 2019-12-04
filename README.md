# Web Request Action

This action makes a web request to any JSON API. Supports all HTTP methods, JSON payload and basic authentication.

## Inputs

| Parameter  | Required | Info                                               |
| ---------- | -------- | -------------------------------------------------- |
| `url`      | `true`   | Web request URL endpoint                           |
| `method`   | `true`   | Web request method (`GET`, `POST`, `PUT`, `PATCH`) |
| `payload`  | `false`  | Web request payload in JSON format                 |
| `username` | `false`  | Basic auth username                                |
| `password` | `false`  | Basic auth password                                |

## Outputs

Output format: `JSON`

```json
{
  "output": {
    "url": "<str url>",
    "method": "<str method>",
    "payload": {},
    "time": "<str time>",
    "statusCode": "<int statusCode>"
  }
}
```

### Example output usage

```yaml
run: |
  $output = '${{ steps.webhook.outputs.output }}' | ConvertFrom-Json
  Write-Host "Time from output $($output.time) statusCode $($output.statusCode)"
```

## Example usage

```yaml
uses: satak/webrequest-action@master
with:
  url: https://webhook.site/${{ secrets.WEBHOOK_ID }}
  method: POST
  payload: '{"name": "${{ env.MY_NAME }}"}'
  username: ${{ secrets.BASIC_AUTH_UN }}
  password: ${{ secrets.BASIC_AUTH_PW }}
```

## Documentation

How to create your custom GitHub action:

<https://help.github.com/en/actions/automating-your-workflow-with-github-actions/creating-a-javascript-action>

- How to compile your `index.js` file:
  - install node
  - install ncc globally wih npm: `npm i -g @zeit/ncc`
  - run `ncc build index.js`
