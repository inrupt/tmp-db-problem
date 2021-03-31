# tmp-db-problem

Tiny demonstration of Digital Bazaar library problem.

Running `node index.js` works fine, output is:
```script
[tmp-db-problem]$ node index.js 
Key: [{
  "type": "Ed25519VerificationKey2020",
  "publicKeyMultibase": "z7JUiLLxWQ9ZjKD92maKfVkt5WdsMCoFBCMHthdNb584u",
  "privateKeyMultibase": "z4jf6XS9YjRVghhkv7UttdNvwAvQcP8qUmrUvBcfnt39jDooQQKvMceWXiytyoQhmJL3sDKxMgdGnwC5Qq3XPgQSZ"
}]
[tmp-db-problem]$
```

...but running `npm test`, the output is:

```script
[tmp-db-problem]$ npm test

> tmp-db-problem@1.0.0 test
> jest

 FAIL  ./simple.test.js
  verificationKey
    ✕ generates a key (2 ms)

  ● verificationKey › generates a key

    TypeError: Ed25519VerificationKey2020.generate is not a function

       8 | describe("verificationKey", () => {
       9 |     it("generates a key", async () => {
    > 10 |         const key = await Ed25519VerificationKey2020.generate();
         |                                                      ^
      11 |         console.log(`Key: [${JSON.stringify(key, null, 2)}]`);
      12 |     });
      13 | });

      at Object.<anonymous> (simple.test.js:10:54)

Test Suites: 1 failed, 1 total
Tests:       1 failed, 1 total
Snapshots:   0 total
Time:        0.88 s
Ran all test suites.
npm ERR! code 1
npm ERR! path /home/pmcb55/Work/Projects/tmp/vc-t2/tmp-db-problem
npm ERR! command failed
npm ERR! command sh -c jest

npm ERR! A complete log of this run can be found in:
npm ERR!     /home/pmcb55/.npm/_logs/2021-03-31T08_55_53_435Z-debug.log
[tmp-db-problem]$
```

But adding Mocha, and the very same test works fine:
```script 
[tmp-db-problem]$ npm run test-mocha simple.test.js

> tmp-db-problem@1.0.0 test-mocha
> mocha --reporter spec "simple.test.js"



  verificationKey
Key: [{
  "type": "Ed25519VerificationKey2020",
  "publicKeyMultibase": "z3TMsyrJb16wpdkBGQNSkyz9FWFzW3wbygkGMM7REfoir",
  "privateKeyMultibase": "z3yWj4X7BwTuQ8NU1KRFHFCWMgFPaohTR8kJ2S1dwvkPFfFYv3E3FwW72uQQgE94M1t3mtEXBRDU6hd4GpunXZbT8"
}]
    ✓ generates a key


  1 passing (7ms)

[tmp-db-problem]$
```
