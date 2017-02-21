# api-explorer

`usage: api <profile> <action> <endpoint> [...data]`

---

`<profile>` is the name of a file in ~/.config/api-explorer

At minimum it should contain a server entry:

`server  https://api.github.com`

You'll likely also want to add authentication.

The [GitHub API](https://developer.github.com/guides/getting-started/) specifies you should provide your access key as a header in the following form:

`Authorization: token 5199831f4dd3b79e7c5b7e0ebe75d67aa66e79d4`

so in the config file you would add

`header  Authorization: token 5199831f4dd3b79e7c5b7e0ebe75d67aa66e79d4`

You can now query the API a lot simpler:

`api github get user`
