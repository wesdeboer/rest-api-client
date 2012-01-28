A simple curl wrapper as an interactive shell for interacting with a REST api.

I found that I was making many curl requests repeatedly on the command line and thought that I could simplify things a little so I put this simple bash script together.

# Installation

1. Clone the repo

    ```git clone git://github.com/wesdeboer/rest-api-client.git rest-api-client```

2. Add to your $PATH

    ```echo 'PATH=$PATH:/path/to/rest-api-client' >> ~/.profile```

3. Run

    ```api search.twitter.com```

4. Example request

    ```@search.twitter.com> GET /search.json?q=github```

# Usage

As soon as you run the api script `api hostname` you will be presented with a command prompt similar to the following `@hostname>` where you are to enter your actions. `hostname` is the base url to your api for example `search.twitter.com`. If you don't pass a hostname as the first argument it will ask you for you before proceeding.

Once you are within the shell you can begin performing requests to your api. The four request types are four standard REST requests methods: `GET`, `PUT`, `POST`, `DELETE`. An example would be `GET /search.json`. You may append a query string to your request. If you are making a PUT or POST request you can pass an additional argument which will be the data string that is sent along with your request for example `@localhost> POST /users/profile.json fname=John&lname=Doe`.

You can also perform a simple action to login/logout, turn the json prettifier on/off or change your host. Type `help` to get a list of options.

`login` will ask for you username and password, this will be submitted on each subsequent request as Basic Authentication.

`logout` this will delete your current credentials, all subsequent requests will be unauthenticated.

`pretty on|off` will enable or disable pretty json which outputs it either nicely formated and indented or as a standard whitespace removed string.

`host [hostname]` will allow you to change the default hostname that requests are performed against. For example you might want to perform a request against your local dev api and again against a sandbox or even production url to compare.

`!!` this is a simplified replica of the bash repeat last command, this will repeat the last *request*. This is great when debugging the same request multiple times so you don't have to re-type the whole thing again. It will ignore any of the actions such as host/login/etc.. so you can run a GET request and then change your login or host and then enter `!!` to run that same GET request again against that new host or with the new login details.

# Requirements

You will need to have curl for the requests but I doubt you were testing a REST api through cli without having installed curl anyways.

**Recommended** In order to output prettified json you currently need python with json or simplejson decoder installed. 

# Caveats

* Currently only Basic Authentication is supported for authenticating against your api.
* JSON output is the ideal format, there is support for outputting json prettified via `python -mjson.tool`. Any other format will just dump the raw output. Be sure you have pretty off `@host> pretty off` if you are expecting another format or python will just respond with a _No JSON object could be decoded_ error.
