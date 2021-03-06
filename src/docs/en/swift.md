## Get connector

```shell
git clone https://github.com/tansrv/tanserver-connectors.git
```

## Install

Copy `swift/src/Tanserver.swift` to your Swift project.

## Requirements

| Platform     | Version
| :------      | :------
| iOS          | 13.0+
| macOS        | 10.15+
| Mac Catalyst | 13.0+
| tvOS         | 13.0+
| watchOS      | 6.0+
| Xcode        | 11.0+

## Example

```swift linenums="1"
/* Initialize connection information.  */
let tan = Tanserver(host: "tanserver.org", port: 2579)

/* Get JSON data from the server.  */
tan.getJSON(userApi: "api",
            jsonString: "{}",
            completion: { jsonData, err in

    if err != nil {
        print(err)  /* An error has occurred, notify the user of network failure.  */
        return
    }

    print(String(data: jsonData!, encoding: .utf8))
})
```

## getJSON()

| Declaration                       | func getJSON(userApi: String, jsonString: String, completion: @escaping (Data?, NWError?) -> Void)
| :------                           | :------
| Description                       | Get JSON data from the server.
| Param `userApi`                   | API provided by the server.
| Param `jsonString`                | The JSON string that will be sent to the server.
| Param `completion(Data, NWError)` | `Data` will contain JSON answer from tanserver. If an error occurs, `NWError` will not be nil.

## Common causes of errors

1. The client is offline or the server is not started.

2. SSL handshake failed.

3. API does not exist.

4. `jsonString` is an invalid JSON string.

5. `jsonString` is too large and exceeds `client_max_body_size`.
