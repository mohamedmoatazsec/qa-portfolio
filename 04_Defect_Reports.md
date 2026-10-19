# Defect reports

**Observed:** 19 October 2026 · **Target:** [SauceDemo](https://www.saucedemo.com/) · **Method:** browser-assisted functional checks

These reports document seeded faults in the public `problem_user` account. Expected behavior is based on visible controls and comparison with `standard_user`. Each issue was reproduced twice within one browser session. No external tickets were submitted.

**Environment:** Windows; browser engine version, viewport and deployed build were not recorded. Only published demo credentials and invented checkout data were used. The original [execution record](Evidence/Browser/Web_Execution_Evidence.json) provides the recorded observations.

**Triage convention:** Severity describes functional impact. Priority is a proposal for an equivalent shopper-facing application: P1 = address first; P2 = schedule after the checkout blocker. These are practice recommendations, not the demo owner's triage decisions.

| Defect | Summary | Severity | Proposed priority | Related case |
|---|---|---|---|---|
| LIVE-BUG-01 | All six products display the same incorrect photo | Medium | P2 | WEB-08 |
| LIVE-BUG-02 | Bolt T-Shirt is not added to the cart | High | P2 | WEB-09 |
| LIVE-BUG-03 | Last Name entry changes First Name and blocks checkout | High | P1 | WEB-10 |

<a id="live-bug-01"></a>

## LIVE-BUG-01 — All six products display the same incorrect photo

**Related case:** WEB-08 · **Severity:** Medium · **Proposed priority:** P2

**Preconditions:** Open SauceDemo inventory as problem_user using the published demo credentials. Retain the standard_user inventory screenshot from WEB-01 as a comparison.

**Steps to reproduce:**

1. Inspect the photograph for each of the six named products.
2. Compare the photographs and image sources with the standard_user baseline.
3. Reload inventory.
4. Inspect the six photographs again.

**Expected:** Every product displays its corresponding photograph. The standard_user comparison shows six distinct product-image sources.

**Actual:** All six products displayed the same dog photograph. Each image was fully loaded and used /assets/sl-404-Cq1a9k9X.jpg. The same result remained after reload; this was incorrect loaded content rather than an incomplete image load.

**Impact:** Incorrect photos make the products harder to recognise. Names and prices remain visible, so customers can still identify items by text.

**Priority rationale:** Schedule after the checkout blocker. Product recognition is affected across the catalog, while names, prices and cart controls remain available.

**Reproducibility:** 2/2 observations in one session: initial inspection and one inspection after reload. Coverage does not include another browser or device.

**Control:** The standard_user control confirmed six loaded, distinct product images.

**Evidence:** [09-problem-product-images.png](Evidence/Browser/09-problem-product-images.png) · [16-standard-image-control.png](Evidence/Browser/16-standard-image-control.png) · [01-standard-inventory.png](Evidence/Browser/01-standard-inventory.png)

<a id="live-bug-02"></a>

## LIVE-BUG-02 — Bolt T-Shirt is not added to the cart

**Related case:** WEB-09 · **Severity:** High · **Proposed priority:** P2

**Preconditions:** Prepare a cart containing one Sauce Labs Backpack as standard_user. Log out and sign in as problem_user. Open inventory; cart count is 1 and Bolt T-Shirt shows Add to cart.

**Steps to reproduce:**

1. Select Add to cart for Sauce Labs Bolt T-Shirt.
2. Inspect its button and the cart count.
3. Reload inventory.
4. Select the same Add to cart button again.
5. Open Cart.
6. Inspect the product rows.

**Expected:** The T-Shirt is added alongside the backpack, its control becomes Remove and cart count increases from 1 to 2.

**Actual:** Both clicks left Add to cart visible and count at 1. No Remove control appeared for this product. The cart contained only the backpack, confirming that this was not merely an incorrect badge.

**Impact:** The problem_user account cannot add the T-Shirt for purchase through its Add to cart control.

**Priority rationale:** Schedule after the checkout blocker. A core cart action fails, but the confirmed scope is one product/account and the backpack remains available.

**Reproducibility:** 2/2 click attempts in one session; the second followed a reload.

**Control:** The same-item standard_user control showed Remove and cart count 2.

**Evidence:** [10-problem-add-to-cart-first.png](Evidence/Browser/10-problem-add-to-cart-first.png) · [11-problem-add-to-cart-reproduced.png](Evidence/Browser/11-problem-add-to-cart-reproduced.png) · [12-problem-cart-item-absent.png](Evidence/Browser/12-problem-cart-item-absent.png) · [17-standard-bolt-add-control.png](Evidence/Browser/17-standard-bolt-add-control.png)

<a id="live-bug-03"></a>

## LIVE-BUG-03 — Last Name entry changes First Name and blocks checkout

**Related case:** WEB-10 · **Severity:** High · **Proposed priority:** P1

**Preconditions:** Prepare one backpack in the cart as standard_user. Log out and sign in as problem_user. Open Cart and select Checkout. Use invented data QA / Tester / 12345.

**Steps to reproduce:**

1. Enter QA in First Name.
2. Enter Tester in Last Name.
3. Enter 12345 in Zip/Postal Code.
4. Inspect the three field values.
5. Select Continue.
6. Reload the information page.
7. Repeat steps 1–5 using sequential keystrokes.

**Expected:** First Name retains QA, Last Name retains Tester and postal code retains 12345. Continue opens the checkout overview.

**Actual:** Last Name remained empty. Browser field filling changed First Name to Tester; sequential typing left First Name as r. Postal code retained 12345. Both attempts displayed “Error: Last Name is required” and did not advance.

**Impact:** The problem_user account cannot complete the required information, blocking checkout before order review.

**Priority rationale:** Address first. Valid input cannot satisfy a required field, preventing the tested account from reaching order review.

**Reproducibility:** 2/2 attempts in one session: one browser field-fill attempt and one post-reload sequential-keystroke attempt.

**Control:** WEB-07 accepted identical data for standard_user and reached the checkout overview.

**Evidence:** [13-problem-checkout-fields.png](Evidence/Browser/13-problem-checkout-fields.png) · [14-problem-checkout-blocked.png](Evidence/Browser/14-problem-checkout-blocked.png) · [15-problem-checkout-reproduced.png](Evidence/Browser/15-problem-checkout-reproduced.png) · [06-standard-checkout-fields.png](Evidence/Browser/06-standard-checkout-fields.png) · [07-standard-checkout-overview.png](Evidence/Browser/07-standard-checkout-overview.png)


