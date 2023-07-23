# Headless UK

A headless [placeUK](https://github.com/g3vv/headless-uk) client written in [python](https://www.python.org/) 3.10.
> Credit to [Headless-Henk](https://github.com/tintin10q/headless-henk) and PlaceNL

# Simple Install

1. Install Python - https://www.python.org/
2. Download a zip of the script - https://github.com/G3VV/headless-uk/archive/refs/heads/main.zip
3. Unzip it inside a folder
4. Run `pip install -r requirements.txt`, this installs all the required stuff. (might need to do `pip install -r requirements.txt --user` or `python pip install -r requirements.txt`)
5. Run `python index.py` (might need to do `python3 index.py`)
6. A file should be automatically created called `config.toml`, configure the settings inside it (see below)
7. Once `config.toml` is configured run `python index.py` again.
8. and you should be finished and the script should be running on your account!

If you encounter any issues join our [Discord](https://discord.gg/ukplace) and ask for help in #script-help

## Toml Config File

You can set the options in a toml configuration file. By default, this file is [config.toml](config.toml) in the same
directory as the program.
You can also change where this file is located using the `--config` flag.

If you start the program without a config file present a basic config file will be created for you.

This is what the default file looks like:

```toml
reddit_username = 'YOUHAVETOADDTHIS'
reddit_password = 'YOUHAVETOADDTHIS'
chief_host = "placeuk.g3v.co.uk"
reddit_uri_https = 'https://gql-realtime-2.reddit.com/query'
reddit_uri_wss = 'wss://gql-realtime-2.reddit.com/query'
canvas_indexes = ["0", "1", "2", "3", "4", "5"]  # Canvas indexes to download, Toml has no null we use 'None' 
stats = false   # Wether to subscribe to stats updates from chief
pingpong = false   # Whether the client should show ping and pong messages.
```

### Using an auth token instead of username

Instead of having `reddit_username` and `reddit_password` you can also have:

```toml
auth_token = "INSERT TOKEN HERE"
```

But if you do not have `reddit_username` and `reddit_password` then the token will not refresh, and you have to replace it every 24 hours.

See the `How to get a reddit jwt token` section for information on how to get a reddit jwt token. 

> Note that in the toml file the `canvas_indexes` are all strings. In the env var this different and it is a json array
> of numbers and null.

# How to get reddit jwt?

The easiest way is to just run `login.py` to get a token. This will also automatically add the token to the `config.toml`.
You can also run `login.py` by doing `poetry run login`. These also support the --config flag.

You can also go to the website:

1. Go to r/place
2. Open dev tools by pressing `ctrl+shift+i`
3. Click on the network tab
4. Locate the pause button but do not press it, it looks like a stop button on chrome.
4. Now in the list of request find a `post` request to `https://gql-realtime-2.reddit.com/query`
5. Press the pause button to stop new request from coming in
6. Click on the post request in the list
7. Click on `headers`
8. Find the Authorization header
9. Copy the value of the authorization header. It should start with `Bearer ` and then a bunch of letters seperated.

> Realize that these tokens are valid for about 1440 minutes. There is no auto token refresh functionality yet. This is
> also because I don't know how reddit refreshes their tokens. Let me know if you koow.

**Be sure to not share this jwt with others!**

<br>
<br>
<br>

[Disclaimer](./disclaimer.md)
