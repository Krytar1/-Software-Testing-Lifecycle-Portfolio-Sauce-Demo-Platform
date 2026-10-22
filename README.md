# -Software-Testing-Lifecycle-Portfolio-Sauce-Demo-Platform
This repository showcases a complete end-to-end software testing lifecycle (STLC) documentation designed and executed for the **Sauce Demo** web application (`https://saucedemo.com`). 
---

## 📋 1. User Story & Acceptance Criteria

**Title:** US-1: Shopping Cart Interactions  
**Description:**  
As a customer of the Swag Labs online store,  
I want to add items to my shopping cart so that I can either remove them, continue shopping, or proceed to the checkout process.

**Acceptance Criteria:**
1. The user must see an "Add to cart" button located next to each product.
2. The user must be able to add items to the shopping cart from both the main inventory page (homepage) and the specific product details page.
3. The default item quantity added to the cart must be 1.
4. After successfully adding an item to the cart, the shopping cart icon badge must update dynamically to display the correct number of items.
5. Within the cart view, the user must be able to continue shopping, remove an item, or proceed to the checkout.
6. All action buttons (*"Checkout"*, *"Remove"*, *"Continue Shopping"*) must be fully visible, active, and clickable.
7. The system must restrict and block users from adding an unexpected or excessive volume of items to the cart.
8. After removing all items the shopping cart must update dynamically leaving empty line and system must disable "checkout" button prevent the user form unwanted actions.

---

## 🧠 2. Test Scenario

### **Test Scenario: Shopping Cart Operations (Add & Remove Flow)** 
**ID:** TS-1
**Title:** Verification of adding and removing items functionality within the shopping cart. 
**Objective:** To ensure the system correctly handles the full product lifecycle in the cart by verifying that: 
* The **"Add to cart"** button is visible and fully active on both the homepage and the product details page. 
* Clicking the “Add item” button successfully adds the item to the cart and dynamically updates the total number of items and the total price. 
* The **"Remove"** button is visible, active, and successfully removes the item from the cart. 
* After item removal the total price and total number of items are correctly updated and decreased. 
* After removal of all items the button “Check out” is inactive or invisible.

---

## 📂 3. Test Cases

### TC-1-1: Add Item to the Shopping Cart from the Main Inventory Page (Happy Path)

* **Preconditions:**
  * The website https://www.saucedemo.com/ is opened.
  * The user is logged in with valid credentials (E.g.,`standard_user` / `secret_sauce`).
  * The main inventory page is displayed.
  * Default number of items is "1".

| # | Test Steps | Test Data | Expected Results |
|---|---|---|---|
| 1 | Click the **"Add to cart"** button next to any available product on the main page. | E.g., "Sauce Labs Backpack" | The button text dynamically changes from "Add to cart" to "Remove". |
| 2 | Verify the shopping cart badge in the top right header. | N/A | The cart badge updates dynamically, displaying the number "1". |
| 3 | Click on the shopping cart badge to open the cart page. | N/A | The cart page opens successfully, displaying the selected product, correct quantity (1), and its description. |

* **Postconditions:** The item is correctly added to the shopping cart and the cart badge remains updated.

---

### TC-1-2: Add Product from Details Page and Attempt Invalid Quantity Update (Negative Path)

* **Preconditions:**
  * The website https://www.saucedemo.com/ is opened.
  * The user is logged in with valid credentials(E.g.,`standard_user` / `secret_sauce`).
  * The main inventory page is displayed.

| # | Test Steps | Test Data | Expected Results |
|---|---|---|---|
| 1 | Click on any available product on the main page. | E.g., "Sauce Labs Bike Light" | The product details page opens successfully, displaying the product description and price. |
| 2 | Click the **"Add to cart"** button on the product details page. | Default quantity: 1 | The text on the button dynamically changes from "Add to cart" to "Remove". |
| 3 | Verify the shopping cart badge in the top right header. | N/A | The updated number of items "1" is displayed on the cart badge. |
| 4 | Click on the shopping cart badge to open the cart view. | N/A | The shopping cart page opens successfully, displaying the added item. |
| 5 | Enter an unexpected quantity in the input box next to the product and click **"Update"**. | Quantity: 330 | The system blocks the operation. An error popup appears stating: *"Number out of stock. The allowed maximum number of products is 10."* The "Update" button becomes disabled. |

* **Postconditions:** The system effectively blocks adding an unexpected or excessive amount of items to the shopping cart.

---

### TC-1-3: Add Item from Main Page, Verify Cart, and Perform Item Removal (End-to-End)

* **Preconditions:**
  * The website is opened https://www.saucedemo.com/ is opened.
  * The user is logged in with valid credentials (E.g.,`standard_user` / `secret_sauce`).
  * The main inventory page is displayed.

| # | Test Steps | Test Data | Expected Results |
|---|---|---|---|
| 1 | Click the **"Add to cart"** button next to any available product on the main page. | E.g., "Sauce Labs Backpack" | The button text dynamically changes from "Add to cart" to "Remove". |
| 2 | Verify the shopping cart badge in the top right header. | N/A | The cart badge updates dynamically, displaying the number "1". |
| 3 | Click on the shopping cart badge in the top right header. | N/A | The cart page opens successfully, displaying the correct product description, quantity "1", and price. |
| 4 | Verify the state of the **"Checkout"** button. | N/A | The "Checkout" button is active and clickable. |
| 5 | Verify the state of the **"Remove"** button next to the item. | N/A | The "Remove" button is active and clickable. |
| 6 | Click the **"Remove"** button inside the cart view. | N/A | The item is successfully removed from the cart. The product row disappears from the list. |
| 7 | Check the **"Checkout"** button after item removal. | N/A | The "Checkout" button becomes disabled (the user cannot proceed with an empty cart). |
| 8 | Verify the shopping cart badge in the top right header again. | N/A | The cart badge updates dynamically, and the number "1" is no longer visible (the badge is empty). |

* **Postconditions:** After removing the final item, the "Checkout" button is disabled, preventing the customer from proceeding with an empty cart.

---

### Bug Report: "Checkout" button remains active after removing all items from the cart

**Bug ID:** BUG-1B
**Status:** New  
**Severity:** Critical 
**Priority:** High  
**Author:** Krystyna Tarczynska  
**Environment:** Windows 11, Google Chrome v155.0.8059.41  
**URL:** `https://saucedemo.com`

#### **Title:**
The "Checkout" button remains active and clickable when the shopping cart is completely empty, allowing users to proceed to checkout.

#### **Steps to Reproduce:**
1. Navigate to `https://www.saucedemo.com/`.
2. Log in with valid credentials: `standard_user` / `secret_sauce`.
3. Click the **"Add to cart"** button next to any available product (e.g., "Sauce Labs Backpack").
4. Verify that the item is added and the cart badge displays "1".
5. Click the shopping cart badge in the top right header to open the cart view.
6. Verify that both **"Remove"** and **"Checkout"** buttons are active.
7. Click the **"Remove"** button next to the product to empty the cart.
8. Observe the state of the **"Checkout"** button.

#### **Actual Result:**
After removing all items, the shopping cart becomes completely empty, but the **"Checkout"** button remains active and fully clickable. The user is able to proceed to the checkout screens and attempt to process an empty order.

#### **Expected Result:**
After all items are removed and the cart item count drops to 0, the **"Checkout"** button must automatically become disabled or hidden. The system must prevent the user from proceeding to the checkout flow with an empty cart.
