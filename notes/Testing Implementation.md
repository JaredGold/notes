# Testing Implementation
```js
// this fn actually hits the DB. it also has a side effect of tracking an event (ex. writing to a log).
async function getNumbersFromDB() {
  let result = null

  try {
     result = await mySQL.getNumbers()

  } catch (err) {
    console.log(err)
  } finally {
    // side effect
    events.trackEvent('fetched numbers')
  }

  return result;
}

// this fn adds the numbers. code under test. it pulls data from a fn that wraps the db call.
async function addNumbersFromDB() {
  const [x, y] = await data.getNumbersFromDB()

  return x + y;
}

// unit test
test('adds numbers from db', async  () => {
  // 1. mock direct dependencies - we want to test the code we've written, not external code
  const getNumbersSpy = jest.spyOn(data, 'getNumbersFromDB').mockImplementation(() => [2, 5]);

  const result = await addNumbersFromDB();

  expect(result).toBe(7)

  // restore spys/mocks to actual code
  getNumbersSpy.mockRestore()
});

// integration test
test('adds numbers from db', async  () => {
  // 1. we can still mock dependencies - but we may not mock direct dependencies. in this case, we probably don't want to
  // actually hit a database (slow, extra setup) - but we might want to hit `getNumbersFromDB`.
  const trackEventSpy = jest.spyOn(events, 'trackEvent');
  const getNumbersFromDBSpy = jest.spyOn(mySQL, 'getNumbersFromDB').mockImplementation(() => [2, 5]);

  const result = await addNumbersFromDB();

  expect(result).toBe(7)

  // cleanup
  trackEventSpy.mockRestore()
  getNumbersFromDBSpy.mockRestore()
});

// e2e test
test('adds numbers from db', async  () => {
  // initialize an in-memory DB (or disk, or w/e). at this point, we're not mocking anything.
  const db = await memoryDB.initialize('localhost:8083')

  // add test data to DB
  await db.addNumbers([2, 5])

  // or, we still might want to mock out our logging because it's not relevant & one more hting to setup
  const trackEventSpy = jest.spyOn(events, 'trackEvent');

  const result = await addNumbersFromDB();

  expect(result).toBe(7)

  // cleanup
  db.shutdown()
  trackEventSpy.mockRestore()
});
```