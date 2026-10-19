# Official source corroboration

After the live browser tests, the official Sauce Labs source was reviewed to confirm that the three observed behaviours are deliberately coded for `problem_user`.

Source snapshot: commit `009b7a5b9db78488b014e689258840a6a7d7741f`, reviewed on 19 October 2026. The exact commit deployed on the live site was not identified, so these references corroborate the training design without proving a deployed code-level root cause.

- **Account identification:** [Credentials.js, lines 55-57](https://github.com/saucelabs/sample-app-web/blob/009b7a5b9db78488b014e689258840a6a7d7741f/src/utils/Credentials.js#L55-L57) identifies `problem_user`.
- **LIVE-BUG-01:** [Inventory.jsx, lines 115-119](https://github.com/saucelabs/sample-app-web/blob/009b7a5b9db78488b014e689258840a6a7d7741f/src/pages/Inventory.jsx#L115-L119) substitutes the same fallback image for that account's products.
- **LIVE-BUG-02:** [InventoryListItem.jsx, lines 33-39](https://github.com/saucelabs/sample-app-web/blob/009b7a5b9db78488b014e689258840a6a7d7741f/src/components/InventoryListItem.jsx#L33-L39) exits the add handler for odd product IDs under this account. [InventoryData.js, lines 9-15](https://github.com/saucelabs/sample-app-web/blob/009b7a5b9db78488b014e689258840a6a7d7741f/src/utils/InventoryData.js#L9-L15) associates the Bolt T-Shirt with ID 1.
- **LIVE-BUG-03:** [CheckOutStepOne.jsx, lines 25-35](https://github.com/saucelabs/sample-app-web/blob/009b7a5b9db78488b014e689258840a6a7d7741f/src/pages/CheckOutStepOne.jsx#L25-L35) directs Last Name changes into First Name for this account. The required Last Name check remains in place.

The portfolio therefore describes actual observations of seeded public demo defects, not new production incidents or unique discoveries.
