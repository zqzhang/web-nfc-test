# Testing Web NFC API

```js
// Alex's thoughts of extending TestRunner interface
interface TestRunner {
  void setNfcSupported(True|False);
  void createNfcDevice(Tag|Peer);
  void appendNfcRecord(RecordType, RecordMediaType, RecordData);
  void proximityEvent(Found | Lost, Milliseconds)
};

// And his usage
function testPassedCB(nfcmessage) {
 // check that message is correct
}

testRuner.createTag();
testRuner.appendNFCRecord("text", "text/plain", "HelloWorld!");
navigator.nfc.watch(testPassedCB);
testRuner.proximityEvent("found", 10);
```
