# dashend (rewritten)

This repository is a rewritten version of [dashend](https://github.com/RoootTheFox/dashend).

This is rewritten to remove all the unnecessary components, fix potential ratelimiting, and to just function as a verification server. No database required!

It implements [dashauth](https://gist.github.com/RoootTheFox/743c983092b4db2a9fec13341d25b61f) GD-message based authentication for verifying user's GD account access.

# Setup
~~before setting anything up, be sure you don't have a VPS that isn't 1005 or 1006'd~~
First, run the following scripts to install all the needed dependencies and build:
```bash
npm install
npm run build
```
After that, copy the `.env.example` or rename it to `.env`
```md
PRODUCTION=1 # whether it should log, recommended to keep off to avoid flooding
TEST_ACC=1 # whether the GD account should be tested to see if it works (the server WILL stop if its invalid)
PORT=3000 # the port to host the server
GD_ACC_ID=AccountIDHere # gd account ID
GD_ACC_PW=AccountPasswordHere # gd account password
GD_ACC_GJP2=GJP2Here # this is optional, only use this if for whatever reason robtops hashing doesnt work and you cant use GD_ACC_PW
```
Once you've configured everything, simply run `npm start` to start the server!

Do note that everything is **in memory**, meaning if the server restarts or shuts down unexpectedly, users will need to reauthenticate if their tokens haven't expired already.

Also it's recommended to use my fork of [dashauth](https://github.com/FireMario211/dashauth) as currently the one made by rooot isn't ported to Geode v4

# Other API Routes not mentioned (that were added by me)
### `POST [base url]/verify`
#### Body:
- `token` The token to check if it's valid
#### Returns:
- `200 Ok` if the **token** is valid
- `401 Unauthorized` if the token is invalid.
#### Example response if OK:
```js
{
    success: true,
    message: "success",
    data: {
        id: 6253758, // GD Account ID
        username: "FireeDev", // GD Account Username
        token: "846b5af4434a935aa25bd0fb04c067502550df64307498067a0dff9a13190788",
        token_expiration: '2024-12-07T19:33:47.840Z' 
    }
}
```

# Instances using this repo
- `dashend.firee.dev`
