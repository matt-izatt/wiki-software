# curl

### Description

Curl is a command-line tool that allows us to do HTTP requests from shell. Curl stands for 'Client URL'.

### Options

#### Send data

Send data as request body

```bash
curl --data <DATA> <URL>
```

_Examples:_

```bash
curl --data "name=John&surname=Doe" http://www.dataden.tech
```

```bash
curl --data '{"name":"John","surname":"Doe"}' http://www.dataden.tech
```

#### Set HTTP Method

Set the verb sent in the request header

```bash
curl --request "<VERB>" <URL>
```

_Example:_

```bash
curl --request "DELETE" https://example.com
```

#### Set HTTP Header

Set a request header

```bash
curl --header "<KEY>: <VALUE>" <URL>
```

_Example:_

```bash
curl --header "X-First-Name: Joe" https://example.com
```

#### Output

Save returned data to a file

```bash
curl --output <FILENAME.EXTENSION> <URL>
```

```shell
curl --output <FILENAME>.<EXTENSION> <URL>
```

_Example_:

```bash
curl --output output.html www.dataden.tech
```

#### Basic Auth

Use basic auth

```bash
curl --user <NAME>:<PASSWORD> --basic <URL>
```

_Example_:

```bash
curl -user name:password --basic https://example.com
```

#### Save cookies

Save cookies to a file

```bash
curl --cookie-jar <FILENAME>.<EXTENSION> <URL>
```

_Example:_

```bash
curl --cookie-jar store-here.txt https://example.com
```

#### Send cookies

Send a cookie

```bash
curl --cookie <FILENAME> <URL>
```

_Example:_

```bash
 curl --cookie cookiefile https://example.com
```
