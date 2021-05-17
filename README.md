<div align="center">
  <h1>
    <br/>
    🥵
    <br />
    @choc-ui/chakra-autocomplete
    <br />
    <br />
  </h1>
  <sup>
    <br />
    <br />
    <a href="https://www.npmjs.com/package/@choc-ui/chakra-autocomplete?style=for-the-badge">
       <img src="https://img.shields.io/npm/v/@choc-ui/chakra-autocomplete.svg?style=for-the-badge" alt="npm package" />
    </a>
    <a href="https://www.npmjs.com/package/@choc-ui/chakra-autocomplete?style=for-the-badge">
      <img src="https://img.shields.io/npm/dw/@choc-ui/chakra-autocomplete.svg?style=for-the-badge" alt="npm  downloads" />
    </a>
<a>
    <img alt="NPM" src="https://img.shields.io/npm/l/@choc-ui/chakra-autocomplete?style=for-the-badge">
</a>

<a><img alt="GitHub Repo stars" src="https://img.shields.io/github/stars/anubra266/choc-autocomplete?logo=github&style=for-the-badge">

</a>
    <br />
    AutoComplete Component for the <a href="https://chakra-ui.com">Chakra UI</a> Library.</em>
    
  </sup>
  <br />
  <br />
  <br />
  <br />
  <pre>npm i <a href="https://www.npmjs.com/package/@choc-ui/chakra-autocomplete">@choc-ui/chakra-autocomplete</a></pre>
  <br />
  <br />
  <br />
  <br />
  <br />
</div>

## Install

```bash
npm i --save @choc-ui/chakra-autocomplete
#or
yarn add @choc-ui/chakra-autocomplete
```

## Preview

### With Mouse

![](example/images/mousePreview.gif)

### With Keyboard

![](example/images/keyboardPreview.gif)

## Demo [on Codesandbox](https://codesandbox.io/s/chakra-autocomplete-demo-elurs)

## Usage

### Basic Usage

```js
import {
  AutoComplete,
  AutoCompleteInput,
  AutoCompleteItem,
  AutoCompleteList,
} from '@choc-ui/chakra-autocomplete';

export default () => {
  const options = ['apple', 'appoint', 'zap', 'cap', 'japan'];

  return (
    <AutoComplete>
      <AutoCompleteInput
        variant="filled"
        placeholder="Search..."
        defaultValue="ap"
        autoFocus
      />
      <AutoCompleteList rollNavigation>
        {options.map((option, oid) => (
          <AutoCompleteItem
            key={`option-${oid}`}
            value={option}
            textTransform="capitalize"
          >
            {option}
          </AutoCompleteItem>
        ))}
      </AutoCompleteList>
    </AutoComplete>
  );
};
```

![](example/images/basic.jpg)

---

### Creating Groups

> You can create groups with the `AutoCompleteGroup` Component

```js
import {
  AutoComplete,
  AutoCompleteGroup,
  AutoCompleteInput,
  AutoCompleteItem,
  AutoCompleteList,
} from '@choc-ui/chakra-autocomplete';

export default () => {
  const fruits = ['Apple', 'Grape', 'Pawpaw'];
  const countries = ['Korea', 'Nigeria', 'India'];

  return (
    <AutoComplete>
      <AutoCompleteInput
        variant="filled"
        placeholder="Search..."
        pl="10"
        defaultValue="ap"
        autoFocus
      />
      <AutoCompleteList rollNavigation>
        <AutoCompleteGroup title="Fruits" showDivider>
          {fruits.map((option, oid) => (
            <AutoCompleteItem
              key={`fruits-${oid}`}
              value={option}
              textTransform="capitalize"
            >
              {option}
            </AutoCompleteItem>
          ))}
        </AutoCompleteGroup>
        <AutoCompleteGroup title="countries" showDivider>
          {countries.map((option, oid) => (
            <AutoCompleteItem
              key={`countries-${oid}`}
              value={option}
              textTransform="capitalize"
            >
              {option}
            </AutoCompleteItem>
          ))}
        </AutoCompleteGroup>
      </AutoCompleteList>
    </AutoComplete>
  );
};
```

![](example/images/group.jpg)

---

## Accessing the internal state

> To access the internal state of the `AutoComplete`, use a function as children (commonly known as a render prop). You'll get access to the internal state `isOpen` and method `onClose`.

