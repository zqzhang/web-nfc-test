# Web NFC API Test Design

## Introduction

## Terms

## Test Design

### IDL to Test


### Example to Test


### Use Case to Test

#### Reading an NFC tag

```js
function processMessage(message) {
  for (let record of message.data) {
    switch (record.recordType) {
      case "string":
        console.log('Data is string: ' + record.data);
        break;
      case "url":
        console.log('Data is URL: ' + record.data);
        break;
      case "json":
        console.log('JSON data: ' + record.data.myProperty.toString());
        break;
      case "opaque":
        if (record.mediaType == 'image/png') {
          var img = document.createElement("img");
          img.src = URL.createObjectURL(new Blob(record.data, record.mediaType));
          img.onload = function() {
            window.URL.revokeObjectURL(this.src);
          };
        }
        break;
    }
  }
}
```

**Pre-condition**: avaiable NFC tag and successfully tap simulation. The
`NFCWatchOptions` doesn't specify whether it is a tag or a peer.

**Notes**:

* Spec typo `NFC.watch(options, callback)` at
  https://w3c.github.io/web-nfc/#dom-nfc-watch; 
  should be `NFC.watch(callback, options)`.
* Spec typo "`MessageCallback`var>callback" at the 7th step
  https://w3c.github.io/web-nfc/#dfn-dispatch-nfc-content;
  should be `<code>MessageCallback</code> <var>callback</var>` in source file.

### Parameter to Test


### Algorithm, Statement to Test


## References