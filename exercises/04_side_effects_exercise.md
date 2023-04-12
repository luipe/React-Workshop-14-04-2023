## Exercise 4 - Cat pics!

**Goal:** Cute kittens, we want to have them, what do you need to know more?

### Task
Instead of a boring text, memory cards should show cute cats.

Images can be rendered in HTML as `img` tag with image URL.
Example: `<img src="https://cataas.com/cat/A55LPR38NHRPPQhU" />`

We can retrieve image URLs of cats from https://cataas.com
- API documentation: https://cataas.com/doc.html
- `https://cataas.com/cat?json=true`
- returns a JSON object with a `"url"` property, e.g. `"cat/A55LPR38NHRPPQhU"`
- _Optional_: explore further query parameters and tag options (e.g. `cute`) of the API


<details>
    <summary>Hint: asynchronous fetching method</summary>

```tsx
const catProviderUrl = "https://cataas.com";

async function fetchCatUrl(): Promise<string> {
  const rawResponse = await fetch(`${catProviderUrl}/cat?json=true`);
  const jsonResponse = await rawResponse.json();
  return catProviderUrl + jsonResponse.url;
}
```
</details>