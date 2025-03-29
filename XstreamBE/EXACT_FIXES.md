# Exact Code Changes

## 1. Error Handling
In data/authorized.js:
```javascript
catch(err) {
    if(err) {
        res.clearCookie('userSave');
        return res.status(401).send({
            hasErrors: true, 
            error: err.message || 'Authentication failed'
        });
    }
}
```

## 2. Cart Validation
In data/checkout.js:
```javascript
const validation = async (data, AccountId) => {
    // Check for required plans
    const items = data.data || [];
    const hasInternet = items.some(item => item.type === 'internet');
    const hasTV = items.some(item => item.type === 'tv');

    if (!hasInternet || !hasTV) {
        throw {
            statusCode: 400,
            message: 'Both Internet and TV plans are required'
        };
    }
    return { validated: true };
};
```

## 3. Transaction Logging
In routes/checkout.js payment-status route:
```javascript
if (Valid === 'True') {
    try {
        helper.validObjectId(CustomField1);
        const checkout = await getItems(CustomField1);
        if(checkout) {
            const update = await updateItems(checkout.data,CustomField1);
            if(update.updated===true) {
                // Add here:
                await logTransaction({
                    accountId: CustomField1,
                    transactionId: TransactionID,
                    amount: Amount,
                    status: 'completed',
                    referenceId: ReferenceID,
                    authCode: AuthCode
                });
                // Continue with existing API calls
```

Apply these changes exactly as shown - they match your current code structure.