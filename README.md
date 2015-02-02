# static-file-handler

A static file Web server written in Dart.
It can be used as a stand-alone command line tool or imported as a package in a Dart application.

[![Build Status](https://drone.io/github.com/DanieleSalatti/dart-static-file-handler/status.png)](https://drone.io/github.com/DanieleSalatti/dart-static-file-handler/latest)

## Usage

The static-file-handler can be used:

* From the command line to serve files from a directory
* To serve static files while your server side app takes care of all the dynamic requests
* To spawn a Web server and serve static content from your app

### Serve a directory from the command line

You can serve files from a directory by running the Dart script located into `bin`:

```shell
cd static_file_handler/bin
dart static_file_handler.dart -r <root-path> -p <port>
```
Optionally, you can specify a configuration file in the command line parameters.

```shell
dart static_file_handler.dart -c <config-file>
```
A sample `config.yaml` file is available in the `bin` folder.

For a description of all the possible parameters:

```shell
dart static_file_handler.dart --help
```

### Serve static files from your server app

Add the package to your pubspec.yaml file:

```yaml
dependencies:
  static_file_handler: any
```

Create an instance of the static file handler using the named constructor `serveFolder(String directory)`, then call `handleRequest(HttpRequest request)` to serve your files. In this way your server application can handle all the dynamic requests, and you won't have to take care of the static files.

```dart
StaticFileHandler fileHandler = new StaticFileHandler.serveFolder("/path/to/folder");

fileHandler.handleRequest(httpRequest);
```
You can see an example that uses the `route` package to feed the static file handler only with non-dynamic requests in the `example/handle_request` folder.

### Spawn a Web server and serve static content from your app

If you just want to serve static files from your application, you can do as follows:

```dart
var fileHandler = new StaticFileHandler(path, port: port);
  
fileHandler.start();
```
When you are done you can stop the Web server using `fileHandler.stop()`.

You can see an example in the `example/serve_folder` folder.

## Adding custom MIME types

It is possible to add custom MIME types through a method call (`addMIMETypes(Map<String, String> types)`), or by editing the config file.

## Issues

Please file issues in the [Issue Tracker](https://github.com/DanieleSalatti/static-file-handler/issues)

## Acknowledgements

Special thanks to Anders Johnsen for the original code.
Thanks to [Adam Singer](https://github.com/financeCoding) for his contribution.