```js
import {
  AutoComplete,
  AutoCompleteInput,
  AutoCompleteItem,
  AutoCompleteList,
} from '@choc-ui/chakra-autocomplete';
import { ChevronDownIcon, ChevronRightIcon } from '@chakra-ui/icons';
import { Icon, InputGroup, InputRightElement } from '@chakra-ui/react';

export default () => {
  const options = ['apple', 'appoint', 'zap', 'cap', 'japan'];

  return (
    <AutoComplete>
      {({ isOpen }) => (
        <>
          <InputGroup>
            <AutoCompleteInput variant="filled" placeholder="Search..." />
            <InputRightElement
              children={
                <Icon as={isOpen ? ChevronRightIcon : ChevronDownIcon} />
              }
            />
          </InputGroup>
          <AutoCompleteList rollNavigation>
            {options.map((option, oid) => (
              <AutoCompleteItem
                key={`optio-${oid}`}
                value={option}
                textTransform="capitalize"
                align="center"
              >
                {option}
              </AutoCompleteItem>
            ))}
          </AutoCompleteList>
        </>
      )}
    </AutoComplete>
  );
};
```

Watch the **Icon** on the **right**.

![](example/images/internalState.gif)

---

## Custom Rendering

> You can Render whatever you want. The `AutoComplete` Items are regular `Chakra` Boxes.

```js
import {
  AutoComplete,
  AutoCompleteInput,
  AutoCompleteItem,
  AutoCompleteList,
} from '@choc-ui/chakra-autocomplete';
import { Avatar, Box, Text } from '@chakra-ui/react';

export default () => {
  const people = [
    { name: 'Dan Abramov', image: 'https://bit.ly/dan-abramov' },
    { name: 'Kent Dodds', image: 'https://bit.ly/kent-c-dodds' },
    { name: 'Segun Adebayo', image: 'https://bit.ly/sage-adebayo' },
    { name: 'Prosper Otemuyiwa', image: 'https://bit.ly/prosper-baba' },
    { name: 'Ryan Florence', image: 'https://bit.ly/ryan-florence' },
  ];

  return (
    <AutoComplete>
      <AutoCompleteInput
        variant="filled"
        placeholder="Search..."
        pl="10"
        defaultValue="ap"
        autoFocus
      />
      <AutoCompleteList rollNavigation>
        {people.map((person, oid) => (
          <AutoCompleteItem
            key={`option-${oid}`}
            value={person.name}
            textTransform="capitalize"
            align="center"
          >
            <Avatar size="sm" name={person.name} src={person.image} />
            <Text ml="4">{person.name}</Text>
          </AutoCompleteItem>
        ))}
      </AutoCompleteList>
    </AutoComplete>
  );
};
```

![](example/images/render.jpg)

---

## Multiple Selection

> Add an `AutoCompleteTags` Component to enable multiple selections.

## API Reference

