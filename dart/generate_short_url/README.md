# 🌐 Shorten any URL using bitly, and tinyurl.

A Dart Cloud Function that shortens any given URL using bitly and tinyurl.

_Example input:_

```json
{
    "provider": "bitly",
    "url": "https://www.google.com"
}
```

_Example output:_


```json
{
    "success": true,
    "url": "https://bit.ly/3SDv4VA"
}
```

## 🚀 Deployment

1. Clone this repository, and enter this function folder:

```
$ git clone https://github.com/open-runtimes/examples.git && cd examples
$ cd dart/generate_short_url
```

2. Place your api tokens inside `/lib/utils/api.dart`

You need to generate bitly access token, bitly group guid, and tinyurl access token, from the links given in the comments:

```dart
class ApiInfo {
  static const String bitly_url = "https://api-ssl.bitly.com/v4/shorten";
  static const String bitly_token = "[TOKEN]"; // https://app.bitly.com/settings/api/
  static const String bitly_group_guid = "[GUID]"; // https://dev.bitly.com/api-reference/#getGroups

  static const String tinyurl_url = "https://api.tinyurl.com/create";
  static const String tinyurl_token = "[TOKEN]"; // https://tinyurl.com/app/settings/api
}
```

3. Enter this function folder and build the code:
```
docker run -e INTERNAL_RUNTIME_ENTRYPOINT=lib/main.dart --rm --interactive --tty --volume ${PWD}:/usr/code openruntimes/dart:2.16 sh /usr/local/src/build.sh
```
As a result, a `code.tar.gz` file will be generated.

4. Start the Open Runtime:
```
docker run -p 3000:3000 -e INTERNAL_RUNTIME_KEY=secret-key --rm --interactive --tty --volume ${PWD}/code.tar.gz:/tmp/code.tar.gz:ro openruntimes/dart:2.16 sh /usr/local/src/start.sh
```

Your function is now listening on port `3000`, and you can execute it by sending `POST` request with appropriate authorization headers. To learn more about runtime, you can visit Dart runtime [README](https://github.com/open-runtimes/open-runtimes/tree/main/runtimes/dart-2.16).

## 🧪 Testing

I have included a python script (`test.py`) to send different POST requests, and test the script. You can tweak the values in that file to test the function for different scenarios.

## 📝 Notes
 - This function is designed for use with Appwrite Cloud Functions. You can learn more about it in [Appwrite docs](https://appwrite.io/docs/functions).
 - This example is compatible with Dart 2.16. Other versions may work but are not guaranteed to work as they haven't been tested. Versions below Dart 2.14 will not work, because Apwrite SDK requires Dart 2.14,