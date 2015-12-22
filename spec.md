# Testing Web NFC API

## Abstract

This document describes functions used in testing the Web NFC API.

## Introduction

Writing cross-browser tests for the
[Web NFC API](https://w3c.github.io/web-nfc/)
is difficult because it interacts with devices that live outside the browser.
This document describes APIs that aid in this testing, and can be implemented
by each browser to either mock out the external interaction, or to configure
an external test device to behave as the test needs.

Tests using these functions will be firstly contributed to [Chromium’s
repository](https://code.google.com/p/chromium/codesearch/#chromium/src/third_party/WebKit/LayoutTests/nfc/),
and will eventually live in the
[W3C’s Web Platform Tests](https://github.com/w3c/web-platform-tests).

## Security and privacy considerations

These functions MUST NOT be exposed to web content. Only trusted testing code
may access them.

## `TestRunner` interface extensions

```js
// partial interface Window {
//   readonly attribute TestRunner testRunner;
// };

// interface TestRunner {
partial interface TestRunner {
  void setNfcSupported(True|False);
  void createNfcDevice(Tag|Peer);
  void appendNfcRecord(RecordType, RecordMediaType, RecordData);
  void proximityEvent(Found | Lost, Milliseconds)
};
```

## Examples

```
function testPassedCB(nfcmessage) {
 // check that message is correct
}

testRuner.createTag();
testRuner.appendNFCRecord("text", "text/plain", "HelloWorld!");
navigator.nfc.watch(testPassedCB);
testRuner.proximityEvent("found", 10);
```

## References

* Testing Web Bluetooth. Draft Community Group Report, 23 September 2015. URL:
  https://webbluetoothcg.github.io/web-bluetooth/tests/
* Kenneth Rohde Christiansen, Zoltan Kis. Web NFC API. Draft Community Group
  Report 13 November 2015. URL: https://w3c.github.io/web-nfc/
