# Product Spec: Pantry Pal

*A food-waste-reducing kitchen companion. Draft v0.1, an example spec with assumptions you can edit.*

## 1. Overview

Pantry Pal helps households track what food they have, know what is about to expire, and decide what to cook tonight. The core promise: **use what you already own before it goes bad.**

## 2. Problem

Households throw away a large share of the food they buy. The causes are mundane: forgotten leftovers, duplicate purchases, and no quick way to turn a random set of ingredients into a meal. Existing inventory apps fail because manual data entry is tedious and people stop after a week.

## 3. Goals and Non-Goals

**Goals**

- Make adding items take under 10 seconds per grocery trip item batch
- Surface the right "use soon" items at the right moment
- Suggest recipes built around expiring ingredients
- Reduce self-reported food waste by 30% within 8 weeks of use

**Non-Goals (v1)**

- Grocery delivery or checkout integrations
- Nutrition or calorie tracking
- Social or recipe-sharing features

## 4. Target Users

| Persona | Description | Key need |
| --- | --- | --- |
| Busy family cook | Shops weekly for 3 to 5 people | Avoid duplicate buys, plan dinners fast |
| Young professional | Cooks a few nights a week | Stop wasting produce and leftovers |
| Budget-conscious student | Shares a kitchen | Stretch groceries, simple recipes |

## 5. Core User Stories

1. As a shopper, I can **scan a receipt** and have items added automatically with estimated expiry dates.
2. As a cook, I can see a **"Use Soon" list** sorted by urgency.
3. As a cook, I can get **recipe suggestions** that prioritize expiring items.
4. As a household member, I can **share one pantry** with others in real time.
5. As a user, I can mark an item **used, tossed, or frozen**, so the app learns my habits.
6. As a shopper, I can view a **"Don't buy" check** while in the store, showing what I already have.

## 6. Functional Requirements

### 6.1 Item capture

- Receipt scan (OCR) with item matching to a food database
- Barcode scan as a fallback
- Manual quick-add with autocomplete
- Default shelf-life estimates by food category and storage location (fridge, freezer, pantry), editable by the user

### 6.2 Expiry alerts

- Daily digest notification at a user-chosen time
- Per-item alerts at 2 days and 0 days before estimated expiry
- Quiet hours and alert-frequency controls

### 6.3 Recipe suggestions

- Rank recipes by the share of expiring ingredients used
- Filters: time available, dietary preferences, allergens
- Show missing ingredients clearly, with a maximum of 3 missing by default

### 6.4 Shared households

- Invite by link, up to 6 members
- Activity feed ("Sam used the spinach")
- Last-write-wins sync with an offline queue

## 7. User Flow: First Week

1. **Day 0:** Onboard, set dietary preferences, scan first receipt.
2. **Day 1:** Confirm auto-detected items and storage locations.
3. **Day 2:** Receive first "Use Soon" digest; open a suggested recipe.
4. **Day 5:** Prompt to log what was used or tossed.
5. **Day 7:** Weekly summary: items saved, estimated money saved.

## 8. Success Metrics

| Metric | Target |
| --- | --- |
| Week-4 retention | 35% |
| Receipts scanned per active user per month | 3 or more |
| Items marked "used" vs. "tossed" | 80/20 ratio |
| Self-reported waste reduction | 30% at 8 weeks |
| Notification opt-out rate | Under 15% |

## 9. Technical Approach

- **Clients:** iOS and Android (cross-platform framework), plus a lightweight web view
- **Backend:** REST API, relational database for households, items, and events
- **OCR and matching:** third-party receipt OCR, with a food-category classifier for shelf-life defaults
- **Recipes:** licensed recipe API, with ingredient matching on normalized names
- **Privacy:** receipt images deleted after processing; data export and deletion on request

## 10. Risks and Mitigations

| Risk | Impact | Mitigation |
| --- | --- | --- |
| OCR misreads receipts | Frustration, churn | Fast review screen; learn from corrections |
| Inaccurate expiry estimates | Loss of trust | Conservative defaults; user-editable dates |
| Notification fatigue | Opt-outs | Single daily digest by default |
| Recipe API cost | Margin pressure | Cache results; limit free-tier lookups |

## 11. Milestones

| Phase | Scope | Target |
| --- | --- | --- |
| Alpha | Manual add, Use Soon list, expiry alerts | Week 6 |
| Beta | Receipt scan, recipe suggestions | Week 12 |
| Launch | Shared households, onboarding polish | Week 16 |

## 12. Open Questions

- Should freemium limits apply to receipt scans or to household size?
- Do we support regional food databases at launch, or English-speaking markets only?
- How should the app handle partially used items (half a bag of rice)?
