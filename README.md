# Web NFC Test

The [Web NFC API](https://w3c.github.io/web-nfc/) specification is now starting
to be in a stable state so we could start to look at creating W3C web platform
tests for it. Here come the [designed test cases](./designed.md).

Chromium project is implementing this feature at
[here](https://www.chromestatus.com/feature/6261030015467520). This feature
gives developers the ability to access Near Field Communication (NFC)
functionality of a device, such as reading and writing NFC tags as well as
exchanging data between NFC capable devices. See also
[launch bug 520391](https://code.google.com/p/chromium/issues/detail?id=520391),
[Blink layout tests](https://code.google.com/p/chromium/codesearch/#chromium/src/third_party/WebKit/LayoutTests/nfc/),
[Blink implementation](https://code.google.com/p/chromium/codesearch/#chromium/src/third_party/WebKit/Source/modules/nfc/).

In order to upstream everything including the implementation to Chromium, the
author Alexander Shalamov would need to provide LayoutTests and for that we will
need to extend TestRunner interface. That comes the
[test specification](./spec.md) with reference to the
[Testing Web Bluetooth](https://webbluetoothcg.github.io/web-bluetooth/tests/).
