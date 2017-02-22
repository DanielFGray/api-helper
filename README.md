# api-helper

## Dependencies

* [curl](https://curl.haxx.se)

## Why

* Many API tasks require sending the same headers or data with every request
* Typing (or digging through your shell history for) the same options is tedious
* You want to be able to save API requests (to your shell rc for example) without leaking your auth tokens everywhere

## Usage

```
usage: api <profile> <action> <endpoint> [...data]
```

* `profile` is the name of a file in `~/.config/api-helper` containing a server URL and arbitrary curl options
* `action` is an http verb like `get`, `put`, `post`, etc
* `endpoint` is a route to be appended to the `server` defined in the `profile`
* `data` are curl options like `--data`  to be sent with the request

## Quick tutorial

At minimum your profile should contain a server entry:

```
~/.config/api-helper/github

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

Which will execute

````
curl --request GET --header 'Authorization: token 5199831f4dd3b79e7c5b7e0ebe75d67aa66e79d4' https://api.github.com/user
````

The remainder of arguments are passed directly to curl, so to pass data to the [API](https://developer.github.com/api/), you use the normal `curl` options. Creating a repo on GitHub is now as simple as:

```
api github post user/repos -d '{"name":"awesome_new_repo"}'
```

---

For [GitLab](https://docs.gitlab.com/ce/api/README.html), the process is similar. Create a file at `~/.config/api-helper/gitlab` and put a server in there:

```
server  https://gitlab.com/api/v3/
```

The [auth for GitLab](https://docs.gitlab.com/ce/api/README.html#authentication) is only slightly different:

```
header  PRIVATE-TOKEN: 9koXpg98eAheJpvBs5tK
```

You can find your GitLab private token on your [account page](https://gitlab.com/profile/account).

You can of course specify multiple `header` entries, if you want to add `sudo` for example.

---

If the API you're using prefers HTTP auth you can specify a user in the config file: 

```
server  https://api.teknik.io/v1
user    user:password
```

Or if the API prefers it as a plain data key:

```
server  http://ws.audioscrobbler.com/2.0/
data    api_key=dfd71eb15d3d76069d85617de769872a
data    format=json
```
