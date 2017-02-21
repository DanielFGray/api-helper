# api-explorer

`usage: api <profile> <action> <endpoint> [...data]`

---

`<profile>` is the name of a file in ~/.config/api-explorer

At minimum it should contain a server entry:

```
server		https://api.github.com
```

You'll likely also want to add authentication.

The [GitHub API](https://developer.github.com/guides/getting-started/) specifies you should provide your [access key](https://github.com/settings/tokens) as a header in the following form:

```
Authorization: token 5199831f4dd3b79e7c5b7e0ebe75d67aa66e79d4
```

so in the config file you would add

```
header  Authorization: token 5199831f4dd3b79e7c5b7e0ebe75d67aa66e79d4
```

You can now query the API a lot simpler:

```
api github get user
```

which is equivalent to

````
curl --request GET --header Authorization: token 5199831f4dd3b79e7c5b7e0ebe75d67aa66e79d4 https://api.github.com/user
````

The remainder of arguments are passed directly to curl, so to pass data to the API, you use the normal `curl` options. Creating a repo on GitHub is now as simple as:

```
api github post user/repos -d '{ "name": "api-explorer", "auto_init": false }'
```
