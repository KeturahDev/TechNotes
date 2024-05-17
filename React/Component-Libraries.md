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
        <Theme>
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
