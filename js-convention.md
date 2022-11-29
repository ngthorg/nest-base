# TypeScript Conventional

## Introduce

## Identifiers

| Style           | Category                                                                                 |
| --------------- | ---------------------------------------------------------------------------------------- |
| `PascalCase`    | [class] / [interface] / [type] / [enum] / [namespaces] / [decorator] / [type parameters] |
| `camelCase`     | [variable] / [parameter] / [function] / [method] / [property] / [module] alias           |
| `CONSTANT_CASE` | global [constant] values, including [enum] values                                        |
| `#ident`        | [private] identifiers are never used.                                                    |

- **Abbreviations**: Treat abbreviations like acronyms in names as whole words, i.e. use `loadHttpUrl`, not `loadHTTPURL`, unless required by a platform name (e.g. `XMLHttpRequest`).

- **Dollar sign**: Identifiers should not generally use `$`, except when aligning with naming conventions for third party frameworks. [See below][name] for more on using $ with Observable values.

- **Type parameters**: Type parameters, like in `Array<T>`, may use a single upper case character (`T`) or `PascalCase`.

- **Test names**: Test method names in Closure `testSuites` and similar xUnit-style test frameworks may be structured with `_` separators, e.g. `testX_whenY_doesZ()`.

- **`_` prefix/suffix**: Identifiers must not use `_` as a prefix or suffix.

  This also means that `_` must not be used as an identifier by itself (e.g. to indicate a parameter is unused).

- **Imports**: Module namespace imports are `camelCase` while files are `snake_case`, which means that imports correctly will not match in casing style, such as

  ```ts
  import fooBar from './foo_bar';
  ```

Naming

- Use pronounceable variable names

  > Distinguish names in such a way that the reader knows what the differences offer.

  ![Bad][bad]

  ```ts
  function isBetween(a1: number, a2: number, a3: number): boolean {
    return a2 <= a1 && a1 <= a3;
  }
  ```

  ![Good][good]

  ```ts
  function isBetween(value: number, left: number, right: number): boolean {
    return left <= value && value <= right;
  }
  ```

- Use pronounceable variable names

  > If you can't pronounce it, you can't discuss it without sounding weird.

  ![Bad][bad]

  ```ts
  class Subs {
    ccId: number;
    billingAddrId: number;
    shippingAddrId: number;
  }
  ```

  ![Good][good]

  ```ts
  class Subscription {
    creditCardId: number;
    billingAddressId: number;
    shippingAddressId: number;
  }
  ```

- Don't add unneeded context

  > If your class/type/object name tells you something, don't repeat that in your variable name.

  ![Bad][bad]

  ```ts
  type Car = {
    carMake: string;
    carModel: string;
    carColor: string;
  };
  ```

  ![Good][good]

  ```ts
  type Car = {
    make: string;
    model: string;
    color: string;
  };
  ```

Naming Booleans

- Don't use negative names for boolean variables.

  ![Bad][bad]

  ```ts
  const isNotEnabled = true;
  ```

  ![Good][good]

  ```ts
  const isEnabled = false;
  ```

- A prefix like `is`, `are`, `or` has helps every developer to distinguish a boolean from another variable by just looking at it

  ![Bad][bad]

  ```ts
  const enabled = false;
  ```

  ![Good][good]

  ```ts
  const isEnabled = false;
  ```

### Variable and Function

- Use `camelCase` for variable and function names

  ![Bad][bad]

  ```ts
  var FooVar;
  function BarFunc() {}
  ```

  ![Good][good]

  ```ts
  var fooVar;
  function barFunc() {}
  ```

### Class

- Use `PascalCase` for class names.

  ![Bad][bad]

  ```ts
  class foo {}
  ```

  ![Good][good]

  ```ts
  class Foo {}
  ```

- Use `camelCase` of class members and methods

  > Reason: Naturally follows from variable and function naming convention.

  ![Bad][bad]

  ```ts
  class Foo {
    Bar: number;
    Baz() {}
  }
  ```

  ![Good][good]

  ```ts
  class Foo {
    bar: number;
    baz() {}
  }
  ```

### Interface

- Use `PascalCase` for name.

  > Reason: Similar to [class]

- Use `camelCase` for members.

  > Reason: Similar to [class]

- Don't prefix with `I`

  > Reason: Unconventional. `lib.d.ts` defines important interfaces without an I (e.g. `Window`, `Document` etc).

  ![Bad][bad]

  ```ts
  interface IFoo {}
  ```

  ![Good][good]

  ```ts
  interface Foo {}
  ```

### Type

- Use `PascalCase` for name.

  > Reason: Similar to [class]

- Use `camelCase` for members.

  > Reason: Similar to [class]

### Namespaces

