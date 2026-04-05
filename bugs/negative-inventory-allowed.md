# 🐞 Bug Report: Negative inventory allowed during adjustment

**Bug ID:** BUG-INV-001
**Module:** Inventory Management
**Severity:** High
**Priority:** High
**Reported By:** Thiago Gibran

## 📝 Description
The inventory adjustment module allows users to enter negative quantities, which bypasses data integrity rules and creates phantom stock.

## 🔄 Steps to Reproduce
1. Open the **Inventory Module**
2. Navigate to **Stock Adjustment**
3. Select an existing SKU (e.g., `SKU-10045`)
4. Enter adjustment quantity: `-10`
5. Click **Save**

## 🎯 Expected Result
The system should block the negative inventory entry and display a validation error: "Quantity cannot be negative."

## 💥 Actual Result
The system accepts the value, saves the adjustment, and updates the total stock to a negative number.

## 🧠 Root Cause Hypothesis
Missing backend validation rule in the inventory adjustment logic. The frontend input field might lack `min="0"` constraints, and the API endpoint is likely accepting any signed integer without boundary checks.

## 💼 Business Impact
If accepted in production, negative inventory corrupts financial reporting, breaks stock valuation algorithms, and causes cascading failures in the procurement module (which relies on accurate stock levels to trigger reorder points).
