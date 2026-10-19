# Website test cases

**Executed:** 19 October 2026 · **Target:** [SauceDemo](https://www.saucedemo.com/) · **Method:** browser-assisted functional checks

Seven baseline checks passed; three scenarios reproduced seeded defects in the published `problem_user` account. Results below use normal shopper expectations, visible UI labels and the working `standard_user` comparison. These are public demo accounts with intentional faults; the failures are not production defect discoveries.

**Environment:** Windows; controlled browser session. Exact browser engine version, viewport and deployed build were not recorded. Each case ran once unless a repeat is stated. Published demo credentials and invented checkout data were used.

| Case | Scenario | Type | Result | Defect |
|---|---|---|---|---|
| WEB-01 | Sign in with a valid account | Functional | PASS | — |
| WEB-02 | Reject a locked account | Negative | PASS | — |
| WEB-03 | Sort products by price | Functional | PASS | — |
| WEB-04 | Add a backpack to the cart | Functional | PASS | — |
| WEB-05 | Remove the only cart item | Functional | PASS | — |
| WEB-06 | Reject checkout with empty information | Negative | PASS | — |
| WEB-07 | Continue with valid checkout information | Functional | PASS | — |
| WEB-08 | Check catalog product photographs | Visual | FAIL | LIVE-BUG-01 |
| WEB-09 | Add a second product to the cart | Functional | FAIL | LIVE-BUG-02 |
| WEB-10 | Retain Last Name during checkout | Functional | FAIL | LIVE-BUG-03 |

## WEB-01 — Sign in with a valid account

**Type:** Functional · **Result:** PASS

**Preconditions:** Open https://www.saucedemo.com/ with no account signed in.

**Test data:** Username standard_user; use the published password shown on the login page.

1. Enter standard_user in Username.
2. Enter the published demo password.
3. Select Login.
4. Inspect the destination and inventory.

**Expected:** The inventory page opens and the product catalog is visible.

**Actual:** The browser reached /inventory.html. All six catalog products were visible, with distinct product-image sources. These images supplied the normal inventory reference for the later problem_user comparison.

**Evidence:** [01-standard-inventory.png](Evidence/Browser/01-standard-inventory.png)

## WEB-02 — Reject a locked account

**Type:** Negative · **Result:** PASS

**Preconditions:** Open the demo login page with no account signed in.

**Test data:** Username locked_out_user; use the published demo password.

1. Enter locked_out_user in Username.
2. Enter the published demo password.
3. Select Login.
4. Inspect the error message and current page.

**Expected:** Login is refused with a locked-account message; the inventory does not open.

**Actual:** The page displayed “Epic sadface: Sorry, this user has been locked out.” The browser remained at https://www.saucedemo.com/. No inventory page was reached by the rejected login attempt.

**Evidence:** [08-locked-out-login.png](Evidence/Browser/08-locked-out-login.png)

## WEB-03 — Sort products by price

**Type:** Functional · **Result:** PASS

**Preconditions:** Sign in as standard_user and open inventory. All six catalog products are present.

**Test data:** Sort option: Price (low to high).

1. Open the product sort selector.
2. Select Price (low to high).
3. Read every displayed price from the first product to the last.
4. Check that all six products remain visible.

**Expected:** All six products remain present and prices appear in non-decreasing numerical order. Equal prices are valid.

**Actual:** Prices were $7.99, $9.99, $15.99, $15.99, $29.99 and $49.99. All six products remained present.

**Evidence:** [02-standard-price-sort.png](Evidence/Browser/02-standard-price-sort.png)

## WEB-04 — Add a backpack to the cart

**Type:** Functional · **Result:** PASS

**Preconditions:** Sign in as standard_user; open inventory with an empty cart. Remove any existing items before starting.

**Test data:** Product: Sauce Labs Backpack; listed price $29.99.

1. Find Sauce Labs Backpack.
2. Select its Add to cart button.
3. Open the cart.
4. Inspect the product name, quantity, price and available control.

**Expected:** The cart contains one Sauce Labs Backpack, quantity 1, priced at $29.99, with a Remove control.

**Actual:** The cart displayed the backpack, quantity 1, $29.99 and a Remove control.

**Evidence:** [03-standard-cart-added.png](Evidence/Browser/03-standard-cart-added.png)

## WEB-05 — Remove the only cart item

**Type:** Functional · **Result:** PASS

**Preconditions:** Continue from WEB-04 as standard_user. The cart contains only one Sauce Labs Backpack.

**Test data:** Remove control for Sauce Labs Backpack.

1. Open the cart if it is not already displayed.
2. Select Remove for the backpack.
3. Inspect the remaining product rows and navigation controls.

**Expected:** The backpack disappears and no product rows remain. Cart navigation remains available.

**Actual:** No product row remained after removal. The cart still displayed its headings, Continue Shopping and Checkout controls.

**Evidence:** [04-standard-cart-removed.png](Evidence/Browser/04-standard-cart-removed.png)

## WEB-06 — Reject checkout with empty information

**Type:** Negative · **Result:** PASS

**Preconditions:** Sign in as standard_user. Add one Sauce Labs Backpack to an otherwise empty cart; open Cart and select Checkout.

**Test data:** First Name, Last Name and Zip/Postal Code: all empty.

1. Verify that all three information fields are empty.
2. Select Continue.
3. Inspect the validation message and page.

**Expected:** Checkout remains on the information page and identifies First Name as required.

**Actual:** “Error: First Name is required” appeared; the URL remained /checkout-step-one.html. Separate validation of Last Name and postal code was not tested by this case.

**Evidence:** [05-standard-required-validation.png](Evidence/Browser/05-standard-required-validation.png)

## WEB-07 — Continue with valid checkout information

**Type:** Functional · **Result:** PASS

**Preconditions:** Sign in as standard_user. Keep one Sauce Labs Backpack in the cart; open Cart and select Checkout.

**Test data:** First Name QA; Last Name Tester; Zip/Postal Code 12345. All data is invented.

1. Enter QA in First Name.
2. Enter Tester in Last Name.
3. Enter 12345 in Zip/Postal Code.
4. Inspect the three values.
5. Select Continue.

**Expected:** Values remain in their own fields and checkout advances to the overview.

**Actual:** The fields retained QA / Tester / 12345. The overview opened at /checkout-step-two.html with the backpack and total $32.39. Finish was not selected.

**Evidence:** [06-standard-checkout-fields.png](Evidence/Browser/06-standard-checkout-fields.png) · [07-standard-checkout-overview.png](Evidence/Browser/07-standard-checkout-overview.png)

## WEB-08 — Check catalog product photographs

**Type:** Visual · **Result:** FAIL · **Defect:** [LIVE-BUG-01](04_Defect_Reports.md#live-bug-01)

**Preconditions:** Sign in as problem_user and open inventory. Use the standard_user inventory from WEB-01 as the comparison.

**Test data:** All six product photographs.

1. Inspect each loaded product photograph.
2. Compare each photograph and image source with the standard_user baseline.
3. Reload inventory.
4. Repeat the inspection.

**Expected:** Each named product displays its corresponding photograph, consistent with the baseline.

**Actual:** All six loaded images showed the same dog photograph and shared one source. The outcome persisted after reload: 2/2 observations in one session. A standard_user control confirmed six distinct, loaded product images.

**Evidence:** [09-problem-product-images.png](Evidence/Browser/09-problem-product-images.png) · [01-standard-inventory.png](Evidence/Browser/01-standard-inventory.png) · [16-standard-image-control.png](Evidence/Browser/16-standard-image-control.png)

## WEB-09 — Add a second product to the cart

**Type:** Functional · **Result:** FAIL · **Defect:** [LIVE-BUG-02](04_Defect_Reports.md#live-bug-02)

**Preconditions:** Prepare one backpack in the cart as standard_user, then log out and sign in as problem_user. Open inventory; Bolt T-Shirt is absent; cart count is 1.

**Test data:** Sauce Labs Bolt T-Shirt; Add to cart.

1. Select Add to cart for Bolt T-Shirt.
2. Inspect its button and cart count.
3. Reload inventory.
4. Repeat the click.
5. Open Cart and inspect the product rows.

**Expected:** The T-Shirt appears in the cart, its button becomes Remove and count increases to 2.

**Actual:** Both attempts left Add to cart and count 1. Cart contained only the backpack. A same-item standard_user control showed Remove and count 2.

**Evidence:** [10-problem-add-to-cart-first.png](Evidence/Browser/10-problem-add-to-cart-first.png) · [11-problem-add-to-cart-reproduced.png](Evidence/Browser/11-problem-add-to-cart-reproduced.png) · [12-problem-cart-item-absent.png](Evidence/Browser/12-problem-cart-item-absent.png) · [17-standard-bolt-add-control.png](Evidence/Browser/17-standard-bolt-add-control.png)

## WEB-10 — Retain Last Name during checkout

**Type:** Functional · **Result:** FAIL · **Defect:** [LIVE-BUG-03](04_Defect_Reports.md#live-bug-03)

**Preconditions:** Prepare one backpack as standard_user, then log out and sign in as problem_user. Open Cart and select Checkout.

**Test data:** QA / Tester / 12345, as in WEB-07.

1. Enter QA in First Name.
2. Enter Tester in Last Name.
3. Enter 12345 in Zip/Postal Code.
4. Inspect each field value.
5. Select Continue.
6. Reload the information page.
7. Repeat using sequential keystrokes.

**Expected:** Each field retains its own value; checkout advances to the overview.

**Actual:** Last Name stayed empty. Browser field filling changed First Name to Tester; sequential typing left it as r. Both attempts showed “Error: Last Name is required” and prevented progression. The standard_user baseline accepted identical data.

**Evidence:** [13-problem-checkout-fields.png](Evidence/Browser/13-problem-checkout-fields.png) · [14-problem-checkout-blocked.png](Evidence/Browser/14-problem-checkout-blocked.png) · [15-problem-checkout-reproduced.png](Evidence/Browser/15-problem-checkout-reproduced.png)

## Scope and evidence

Checkout stopped at the overview. Temporary cart items were removed and the browser was left at login.

The [execution record](Evidence/Browser/Web_Execution_Evidence.json) retains timestamps, image-source checks, field values and control observations. Cross-browser coverage, performance and a complete regression suite are outside this exercise.

