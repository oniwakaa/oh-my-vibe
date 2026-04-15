## Testing a Login Flow

```
/playwright Test the login flow on localhost:3000/login

[Agent will:]
1. Navigate to localhost:3000/login
2. Ask for test credentials (via ask_user_question)
3. Fill username and password fields
4. Click login button
5. Wait for navigation
6. Verify redirect to dashboard
7. Take screenshot of logged-in state
```

## Verifying a Form Submission

```
/playwright Verify that the contact form submits successfully

[Agent will:]
1. Navigate to /contact
2. Fill name, email, message fields
3. Click submit
4. Wait for success message
5. Screenshot the success state
```

## Scraping Data from a Page

```
/playwright Extract all product names and prices from /products

[Agent will:]
1. Navigate to /products
2. Use browser_evaluate to extract data
3. Return structured list: [{ name: "...", price: "..." }]
```

## Taking Screenshots for Documentation

```
/playwright Take screenshots of the user settings page for documentation

[Agent will:]
1. Navigate to /settings
2. Screenshot full page
3. Screenshot each tab (Account, Security, Notifications)
4. Save with descriptive names
```

## Testing Responsive Design

```
/playwright Test the homepage at mobile (375px) and desktop (1920px) widths

[Agent will:]
1. Set viewport to 375px width
2. Navigate to homepage
3. Screenshot mobile layout
4. Set viewport to 1920px width
5. Screenshot desktop layout
6. Compare side by side
```

## Checking Dark Mode

```
/playwright Verify dark mode toggle works correctly

[Agent will:]
1. Navigate to page
2. Screenshot light mode
3. Click dark mode toggle
4. Verify CSS variables changed
5. Screenshot dark mode
```

## Debugging Visual Issues

```
/playwright The button at line 42 in src/components/Button.tsx doesn't show hover state

[Agent will:]
1. Locate the button on the page
2. Take screenshot of initial state
3. Hover over the button
4. Take screenshot of hover state
5. Extract computed styles
6. Compare and identify issue
```
