when wen run the test script in react,jest finds all files ending in .test.js and executes tests inside them

### diffrence between `describe`, `it` and `test`:
`describe(name, fn)` creates a block that groups together several related tests in one "test suite".

`it`(is aliased by `test` so it does the same thing as `it`), this is a unit test itself. Usually you name it something like should do somethingso that it reads as a natural sentence. So you would group multiple `its` under one `describe`.

This gives you a bunch of new options, ifa you want to only run a group of tests, you can write `describe.only` (or `it.only` for a single test). You can add `.skip` instead of `.only` to skip a bunch of tests. Finally you can add `beforeEach/afterEach` hooks to run before or after each test in a describe block.