**NB**: Feel free to request any additional `Prop` in [Issues](https://github.com/anubra266/choc-autocomplete/issues/new/).

### **AutoComplete**

Wrapper and Provider for `AutoCompleteInput` and `AutoCompleteList`

**AutoComplete** composes [**Box**](https://chakra-ui.com/docs/layout/box) so you can pass all Box props to change its style.

**NB**: If you have more than one `AutoComplete` Component on a page, they must be assigned unique `id`s

---

`onChange`

---

**Description**

> Function that provides current Input value and is called anytime, suggestion is selected- useful for uncontrolled Input, but wants to use Value

**Type**

```ts
(value: string) => void
```

**Default**

`null`

**Required**

No

---

`onSelectOption`

---

**Description**

> Will be called every time suggestion is selected via mouse or keyboard. It returns the `selectedValue`, the`selectionMethod` and a boolean specifying if the `input` is a new one; useFul when combined `creatable` mode.

**Type**

```ts
(optionValue: string, selectMethod: 'click'|'keyboard', isNewInput: boolean) => void;
```

**Default**

`null`

**Required**

No

---

`onOptionHighlight`

---

**Description**

> Will be called every time the highlighted option changes.

**Type**

```ts
(optionValue: string) => void
```

**Default**

`null`

**Required**

No

---

`defaultValue`

---

**Description**

> The default value of the autocomplete input.

**Type**

```ts
string;
```

**Default**

`''`

**Required**

No

---

`creatable`

---

**Description**

> Allows user to add new Input, when no suggestions matches the input.

**Type**

```ts
boolean;
```

**Default**

`false`

**Required**

No

---

`emphasize`

---

**Description**

> The parts of the option string that match the `AutoCompleteInput` value are emphasized. Pass boolean to bolden it, or a Chakra `CSSObject` for custom styling.
> e.g.

```html
<AutoComplete emphasize>
  ...
</AutoComplete>

<!--Or-->

<AutoComplete emphasize={{ color: 'blue.400', fontWeight: 'bold' }}>
  ...
</AutoComplete>
```

![](example/images/emphasize.gif)

**Type**

```ts
boolean | CSSObject;
```

**Default**

```ts
const emphasizeStyles = {
  fontWeight: 'extrabold',
};
```

**Required**

No

---

`shouldRenderSuggestions`

---

**Description**

> By default, suggestions are rendered when the input isn't blank. Feel free to override this behaviour. This function gets the current value of the input

> **e.g.** The following function is to show the suggestions only if the input has more than **two** characters.

```ts
function shouldRenderSuggestions(value) {
  return value.trim().length > 2;
}
```

**Type**

```ts
(value: string) => void
```

**Default**

`null`

**Required**

No

---

`focusInputOnSelect`

---

**Description**

> Determines if Input should be focused after Select

**Type**

```ts
boolean;
```

**Default**

`true`

**Required**

No

---

`closeOnSelect`

---

**Description**

> If true, the menu will close when an item is selected, by mouse or keyboard.

**Type**

```ts
boolean;
```

**Default**

`true`

**Required**

No

---

`closeOnBlur`

---

**Description**

> If true, the menu will close when the `AutoComplete` Component loses focus.

**Type**

```ts
boolean;
```

**Default**

`true`

**Required**

No

---

`suggestWhenEmpty`

---

**Description**

> If the suggestions shoud show when the input is Empty. - It is used when the input is focused.

**Type**

```ts
boolean;
```

**Default**

`false`

**Required**

No

---

`suggestWhenEmpty`

---

**Description**

> Component to render when no match is found. Pass null, to just close the menu.

**Type**

```ts
ReactNode;
```

**Default**

`null`

**Required**

No

### **AutoCompleteInput**

Input for `AutoComplete` value.

**AutoComplete** composes [**Input**](https://chakra-ui.com/docs/form/input) so you can pass all Input props to change its style.

---

`selectOnFocus`

---

**Description**

> Determines if input's text is selected, when the input is focused.

**Type**

```ts
boolean;
```

**Default**

`false`

**Required**

No

### **AutoCompleteList**

Wrapper for `AutoCompleteGroup` and `AutoCompleteItem`

**AutoCompleteList** composes [**Box**](https://chakra-ui.com/docs/layout/box) so you can pass all Box props to change its style.

---

`rollNavigation`

---

**Description**

> Determines if keyboard navigation should roll over after getting to either ends.

**Type**

```ts
boolean;
```

**Default**

`false`

**Required**

No

![](example/images/rollNavigation.gif)

### **AutoCompleteGroup**

Wrapper for collections of `AutoCompleteItem`s

**AutoComplete** composes [**Box**](https://chakra-ui.com/docs/layout/box) so you can pass all Box props to change its style.

---

`showDivider`

---

**Description**

> Determines if a divider should be rendered above the group. The **divider** will automatically be unrendered when that group is first in that suggestions.

**Type**

```ts
boolean;
```

**Default**

`null`

**Required**

No

![](example/images/divider.gif)

---

`dividerColor`

---

**Description**

> Color for the group divider, when `showDivider` is `true`

**Type**

```ts
string;
```

**Default**

`inherit`

**Required**

No

---

`titleStyles`

---

**Description**

> Styles to be applied to group's `title`. It Composes [**Text**](https://chakra-ui.com/docs/layout/box) so you can pass all Text props to change its style.

**Type**

```ts
TextProps;
```

**Default**

```ts
const textStyles: TextProps = {
  fontSize: 'xs',
  textTransform: 'uppercase',
  fontWeight: 'extrabold',
  letterSpacing: 'wider',
  ml: '5',
};
```

**Required**

No

### **AutoCompleteItem**

This Composes your suggestions

**AutoComplete** composes [**Flex**](https://chakra-ui.com/docs/layout/flex) so you can pass all Flex props to change its style.

---

`_focus`

---

**Description**

> Like the default pseudo `_focus`, but this determines the style applied when that `Item` highlighted by mouse or keyboard,

**Type**

```ts
CSSObject;
```

**Default**

```ts
const _focus = {
  bg: useColorModeValue('gray.200', 'whiteAlpha.100'),
};
```

**Required**

No
