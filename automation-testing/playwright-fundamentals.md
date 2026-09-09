# Playwright Fundamentals

## 1. Basic Test Structure

```ts
import { test, expect } from @playwright/test;

test('Open Playwright website', async ({page}) => {
    await page.goto('https://playwright.dev');

    await expect(page).toHaveTitle(/Playwright/);
});
```

### `import`

Imports functionality from another module.

```ts
import { test, expect } from @playwright/test;
```

- `test` → creates test cases
- `expect` → creates assertions

---

### `test()`

Defines a test case.

```ts
test('test name', async ({ page }) => {
    // test steps
});
```

Structure:

```ts
test(
    test name,
    async ({ page }) => {
        test steps
    }
)
```

---

### `async`

Marks a function as asynchronous so `await` can be used inside it.

```ts
async ({ page }) => {
    await page.goto(url);
}
```

---

### `await`

Waits for an asynchronous operation to complete before continuing.

```ts
await page.goto(url);
await page.click();
```

Mental model:

```text
Do operation
     ↓
Wait for it
     ↓
  Continue
```

---

### `page`

Represents the browser page/tab controlled by Playwright.

Common examples:

```ts
await page.goto(url);
await page.getByRole('button').click();
await page.getByLabel('Username').fill('Amir');
```

---

## 2. Actions vs Assertions

### Actions

Actions tells the browser to do something.

```ts
await page.goto(url);
await locator.fill('text');
await locator.click();
```

Common actions:

```ts
page.goto()
locator.click()
locator.fill()
locator.press()
locator.check()
locator.selectOption()
```

### Assertions

Assertions verify that the application behaves as expected.

```ts
await expect(locator).toBeVisible();
await expect(locator).toHaveText('Dashboard');
```

Mental model:

```text
    ACTION
      ↓
 Do Something
      ↓
  ASSERTION
      ↓
Verify Result
```

---

## 3. `expect()`

Used to define what the test expects to be true.

```ts
await expect(page).toHaveTitle(/Playwright/);
```

Common assertions:

```ts
await expect(locator).toBeVisible();
await expect(locator).toBeHidden();
await expect(locator).toHaveText('Hello');
await expect(locator).toContainText('Hello');
await expect(locator).toHaveValue('Amir');
await expect(locator).toBeEnabled();
await expect(locator).toBeDisabled();

await expect(page).toHaveTitle(/Dashboard/);
await expect(page).toHaveURL(/dashboard/);
```

Prefer Playwright's web-first assertions:

```ts
await expect(locator).toBeVisible();
```

instead of manually checking:

```ts
expect(await locator.isVisible()).toBe(true);
```

> Playwright assertions can automatically wait/retry for the expected condition.

---

## 4. Locators

A **locator** tells Playwright how to find an alement on the page.

Example:

```ts
const loginButton = page.getByRole('button', { name: 'login' });

await loginButton.click();
```

A locator does not perform the action itself.

```text
        Locator
           ↓
Finds/represents an element
           ↓
         Action
           ↓
click / fill / check / etc.
```

---

## 5. `getByRole()`

Finds elements based on their accessible role.

```ts
page.getByRole('button', { name: 'Login' });
```

Examples:

```ts
page.getByRole('button', { name: 'Login' });
page.getByRole('textbox', { name: 'Username' });
page.getByRole('link', { name: 'Home' });
page.getByRole('checkbox', { name: 'Remember me' });
page.getByRole('heading', { name: 'Dashboard' });
```

Common roles:

```text
button
textbox
link
checkbox
radio
heading
combobox
```

Prefer user-facing locators such as roles when appropriate.

---

## 6. `getByLabel`

Finds form controls using their associated label.

Example HTML:

```html
<label for="username">Username</label>
<input id="username">
```

PLaywright:

```ts
await page.getByLabel('Username').fill('Amir');
```

Another Example:

```ts
await page.getByLabel('Password').fill('password123');
```

Useful for:

```text
Username
Password
Email
Phone Number
Address
etc.
```

---

## 7. `getByText()`

Finds an element based on visible text.

```ts
await page.getByText('Dashboard').click();
```

Example assertion:

```ts
await expect(page.getByText('Dashboard')).toBeVisible();
```

---

## 8. `locator()`

A more general locator method.

```ts
page.locator('input');
```

CSS selector:

```ts
page.locator('#username');
```

Class:

```ts
page.locator('.login-button');
```

Attribute:

```ts
page.locator('[data-testid="login-button"]');
```

Use specific, stable selectors where necessary.

