# Chatopera Docs BOT

Documentation as a Chatbot. You know, for chat.

[Demo](https://oh-my.cskefu.com/im/text/0e8xuk.html)

![image](https://user-images.githubusercontent.com/3538629/165872617-4528090d-c662-4d9a-b60c-db8340625b14.png)

## Featured

* Parse local markdown docs inside directory recursivly, generate FAQs File for Chatopera BOT Platform.

* Further import into a BOT on Chatopera, details in [doc](https://dwz.chatopera.com/754yr1).

## Install

Publish on npmjs, [link](https://www.npmjs.com/package/@chatopera/docsbot).

```
npm install -g @chatopera/docsbot
```

Now, `docsbot` is available in CLI path.

## Usage

```
docsbot --baseurl $BASE_URL \
    -i $DOCS_HOME \
    -f $DOCS_FOLDERS \
    -o $FAQ_OUTOUT
```

| Key | Sample | Description |
| --- | --- | --- |
| `BASE_URL` | `https://docs.chatopera.com/products/` | conjunction for the per doc page link  |
| `DOCS_HOME` | `~/chatopera/docs/docfx_project/products` | Docs root dir |
| `DOCS_FOLDERS` | `chatbot-platform,cskefu` | Child dirs to be parsed in root dir |
| `FAQ_OUTPUT_FILE` | `./tmp/bot.faq.json` | Generated file in Chatopera BOT FAQ Format |

Assume your docs folders are like this, and docs site are at <https://docs.chatopera.com/products/>:

```
$DOCS_HOME(Root dir)
└───chatbot-platform
    |───appendix
    |───contract
    |───explanations
    |───howto-guides
    |───references
    │   ├───func-builtin
    │   └───sdk
    │       ├───chatbot
    │       └───chatopera
    └───tutorials
```

Then, the Docs link address of `$DOCS_HOME/chatbot-platform/appendix/index.md` would be interpreted as `https://docs.chatopera.com/products/chatbot-platform/appendix/index.html`.

This docs are also hosted [on GitHub](https://github.com/chatopera/docs).

* baseurl: set with command line
* docfoler: iterater with `DOCS_FOLDER`, split by `,`
* filepath: the markdown files in each `docfoler`, where extension `.md` is replaced with `.html`

## Upload into Chatopera BOT Platform

Install Chatopera SDK for `bot` CLI.

```
npm install -g @chatopera/sdk
```

Touch .env

```
# Chatopera BOT Service endpoint
BASE_URL=https://docs.chatopera.com/products/
BOT_PROVIDER=https://bot.chatopera.com
BOT_CLIENT_ID=xx
BOT_CLIENT_SECRET=xx
BOT_ACCESS_TOKEN=
# BOT_FAQ_FILE is generated by docsbot
BOT_FAQ_FILE=bot.faq.json
```

Run the job

```
source .env
bot faq -a import -f ./$BOT_FAQ_FILE
```

### Others

```
docsbot --help
```

## Development

```
npm install
node bin/cmd.js --help
cp sample.env .env
./scripts/dev.sh
```

## License

[Apache2](./LICENSE)

[![chatoper banner][co-banner-image]][co-url]

[co-banner-image]: https://user-images.githubusercontent.com/3538629/42383104-da925942-8168-11e8-8195-868d5fcec170.png
[co-url]: https://docs.chatopera.com
