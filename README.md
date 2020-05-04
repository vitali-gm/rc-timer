# RcTimerOrg


Vue.js Component.

And of course RcTimerOrg itself is open source with a [public repository][ghu]
 on GitHub.

### Installation

```sh
$ npm i rc-timer-org
```


### Usage
```sh
<template>
    <div>
        <rc-timer-org expire="2020-05-02 23:59:59"/>
    </div>
</template>

<script>
import { RcTimerOrg } from 'rc-timer-org'
 export default {
     name: 'NAME',
     components: { RcTimerOrg },
      ...
 }
 </script>

```

### Props

> expire - expire datetime, format: 2020-05-02 23:59:59
> noTitles - hide hint text, default: false
> noZero - hide zero text, default: false, example: 5:10:5

### Example
noTitle
```sh
<rc-timer-org expire="2020-05-10 23:59:59" noTitle/>
```

noZero
```sh
<rc-timer-org expire="2020-05-10 23:59:59" noZero/>
```



License
----

MIT



[ghu]: <https://github.com/vitali-gm/rc-timer>
