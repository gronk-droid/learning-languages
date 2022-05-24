# Requests in JS

## Using the `fetch()` function:

#### `GET` Request

<div style="margin: auto; width: 100%; background-color: #2d2a2e">

![](assets/fetch-post.svg)
</div>

```js{highlight=14-25}
// Information to reach API
const url = 'https://api.datamuse.com/words?sl=';

// Selects page elements
const inputField = document.querySelector('#input');
const submit = document.querySelector('#submit');
const responseField = document.querySelector('#responseField');

// Asynchronous function
const getSuggestions = () => {
  const wordQuery = inputField.value;
  const endpoint = `${url}${wordQuery}`;

  fetch(endpoint, {cache: 'no-cache'}).then(response => {
    if (response.ok) {
      return response.json();
    }
    throw new Error('Request failed!');
  }, networkError => {
    console.log(networkError.message)
  }).then(jsonResponse => {
    // renderRawResponse(jsonResponse)
    renderResponse(jsonResponse)
  })
}
```

#### `POST` Request

<div style="margin: auto; width: 100%; background-color: #2d2a2e">

![](assets/fetch-post.svg)
</div>

```js{highlight=11-31}
// Information to reach API
const apiKey = process.env.REBRANDLY_API_KEY;
const url = 'https://api.rebrandly.com/v1/links';

// Some page elements
const inputField = document.querySelector('#input');
const shortenButton = document.querySelector('#shorten');
const responseField = document.querySelector('#responseField');

// Asynchronous functions
const shortenUrl = () => {
  const urlToShorten = inputField.value;
  const data = JSON.stringify({destination: urlToShorten});

	fetch(url, {
    method: 'POST',
    headers: {
      'Content-type': 'application/json',
      'apikey': apiKey
    },
    body: data
  }).then(response => {
    if (response.ok) {
      return response.json()
    }
    throw new Error('Request failed!')
  }, networkError => {console.log(networkError.message)})
  .then(jsonResponse => {
    renderResponse(jsonResponse)
  })
}
```
