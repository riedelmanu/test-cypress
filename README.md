# Cypress RPA Project - SauceDemo E2E Tests

This repository contains an academic project for the course *Technologies for Automation* at UTN FRCU.  
The goal is to demonstrate the use of **Cypress** as an automation and testing tool applied to a real-world scenario:  
automating the purchase flow in the demo e-commerce site [SauceDemo](https://www.saucedemo.com).

---

## Features

- End-to-End (E2E) automated tests with [Cypress](https://www.cypress.io/).
- Test different user profiles provided by SauceDemo:
  - `standard_user` → happy path (successful purchase flow).
  - `locked_out_user` → blocked account, login fails.
  - `problem_user` → broken/repeated product images.
  - `performance_glitch_user` → slow loading and login delays.
  - `error_user` → functional errors with buttons like "Add to cart" or "Checkout".
  - `visual_user` → layout and style issues (fonts, sizes, disordered UI).
- Validates system behavior under both normal and problematic scenarios.

---

## Installation

1. Clone this repository:
   ```bash
   git clone https://github.com/your-user/cypress-rpa.git
   cd cypress-rpa
   ```

2. Initialize a Node.js project:
   ```bash
   npm init -y
   ```

3. Install Cypress as a dev dependency:
   ```bash
   npm install cypress --save-dev
   ```

---

## Project Structure

```
cypress-rpa/
 ├─ cypress/
 │   └─ e2e/
 │       └─ form_test.cy.js   # Test script
 ├─ package.json
 └─ README.md
```

---

## Running the Tests

Open the Cypress Test Runner:
```bash
npx cypress open
```

Or run tests in headless mode:
```bash
npx cypress run
```

---

## Example Test (Purchase Flow)

```javascript
const users = [
  { name: 'standard_user', shouldPass: true },
  { name: 'locked_out_user', shouldPass: false },
  { name: 'problem_user', shouldPass: false },
  { name: 'performance_glitch_user', shouldPass: false },
  { name: 'error_user', shouldPass: false },
  { name: 'visual_user', shouldPass: false }
]

describe('Purchase flow in SauceDemo', () => {
  users.forEach(user => {
    it(`Purchase attempt with ${user.name}`, () => {
      cy.visit('https://www.saucedemo.com/')
      cy.get('#user-name').type(user.name)
      cy.get('#password').type('secret_sauce')
      cy.get('#login-button').click()

      cy.get('#add-to-cart-sauce-labs-backpack').click()
      cy.get('.shopping_cart_link').click()
      cy.get('#checkout').click()
      cy.get('#first-name').type('Manu')
      cy.get('#last-name').type('Riedel')
      cy.get('#postal-code').type('3260')
      cy.get('#continue').click()
      cy.get('#finish').click()

      cy.contains('h2', 'Thank you for your order!').should(
        user.shouldPass ? 'be.visible' : 'not.exist'
      )
    })
  })
})
```

---

## Requirements

- Node.js (v18+ recommended) → [Download here](https://nodejs.org/)  
- npm (comes with Node.js)  

---

## References

- [Cypress Documentation](https://docs.cypress.io/)  
- [SauceDemo](https://www.saucedemo.com)  

---

## Authors

- Juan Ignacio Basgall  
- Juan Cruz Ingani  
- Manuel Ángel Riedel  
- Akeem Silva  

---
