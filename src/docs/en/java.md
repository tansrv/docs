## Get connector

```shell
git clone https://github.com/tansrv/tanserver-connectors.git
```

## Install

Copy `java/tan` directory in your project and import it.

## Requirements

| Platform | Version
| :------  | :------
| Java     | 7+
| Android  | 7.0+

## Example

```java linenums="1"
import tan.Tanserver;
import java.io.IOException;

/* Initialize connection information.  */
Tanserver tan = new Tanserver("tanserver.org", 2579);

/* Get JSON string from the server.  */
tan.getJSON("api", "{}", new Tanserver.Callback() {

    @Override
    public void onSuccess(String jsonString) {
        System.out.println(jsonString);
    }

    @Override
    public void onFailure(IOException err) {
        /* An error has occurred, notify the user of network failure.  */
        System.out.println("ERROR! " + err.getMessage());
    }
});
```

## getJSON()

| Declaration        | `void` getJSON(String userApi, String jsonString, Callback callback)
| :------            | :------
| Description        | Get JSON string from the server.
| Param `userApi`    | API provided by the server.
| Param `jsonString` | The JSON string that will be sent to the server.
| Param `callback`   | Needs to implement `void onSuccess(String jsonString)` and `void onFailure(IOException err)`. When the request is successful, `onSuccess()` will be called, otherwise `onFailure()` will be called.
| Note               | Android must add `<uses-permission android:name="android.permission.INTERNET"/>` in `AndroidManifest.xml`.

## Common reasons why `onFailure()` is called

1. The client is offline or the server is not started.

2. SSL handshake failed.

3. API does not exist.

4. `jsonString` is an invalid JSON string.

5. `jsonString` is too large and exceeds `client_max_body_size`.
