# api documentation for  [yaml (v0.3.0)](https://github.com/tj/js-yaml)  [![npm package](https://img.shields.io/npm/v/npmdoc-yaml.svg?style=flat-square)](https://www.npmjs.org/package/npmdoc-yaml) [![travis-ci.org build-status](https://api.travis-ci.org/npmdoc/node-npmdoc-yaml.svg)](https://travis-ci.org/npmdoc/node-npmdoc-yaml)
#### Yaml parser

[![NPM](https://nodei.co/npm/yaml.png?downloads=true)](https://www.npmjs.com/package/yaml)

[![apidoc](https://npmdoc.github.io/node-npmdoc-yaml/build/screenCapture.buildNpmdoc.browser._2Fhome_2Ftravis_2Fbuild_2Fnpmdoc_2Fnode-npmdoc-yaml_2Ftmp_2Fbuild_2Fapidoc.html.png)](https://npmdoc.github.io/node-npmdoc-yaml/build/apidoc.html)

![npmPackageListing](https://npmdoc.github.io/node-npmdoc-yaml/build/screenCapture.npmPackageListing.svg)

![npmPackageDependencyTree](https://npmdoc.github.io/node-npmdoc-yaml/build/screenCapture.npmPackageDependencyTree.svg)



# package.json

```json

{
    "author": {
        "name": "TJ Holowaychuk",
        "email": "tj@vision-media.ca"
    },
    "bugs": {
        "url": "https://github.com/tj/js-yaml/issues"
    },
    "dependencies": {},
    "description": "Yaml parser",
    "devDependencies": {},
    "directories": {},
    "dist": {
        "shasum": "c31a616d07acdbc2012d73a6ba5b1b0bdd185a7f",
        "tarball": "https://registry.npmjs.org/yaml/-/yaml-0.3.0.tgz"
    },
    "gitHead": "18814da3b49eea33186c48e3d5ebf8a4b7c2af6c",
    "homepage": "https://github.com/tj/js-yaml",
    "license": "MIT",
    "main": "./lib/yaml.js",
    "maintainers": [
        {
            "name": "tjholowaychuk",
            "email": "tj@vision-media.ca"
        },
        {
            "name": "jbnicolai",
            "email": "jappelman@xebia.com"
        }
    ],
    "name": "yaml",
    "optionalDependencies": {},
    "readme": "ERROR: No README data found!",
    "repository": {
        "type": "git",
        "url": "git+https://github.com/tj/js-yaml.git"
    },
    "scripts": {},
    "version": "0.3.0"
}
```



# <a name="apidoc.tableOfContents"></a>[table of contents](#apidoc.tableOfContents)

#### [module yaml](#apidoc.module.yaml)
1.  [function <span class="apidocSignatureSpan">yaml.</span>eval (str)](#apidoc.element.yaml.eval)
1.  [function <span class="apidocSignatureSpan">yaml.</span>tokenize (str)](#apidoc.element.yaml.tokenize)
1.  string <span class="apidocSignatureSpan">yaml.</span>version



# <a name="apidoc.module.yaml"></a>[module yaml](#apidoc.module.yaml)

#### <a name="apidoc.element.yaml.eval"></a>[function <span class="apidocSignatureSpan">yaml.</span>eval (str)](#apidoc.element.yaml.eval)
- description and source-code
```javascript
eval = function (str) {
  return (new Parser(exports.tokenize(str))).parse()
}
```
- example usage
```shell
...

CommonJS JavaScript YAML parser, fast and tiny. Although this implementation
does not currently support the entire YAML specification, feel free to
fork the project and submit a patch :)

# Usage

  require('yaml').eval(string_of_yaml)

# Currently Supports

* Comments
* Sequences (arrays)
* Maps (hashes)
* Inline sequences
...
```

#### <a name="apidoc.element.yaml.tokenize"></a>[function <span class="apidocSignatureSpan">yaml.</span>tokenize (str)](#apidoc.element.yaml.tokenize)
- description and source-code
```javascript
tokenize = function (str) {
  var token, captures, ignore, input,
      indents = 0, lastIndents = 0,
      stack = [], indentAmount = -1

  // Windows new line support (CR+LF, \r\n)
  str = str.replace(/\r\n/g, "\n");

  while (str.length) {
    for (var i = 0, len = tokens.length; i < len; ++i)
      if (captures = tokens[i][1].exec(str)) {
        token = [tokens[i][0], captures],
        str = str.replace(tokens[i][1], '')
        switch (token[0]) {
          case 'comment':
            ignore = true
            break
          case 'indent':
            lastIndents = indents
            // determine the indentation amount from the first indent
            if (indentAmount == -1) {
              indentAmount = token[1][1].length
            }

            indents = token[1][1].length / indentAmount
            if (indents === lastIndents)
              ignore = true
            else if (indents > lastIndents + 1)
              throw new SyntaxError('invalid indentation, got ' + indents + ' instead of ' + (lastIndents + 1))
            else if (indents < lastIndents) {
              input = token[1].input
              token = ['dedent']
              token.input = input
              while (--lastIndents > indents)
                stack.push(token)
            }
        }
        break
      }
    if (!ignore)
      if (token)
        stack.push(token),
        token = null
      else
        throw new SyntaxError(context(str))
    ignore = false
  }
  return stack
}
```
- example usage
```shell
n/a
```



# misc
- this document was created with [utility2](https://github.com/kaizhu256/node-utility2)
