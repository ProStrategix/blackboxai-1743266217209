# Authentication Changes Validation Steps

## Test Case 1: Invalid Login
1. Start your server
2. Try to login with invalid credentials
Expected: 
- Clear error message
- Redirect to register page
- Cookie cleared

## Test Case 2: Session Timeout
1. Login successfully
2. Wait for session to expire (or delete cookie)
3. Try to access protected route
Expected:
- Clean redirect to login
- No silent failures
- Cookie cleared

## Test Case 3: API Error
1. Use Postman/curl to hit auth endpoint with invalid token
```bash
curl -X POST http://localhost:3000/auth/status \
  -H "Content-Type: application/json" \
  -d '{"token": "invalid"}'
```
Expected:
- Status 400/401
- JSON error response
- Clear error message

## Verification Checklist
- [ ] No silent failures
- [ ] Clear error messages
- [ ] Proper redirects
- [ ] Cookies cleaned up
- [ ] API returns JSON errors

If any test fails, the error handler needs adjustment.