# Component Library Options for React

Keturah Smith, May 2024

## Radix UI

A Next JS library.

### Set up:

- install at root of project: `npm install @radix-ui/themes`
- import global CSS file at the root of the app: `import '@radix-ui/themes/styles.css'`
- Wrap the children of body in theme:

```js
import { Theme } from "@radix-ui/themes";

export default function () {
  return (
    <html>
      <body>
        <Theme
          accentColor="crimson"
          grayColor="sand"
          radius="large"
          scaling="95%"
        >
          <MyApp />
        </Theme>
      </body>
    </html>
  );
}
```

- Use components in app

```js
import { Flex, Text, Button } from "@radix-ui/themes";

export default function MyApp() {
  return (
    <Flex direction="column" gap="2">
      <Text>Hello from Radix Themes :)</Text>
      <Button>Let's go</Button>
    </Flex>
  );
}
```

<!-- ### Projects Used:

- []() -->

## Daisy UI

A tailwind CSS component library.

### Set up:

- install at root of project: `npm i -D daisyui@latest`
- Add daisy UI to tailwind.config.js:

```js
module.exports = {
  //...
  plugins: [require("daisyui")],
};
```

- To implement themes:

```js
plugins: [require("daisyui")],
  daisyui: {
    themes: ["forest", "winter", "emerald"],
  },
```

- Use components in app by using keywords in tailwind:

```js
<button className="btn btn-info">Info</button>
<button className="btn btn-success">Success</button>
<button className="btn btn-warning">Warning</button>
<button className="btn btn-error">Error</button>
```
