# Web NFC API Test Design

## Introduction

This document is trying to design web platform tests for the
[Web NFC API](https://w3c.github.io/web-nfc/) specification.

The designed test cases are described by **test assertion** with proper
pre-/post-condition.

## Terms

Most of the terms are designed in W3C
[test methodology](http://www.w3.org/TR/test-methodology/) specification
which specify a method for wirting testable conformance requirements.

* **Requirement** means conformance requirement of the specification to be
  tested.
* **Test assertion** is a prose description of a test case intended for human
  testers - i.e., for a given test case, testable assertion defines exactly
  what the user agent needs to do (behaviorally or conditionally) to pass the
  test case. It is important to note that testable assertions don’t appear in
  a specification - they only appear in a test suite to describe a test case. 
* A **test case** is a machine processable object that is used to test one
  or more conformance requirements

## Test Design

### IDL to Test


### Example to Test


### Use Case to Test

#### Reading an NFC tag

```js
navigator.nfc.watch((message) => {
  // Test assertion: check that successfully read an NFC device.

  // Issue: seems it cannot get here if ndef.TNF is 6 (NFC Unchaged Type record)
  // or 7 (NFC Reserved Type record), surpose there is a tag with such record.
  // Then the watch doesn't take effect as it cannot read the NFC tag, right?
  // Or will it reject the promise?

  // Process massage here to check more.
  processMessage(message);
}).then(() => {
  // Added a watch.
  // Test assertion: check that navigator.nfc.watch() returns a promise.
}).catch((error) => {
  // Failed to add a watch.
  // Can further check the errors, e.g. SecurityError, NotSupportedError.
});

function processMessage(message) {
  // Test assertion: check that message is a dictionary of NFCMessage, etc.
  // https://w3c.github.io/web-nfc/#dom-nfcmessage

  for (let record of message.data) {
    // Test assertions: check that a certain type of record is read.
    // These assertions are useful for reading -> re-writing -> reading cases.

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