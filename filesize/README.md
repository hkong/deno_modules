# filesize

filesize provides a simple way to get a human readable file size string from a number (float or integer) or string.

## Optional settings

`import { filesize, Options } from "https://deno.land/x/filesize/mod.ts";`

`filesize()` accepts an optional descriptor object, `Options`, as a second argument, so you can customize the output.

### base

_*(number)*_ Number base, default is `2`

### bits

_*(boolean)*_ Enables `bit` sizes, default is `false`

### exponent

_*(number)*_ Specifies the symbol via exponent, e.g. `2` is `MB` for base 2, default is `-1`

### fullform

_*(boolean)*_ Enables full form of unit of measure, default is `false`

### fullforms

_*(array)*_ Array of full form overrides, default is `[]`

### locale (overrides 'separator')

_*(string || boolean)*_ BCP 47 language tag to specify a locale, or `true` to use default locale, default is `""`

### localeOptions (overrides 'separator', requires string for 'locale' option)

_*(object)*_ Dictionary of options defined by ECMA-402 ([Number.prototype.toLocaleString](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number/toLocaleString)). Requires locale option to be explicitly passed as a string, otherwise is ignored.

### output

_*(string)*_ Output of function (`array`, `exponent`, `object`, or `string`), default is `string`

### round

_*(number)*_ Decimal place, default is `2`

### separator

_*(string)*_ Decimal separator character, default is `.`

### spacer

_*(string)*_ Character between the `result` and `symbol`, default is `" "`

### standard

_*(string)*_ Standard unit of measure, can be `iec` or `jedec`, default is `jedec`; can be overruled by `base`

### symbols

_*(object)*_ Dictionary of SI/JEDEC/IEC symbols to replace for localization, defaults to english if no match is found

### unix

_*(boolean)*_ Enables unix style human readable output, e.g `ls -lh`, default is `false`

## Examples

<!-- prettier-ignore-start -->
```javascript
import { filesize, Options } from "https://deno.land/x/filesize/mod.ts";
filesize(500);                                        // "500 B"
filesize(500, new Options({ bits: true }));           // "4 Kb"
filesize(265318, new Options({ base: 10 }));          // "265.32 kB"
filesize(265318);                                     // "259.1 KB"
filesize(265318, new Options({ round: 0 }));          // "259 KB"
filesize(265318, new Options({ output: "array" }));   // [259.1, "KB"]
filesize(265318, new Options({ output: "object" }));  // {value: 259.1, symbol: "KB", exponent: 1}
filesize(1, new Options({ symbols: { B: "Б" } }));    // "1 Б"
filesize(1024);                                       // "1 KB"
filesize(1024, new Options({ exponent: 0 }));         // "1024 B"
filesize(1024, new Options({ output: "exponent" }));  // 1
filesize(265318, new Options({ standard: "iec" }));   // "259.1 KiB"
filesize(265318, new Options({ standard: "iec", fullform: true })); // "259.1 kibibytes"
filesize(12, new Options({ fullform: true, fullforms: ["байтов"] })); // "12 байтов"
filesize(265318, new Options({ separator: "," }));    // "259,1 KB"
filesize(265318, new Options({ locale: "de" }));      // "259.1 KB"
```
<!-- prettier-ignore-end -->

## Test

`deno test test.ts`

## License

Copyright (c) 2019 Jason Mulligan
Copyright (c) 2020 David Stone

Licensed under the MIT license.