When possible, prefer user-facing locators:

```ts
getByRole()
getByLabel()
getByText()
```

---

## 9. Filling Input Fields

Use `.fill()` to enter text.

```ts
await page.getByLabel('Username').fill('Amir');
await page.getByLabel('Password').fill('password123');
```

General pattern:

```ts
await locator.fill('value');
```

Example:

```ts
const username = page.getByLabel('Username');

await username.fill('Amir');
```

---

## 10. Clicking Elements

Use `.click()`.

```ts
await page.getByLabel('button', { name: 'Login' }).click();
```

General pattern:

```ts
await locator.click();
```

---

## 11. Example: Simple Login Flow

```ts
import { text, expect } from '@playwright/test';

test('User can login', sync ({ page }) => {
    await page.goto('https://example.com/login');

    await page.getByLabel('Username').fill('Amir');
    await page.getByLabel('Password').fill('password123');

    await page.getByRole('button', {name: 'Login' }).click();

    await expect(page.getByText('Dashboard')).toBeVisible();
});
```

Flow:

```text
    Open login page
            ↓
    Find username field
            ↓
      Fill username
            ↓
    Find password field
            ↓
      Fill password
            ↓
    Find login button
            ↓
          Click
            ↓
      Find Dashboard
            ↓
Verify Dashboard is visible
```

---

## 12. Test Anatomy

A typical Playwright test can bbe thought of as:

```text
  SETUP
    ↓
  ACTION
    ↓
  ACTION
    ↓
  ACTION
    ↓
 ASSERTION
 ```

 Example:

 ```ts
 test('login', async ({ page }) => {
    // Setup / navigation
    await page.goto('/login');

    // Actions
    await page.getByLabel('Username').fill('Amir');
    await page.getByLabel('Password').fill('password123');
    await page.getByRole('button', { name: 'Login' }).click();

    // Assertion
    await expect(page.getBYText('Dashboard')).toBeVisible();
 });
 ```

 ---

 ## 13. Multiple Tests

 A test file can contain multiple tests.

 ```ts
 import { test, expect } from '@playwright/test';

 test('homepage loads', async ({ page }) => {
    await page.goto('https://example.com');

    await expect(page).toHaveTitle(/Example/);
 });

 test('login button is visible', async ({ page }) => {
    await page.goto('https://example.com');

    awat expect(page.getByRole('button', { name: 'Login' })).toBeVisible();
 });
```

Each test should ideally be independent.

---

## 14. Running Tests

Run all Playwright tests:

```node
npx playwright test
```

Run tests with browser visible:

```node
npx playwright test --headed
```

Run using Playwright UI Mode:

```node
npx playwright test --ui
```

Run a specific test file:

```node
npx playwright test tests/example.spec.ts
```

---

## 15. Useful Mental Model

When writing Playwright automation, think:

```text
1. What page am I on?
            ↓
2. What element do I need?
            ↓
3. How can I locate it?
            ↓
4. What action should I perform?
            ↓
5. What should happen?
            ↓
6. How do I assert the result?
```

Example:

```text
    Login page
        ↓
  Username field
        ↓
getByLabel('Username')    
        ↓
    fill('Amir')
        ↓
Username contains Amir
        ↓
expect(...).toHaveValue('Amir')
```

---

## 16. Core Syntax to Remember

```ts
// Define a test
test('test name', async ({ page }) => {
    // Navigate
    await page.goto('https://example.com');

    // Locate + interact
    await page.getByLabel('Username').fill('Amir');
    await page.getByRole('button', { name: 'Login' }).click();

    // Assert
    await expect(page.getByText('Dashboard')).toBeVisible();
});
```

## Quick Reference

| **Syntax** | **Purpose** |
|---|---|
| `test()` | Define a test |
| `expect()` | Define an assertion |
| `async` | Allow asynchronous operations |
| `await` | Wait for an async operation |
| `page` | Browser page/tab |
| `page.goto()` | Navigate to URL |
| `getByRole()` | Locate by accessible role |
| `getByLabel()` | Locate form control by label |
| `getByText()` | Locate by visible text |
| `locator()` | General locator |
| `.fill()` | Enter text |
| `.click()` | Click element |
| `.check()` | Check checkbox/radio |
| `selectOption()` | Select dropdown option |
| `toBeVisible()` | Assert element is visible |
| `toHaveText()` | Assert element text |
| `toHaveValue()` | Assert input value |
| `toHaveTitle()` | Assert page title |
| `toHaveURL()` | Assert page URL |

---
