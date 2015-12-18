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

**Notes**:

* There is a typo `NFC.watch(options, callback)` at
  https://w3c.github.io/web-nfc/#dom-nfc-watch
  Should be `NFC.watch(callback, options)`

### Parameter to Test


### Algorithm, Statement to Test


## References