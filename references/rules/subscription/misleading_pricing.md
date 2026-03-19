# Rule: Misleading Subscription Pricing Display
- **Guideline**: 3.1.2 – Business – Payments – Subscriptions
- **Severity**: REJECTION
- **Category**: subscription

## What to Check
The subscription purchase flow must display the **actual billed amount** as the most prominent pricing element. Calculated/derived pricing (e.g., "only $2.50/month" for an annual plan billed at $29.99/year) must be **subordinate** in:

- Font size
- Font weight
- Color contrast
- Position/layout

### Common Violations
- Showing "$2.50/mo" in large bold text while "$29.99/year" is in small gray text
- Using a bright accent color for the calculated monthly price but muted text for the real billed amount
- Placing the per-month breakdown above or more prominently than the actual charge
- Free trial text overshadowing the post-trial billed price

## How to Detect

### Code Inspection
```bash
# Find subscription UI code
grep -rn "paywall\|subscribe\|pricing\|subscription" --include="*.swift" --include="*.dart" .

# Look for calculated pricing patterns
grep -rn "perMonth\|per_month\|monthly.*price\|price.*month\|calculated\|divided" --include="*.swift" --include="*.dart" .
```

### Visual Inspection
1. Run the app and navigate to the subscription purchase screen
2. Compare the visual hierarchy of:
   - The calculated price (per month/week breakdown)
   - The actual billed amount (what Apple will charge)
   - Free trial or introductory pricing text
3. The **billed amount** must be the largest, boldest, most visible price

### Checklist
- [ ] Billed amount uses the largest font size among all pricing elements
- [ ] Billed amount has the highest contrast color
- [ ] Billed amount is positioned prominently (not buried below other pricing)
- [ ] Calculated/broken-down pricing uses smaller, lighter text
- [ ] Free trial terms do not overshadow the post-trial price

## Resolution
1. Make the total billed amount the most prominent pricing text
2. Show calculated pricing (per month / per week) in smaller, subordinate text
3. Ensure free trial duration is visible but does not overshadow the billing amount
4. Follow [Apple HIG guidance for subscription purchase flows](https://developer.apple.com/design/human-interface-guidelines/in-app-purchase)

## Example Rejection
> **Guideline 3.1.2 - Business - Payments - Subscriptions**
>
> One or more auto-renewable subscriptions are marketed in the purchase flow in a way that may mislead or confuse users about the subscription terms or pricing. Specifically:
>
> - The auto-renewable subscription displays the monthly calculated pricing for the subscription more clearly and conspicuously than the billed amount.
>
> Next Steps
>
> To resolve this issue, it would be appropriate to:
>
> - Revise the auto-renewable subscription purchase flow to ensure that the billed amount is the most clear and conspicuous pricing element in the layout. Any other pricing elements, including free trial, introductory pricing, and calculated pricing information, must be displayed in a subordinate position and size to the total billed amount.
