# Web NFC API Test Design

## Introduction

## Terms

## Test Design

### IDL to Test


### Example to Test


### Use Case to Test

#### Reading an NFC tag

```js
navigator.nfc.watch((message) => {
  // Process massage here or do more checking here.
  processMessage(message);
}).then(() => {
  // Added a watch.
}).catch((error) => {
  // Failed to add a watch.
});

function processMessage(message) {
  for (let record of message.data) {
    // The record here shall be NDEF record parsed following
    // https://w3c.github.io/web-nfc/#dfn-parsing-ndef-record
    switch (record.recordType) {
      case "empty":
        // record.mediaType = ""
        break;
      case "text":
        // record.mediaType = "text/plain"
        // record.mediaType = "text/plain;lang=*"
        break;
      case "url":
        // record.mediaType = "text/plain"
        break;
      case "json":
        // record.mediaType = "application/*json"
        break;
      case "opaque":
        // record.mediaType = ndef.TYPE 
        // record.mediaType = "application/octet-stream"
        break;
      default:
        // The 4.8 step doesn't specify the `record.recordType`,
        // we can check the message.url here.
        // Maybe this is a spec bug because the 5 step says that only
        // If NFC@[[suspended]] is false and message.data is not empty,
        // run the dispatch NFC content steps given message.
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
* Spec typo "`MessageCallback`var>callback" at the 1.7 step
  https://w3c.github.io/web-nfc/#dfn-dispatch-nfc-content;
  should be `<code>MessageCallback</code> <var>callback</var>` in source file.
* Spec typo `"application/octet-stream` at the 4.9.2 step
  https://w3c.github.io/web-nfc/#dfn-parsing-ndef-record;
  miss a `"`.
* Spec error in Example 4 `case "string":`; should be `case "text":` per
  https://w3c.github.io/web-nfc/#the-nfcrecord-dictionary

### Parameter to Test


### Algorithm, Statement to Test


## References