- Use `PascalCase` for names

  > Reason: Convention followed by the TypeScript team. [Namespaces] are effectively just a [class] with static members. [Class] names are `PascalCase` => Namespace names are `PascalCase`

  ![Bad][bad]

  ```ts
  namespace IFoo {}
  ```

  ![Good][good]

  ```ts
  namespace Foo {}
  ```

### Enum

- Use `PascalCase` for enum names

  ![Bad][bad]

  ```ts
  enum color {}
  ```

  ![Good][good]

  ```ts
  enum Color {}
  ```

- Use `CONSTANT_CASE` for enum member

  ![Bad][bad]

  ```ts
  enum color {
    red = 'red',
    gray_dark = '#273444',
    grayLight = '#d3dce6',
  }
  ```

  ![Good][good]

  ```ts
  enum Color {
    RED = 'red',
    GRAY_DARK = '#273444',
    GRAY_LIGHT = '#d3dce6',
  }
  ```

### Null vs. Undefined

- Prefer not to use either for explicit unavailability

  > Reason: these values are commonly used to keep a consistent structure between values. In TypeScript you use types to denote the structure

  ![Bad][bad]

  ```ts
  type Foo = { x: number; y?: number };
  const foo: Foo = { x: 123, y: undefined };
  ```

  ![Good][good]

  ```ts
  type Foo = { x: number; y?: number };
  const foo: Foo = { x: 123 };
  ```

- Use truthy check for **objects** being `null` or `undefined`

  ![Bad][bad]

  ```ts
  if (error === null)
  ```

  ![Good][good]

  ```ts
  if (error)
  ```

- Use `== null` / `!= null` (not `===` / `!==`) to check for `null` / `undefined` on primitives as it works for both `null`/`undefined` but not other falsy values (like `''`, `0`, `false`) e.g.

  ![Bad][bad]

  ```ts
  if (error !== null) // does not rule out undefined
  ```

  ![Good][good]

  ```ts
  if (error != null) // rules out both null and undefined
  ```

### Quotes

- Prefer single quotes (') unless escaping.

  > Reason: More JavaScript teams do this (e.g. `airbnb`, `standard`, `npm`, `node`, `google/angular`, `facebook/react`). It's easier to type (no shift needed on most keyboards). `Prettier` team recommends single quotes as well

  > Double quotes are not without merit: Allows easier copy paste of objects into JSON. Allows people to use other languages to work without changing their quote character. Allows you to use apostrophes e.g. He's not going.. But I'd rather not deviate from where the JS Community is fairly decided.

- When you can't use double quotes, try using back ticks (`).
  > Reason: These generally represent the intent of complex enough strings.

### Spaces

- Use 2 spaces. Not tabs.
  > Reason: More JavaScript teams do this (e.g. `airbnb`, `idiomatic`, `standard`, `npm`, `node`, `google/angular`, `facebook/react`). The TypeScript/VSCode teams use 4 spaces but are definitely the exception in the ecosystem.

### Semicolons

- Use semicolons.

### Array

- Annotate arrays as foos: `Foo[]` instead of foos: `Array<Foo>`.
  > Reasons: It's easier to read. It's used by the TypeScript team. Makes easier to know something is an array as the mind is trained to detect `[]`.

### Filename

- Name files with `camelCase`. E.g. `utils.ts`, `map.ts` etc.
  > Reason: Conventional across many JS teams.
- When the file exports a component and your framework (like React) wants component to be PascalCased, use pascal case file name to match e.g. `Accordion.tsx`, `MyControl.tsx`.
  > Reason: Helps with consistency (little overthought required) and its what the ecosystem is doing.

type vs. interface

- Use type when you might need a union or intersection:

  ```ts
  type Foo = number | { someProperty: number };
  ```

- Use interface when you want extends or implements e.g.

  ```ts
  interface Foo {
    foo: string;
  }
  interface FooBar extends Foo {
    bar: string;
  }
  class X implements FooBar {
    foo: string;
    bar: string;
  }
  ```

- Otherwise use whatever makes you happy that day. I use [type]

`==` or `===`

- Both are mostly safe for TypeScript users. I use `===` as that is what is used in the TypeScript codebase.

[class]: #class 'Class'
[interface]: #interface 'Interface'
[type]: #type 'Type'
[enum]: #enum 'Enum'
[namespaces]: #enum 'Namespaces'
[decorator]: #decorator 'Decorator'
[type parameters]: #type-parameters 'Type Parameters'
[variable]: #variable-and-function 'Variable'
[parameter]: #decorator 'Parameter'
[function]: #variable-and-function 'Function'
[method]: #decorator 'Method'
[property]: #decorator 'Property'
[module]: #decorator 'Module'
[constant]: #decorator 'Constant'
[private]: #decorator 'Private'

<!-- sub -->

[name]: #decorator 'Private'

<!-- badges -->

[bad]: https://img.shields.io/static/v1?label=&message=Bad&color=red
[good]: https://img.shields.io/static/v1?label=&message=Good&color=green
