
# Badge Feature for Dawn Theme

This theme extends Shopify's Dawn theme with a customizable product badge display.

## Feature Overview

The badge system displays dynamic product labels (badges) such as Sale, Sold Out, New, Exclusive, Best Seller, and Low Stock. Badges are prioritized, customizable, and can be managed by store admins.

### Supported Badge Types

- **Sale**: Shown when a product's compare-at price is higher than its price.
- **Sold Out**: Shown when a variant is unavailable.
- **Low Stock**: Shown when inventory is 10 or less (Shopify-managed inventory).
- **New**: Set via variant metafield (`custom.custom_badges`).
- **Exclusive**: Set via variant metafield (`custom.custom_badges`).
- **Best Seller**: Set via variant metafield (`custom.custom_badges`).

### Badge Priority (Single Badge Mode for Product Cards)

1. User Preference (`custom.badge_display_preference` metafield)
2. Sold Out
3. New
4. Sale
5. Exclusive
6. Best Seller
7. Low Stock

## For Clients: Creating & Managing Badges

### 1. Setting Custom Badges (New, Exclusive, Best Seller)

- Go to **Products** in Shopify admin
- Select a product and variant
- Under **Metafields**, add or edit `Custom Badges` with one or more of: `New`, `Exclusive`, `Best Seller` 

### 2. Setting Badge Display Preference

- In the product's **Metafields**, add or edit `Badge Display Preference` with one of:
	- `New`, `Best Seller`, `Sale`, `Low Stock`, `Sold Out`, `Exclusive`
- This will force the preferred badge to show (if available) on product cards

### 3. Automatic Badges

- **Sale**: Set a compare-at price higher than the price
- **Sold Out**: When variant inventory is zero/unavailable
- **Low Stock**: When inventory is 10 or less

### 4. Customizing Badge Text & Color

- Go to **Online Store > Customize > Theme settings > Badge Settings**
- Change label text and color scheme for each badge type

### 5. Display Modes

- **Product Cards**: Only the highest-priority badge is shown
- **Product Pages**: All applicable badges are shown

## For Developers: Maintaining the Badge Feature

### Architecture

- Centralized logic in `snippets/product-badge.liquid`
- Badge settings in `config/settings_schema.json` and `settings_data.json`
- Badge styles in `assets/base.css`

### Key Implementation Details

- Uses `target_variant.available` for variant-specific logic
- Reads badge preference from `product.metafields.custom.badge_display_preference`
- Reads custom badges from `variant.metafields.custom.custom_badges`
- Priority and display logic is DRY and easy to extend

### Adding or Modifying Badges

1. Update badge logic in `snippets/product-badge.liquid`
2. Add settings in `settings_schema.json` and `settings_data.json`
3. Add translations in `locales/en.default.schema.json`
4. Add or update CSS in `assets/base.css`

### Rendering Badges

```
{% render 'product-badge', product: product %} {# single badge (card) #}
{% render 'product-badge', product: product, show_multiple: true %} {# all badges (product page) #}
```

### Troubleshooting

- Ensure metafield keys/values are correct and case-sensitive
- Check badge priority order in `product-badge.liquid`
- Use the theme customizer to verify badge appearance

### Maintenance

- Keep this documentation updated with any badge logic or UI changes
- Test all badge types and edge cases after updates

---

For further support, see the code in `snippets/product-badge.liquid` and related config files.
