# Cart Validation Changes

## File: data/cart.js
Add validation before cart operations:

```javascript
// Add at top
const validateCartPlans = require('./planValidation').validateCartPlans;

// Add before addToCart function
const validateCart = async (itemId, AccountId) => {
    const validation = await validateCartPlans([{itemId}], AccountId);
    if (!validation.validated) {
        throw {
            statusCode: 400,
            message: validation.error || 'Invalid plan combination'
        };
    }
    return true;
};
```

## Test Steps
1. Try adding basic plan only
2. Try adding internet only
3. Try valid combination

Expected:
- Clear validation errors
- No silent failures
- Proper error messages