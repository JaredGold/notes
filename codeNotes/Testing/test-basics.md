# Testing

#### When all else fails...

Click [here](https://testing-library.com/docs/queries/about/)

## 3 queries (find, get, query)
- find - async = will wait for element to appear - will throw if not found
- get - sync = expects the element to be there - will throw if not found
- query - sync = returns null if element is not found

```
// ideal as it's searching for the element based on accessibility properties and the
// API is very flexible. the 2nd arg can take all sorts of other properties to filter
// queried elements on diff things ex. checked or unchecked checkboxes, hidden elements, etc.
getByRole('button', { name : 'Click Me' }) 

// these are 2nd best, in no specific order. p straight forward - specificity is king.
// narrowing our results by label, placeholder text, etc. is ideal.
getByAltText('Some Image')
getByLabelText('Click Me');
getByPlaceholderText('Some Input')
getByDisplayValue('Some Input')
getByTitle('some title')

// runner up, staple.  `ByText` is still fine - but if you really want to take your
// code to the next level, consider using the queries above
getByText('Click Me');

// this is ok - don't sweat it - but a good rule of thumb is that it should only be
// used where the others can't be. test IDs can be flakey and don't really tell
// a good story. they can be useful for testing things like container elements
// and small arbritrary elements ex. a loading spinner, however take note that
// `getByTitle` can be used in cases of an SVG image with a `title` element.
getByTestId('some-component')
```