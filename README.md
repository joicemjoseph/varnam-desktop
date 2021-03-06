# Varnam Desktop App
=============

Cross-platform desktop app for Varnam. Uses [varnam-editor](https://github.com/thetronjohnson/varnam-editor) as GUI frontend.

### Installation

Clone the repo.

Build `libvarnam` :

```
git submodule update --init --recursive
cd libvarnam/libvarnam && cmake . && make varnamstatic && ln -s $(realpath libvarnamstatic.a) libvarnam.a && cd -
```

Build `varnam` :

```
make deps
make editor
make build
```

Run :

```
./varnam
```

Thanks to [stuffbin](https://github.com/knadh/stuffbin), HTML+CSS+JS files are all merged into one big binary (`varnam`).

### Usage

varnamd supports the following command line arguments:

+ `p` int. Run daemon in specified port
+ `max-handle-count` int. Maximum number of handles can be opened for each language
+ `host` string. Host for the varnam daemon server. 
+ `ui` string. UI directory path. Put your index.html here.
+ `enable-internal-apis` boolean. Enable internal APIs
+ `enable-ssl` boolean
+ `cert-file-path` string. Certificate file path
+ `key-file-path` string.
+ `upstream` string. Provide an upstream server
+ `enable-download`. string. Comma separated language identifier for which varnamd will download words from upstream
+ `sync-interval` int.
+ `log-to-file` boolean. If true, logs will be written to a file
+ `version`

### API

When a request is made to translate a word, say 'Malayalam',

`Request URL:  https://api.varnamproject.com/tl/{langCode}/{Word}`

`Request Method: GET`

and the response for https://api.varnamproject.com/tl/ml/Malayalam will be:

```json
{
  "success": true,
  "error": "",
  "at": "2020-07-02 11:10:30.309343848 +0000 UTC",
  "result": [
    "മലയാളം",
    "മലയാലം",
    "മലയാ‍ളം",
    "മലായാളം",
    "മലയളം",
    "മ്മലയലം",
    "മലയാളമാ",
    "മലയാളമാദ്ധ്യമത്തിലൂ",
    "മലയാളമാദ്ധ്യമത്തിലൂടെ",
    "മലയാളമാദ്ധ്യമത്തിൽ",
    "മലയാളമാദ്ധ്യമം"
  ],
  "input": "Malayalam"
}
```

##### see server.go for supported APIs.
