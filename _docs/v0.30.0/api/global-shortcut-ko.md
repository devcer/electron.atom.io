---
version: v0.30.0
category: API
title: 'Global Shortcut Ko'
source_url: 'https://github.com/atom/electron/blob/master/docs/api/global-shortcut-ko.md'
---

﻿# global-shortcut

`global-shortcut` 모듈은 사용자가 다양한 단축키 작업을 정의 할 수 있도록 운영체제의 전역 키보드 단축키를 설정 등록/해제 하는 방법을 제공합니다.
참고로 설정된 단축키는 어플리케이션이 백그라운드로 작동(창이 포커스 되지 않음) 할 때도 여전히 계속 작동합니다.

```javascript
var globalShortcut = require('global-shortcut');

// 'ctrl+x' 단축키를 리스너에 등록합니다.
var ret = globalShortcut.register('ctrl+x', function() { console.log('ctrl+x is pressed'); })

if (!ret) {
  console.log('registration failed');
}

// 단축키가 등록되었는지 확인합니다.
console.log(globalShortcut.isRegistered('ctrl+x'));

// 단축키의 등록을 해제합니다.
globalShortcut.unregister('ctrl+x');

// 모든 단축키의 등록을 해제합니다.
globalShortcut.unregisterAll();
```

## globalShortcut.register(accelerator, callback)

* `accelerator` [Accelerator](http://electron.atom.io/docs/v0.30.0/api/accelerator-ko)
* `callback` Function

`accelerator`로 표현된 전역 단축키를 등록합니다. 유저로부터 등록된 단축키가 눌렸을 경우 `callback` 함수가 호출됩니다.

## globalShortcut.isRegistered(accelerator)

* `accelerator` [Accelerator](http://electron.atom.io/docs/v0.30.0/api/accelerator-ko)

지정된 `accelerator` 단축키가 등록되었는지 여부를 확인합니다. 반환값은 boolean(true, false) 입니다.

## globalShortcut.unregister(accelerator)

* `accelerator` [Accelerator](http://electron.atom.io/docs/v0.30.0/api/accelerator-ko)

`키코드`에 해당하는 전역 단축키를 등록 해제합니다.

## globalShortcut.unregisterAll()

모든 전역 단축키 등록을 해제합니다.
