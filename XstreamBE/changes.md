# Required Changes

## 1. Auth Fix
```javascript
// utils/authErrorHandler.js
handleAuthError = (err, res, isAPI) => {
    res.clearCookie('userSave');
    return isAPI ? res.status(400).json({error: err.message}) : res.redirect('/register');
};
```

## 2. Cart Fix
```javascript
// data/planValidation.js
validateCartPlans = async (items, accountId) => {
    if (!items.find(i => i.type === 'internet')) return {validated: false, error: 'Internet required'};
    if (!items.find(i => i.type === 'tv')) return {validated: false, error: 'TV plan required'};
    return {validated: true};
};
```

## 3. Payment Fix
```javascript
// data/transactionLog.js
logTransaction = async (data) => {
    return db.transactions.insertOne({
        accountId: data.accountId,
        amount: data.amount,
        status: data.status,
        timestamp: new Date()
    });
};
```

Make these changes in your IDE, commit each one separately, then we can test.