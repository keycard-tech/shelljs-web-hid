## ShellJS Web HID

ShellJS Web HID is an implementation of the communication layer.

***

### Installation

```
npm install @choppu/shelljs-web-hid
```

### Usage example

```javascript
import TransportWebHID from "@choppu/shelljs-web-hid";
...
let transport: any;
transport = await TransportWebHID.create();
...
```

### Live Demo

You can check a demo at [Shell Web HID Example Page](https://choppu.github.io/shelljs-example/).

### Support status

WebHID is currently only supported on Google Chrome / Chromium and Microsoft Edge (version 89 and later) and on Electron renderers. It requires a secure context (HTTPS or `localhost`). It is not supported on Safari or Firefox, where `TransportWebHID.isSupported()` resolves to `false`.

## API

#### Table of Contents

- [ShellJS Web HID](#shelljs-web-hid)
  - [Installation](#installation)
  - [Usage example](#usage-example)
  - [Live Demo](#live-demo)
  - [Support status](#support-status)
- [API](#api)
    - [Table of Contents](#table-of-contents)
  - [TransportWebHID](#transportwebhid)
    - [Parameters](#parameters)
    - [close](#close)
    - [exchange](#exchange)
      - [Parameters](#parameters-1)
    - [isSupported](#issupported)
    - [list](#list)
    - [listen](#listen)
      - [Parameters](#parameters-2)
    - [request](#request)
    - [openConnected](#openconnected)
    - [open](#open)
      - [Parameters](#parameters-3)

### TransportWebHID

**Extends Transport**

WebHID Transport implementation.

#### Parameters

*   `device` **HIDDevice**

#### close

Releases the transport device.

Returns **[Promise](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Promise)\<void>**

#### exchange

Exchanges with the device using the APDU protocol.

##### Parameters

*   `apdu` **[Buffer](https://nodejs.org/api/buffer.html)**

Returns **[Promise](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Promise)<[Buffer](https://nodejs.org/api/buffer.html)>** a promise of the APDU response

#### isSupported

Checks whether the WebHID transport is supported.

Returns **[Promise](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Promise)<[boolean](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Boolean)>**

#### list

Lists the WebHID devices that were previously authorized by the user.

Returns **[Promise](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Promise)<[Array](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Array)\<HIDDevice>>**

#### listen

Actively listens to WebHID devices and emits ONE device
that was either accepted before, if not it will trigger the native permission UI.

Important: it must be called in the context of a UI click!

##### Parameters

*   `observer` **Observer\<DescriptorEvent\<HIDDevice>>**

Returns **Subscription**

#### request

Similar to create(), except that it will always display the device permission (even if some devices are already accepted).

Returns **[Promise](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Promise)\<TransportWebHID>**

#### openConnected

Similar to create(), except that it will never display the device permission (it returns a Promise\<?Transport>, null if it fails to find a device).

Returns **[Promise](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Promise)\<(TransportWebHID | null)>**

#### open

Creates a Shell transport with a HIDDevice.

##### Parameters

*   `device` **HIDDevice**

Returns **[Promise](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Promise)\<TransportWebHID>**
