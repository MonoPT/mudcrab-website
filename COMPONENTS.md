# Mudcrab component inventory

This document is the implementation plan for the reusable component library in `src/components`. The visual direction follows the reference board: dark Skyrim-inspired surfaces, quiet blue accents, fine borders, generous spacing, and restrained ornament. The system should stay consistent and accessible rather than reproduce every visual detail from the generated image.

## Global conventions

- **Font:** `Inter` for body copy, labels, navigation, controls, and metadata.
- **Display font:** `Cinzel` for page titles, section headings, card headings, and brand lockups.
- **Components:** Svelte 5 components using runes and snippets where composition is needed.
- **Primitives:** Use `bits-ui` for behavior-heavy components such as accordion, tabs, select, checkbox, radio group, switch, dialog, tooltip, and dropdown menu.
- **Styling:** Component styles should consume CSS custom properties from `src/routes/theme.css`; components should not hard-code the palette.
- **Accessibility:** Keyboard support, visible focus states, semantic elements, labels, ARIA state, reduced motion, and sufficient color contrast are required.
- **Icons:** Use the installed `@lucide/svelte` icon set. Prefer direct component imports and accept custom icons through snippets or `children`, not string names that require a hidden registry.

## Component inventory

### 1. Brand and layout

#### `BrandMark.svelte`
Reusable identity lockup for the header, footer, and showcase hero.

| Attribute | Type | Default | Description |
|---|---|---|---|
| `name` | `string` | `'Mudcrab'` | Brand name. |
| `subtitle` | `string` | `undefined` | Optional supporting line. |
| `compact` | `boolean` | `false` | Mark-only or reduced lockup for narrow spaces. |
| `href` | `string` | `'/'` | Destination when rendered as a link. |
| `class` | `string` | `''` | Additional class names. |

#### `SiteHeader.svelte`
Responsive navigation/header shell.

| Attribute | Type | Default | Description |
|---|---|---|---|
| `brand` | `Snippet` | required | Brand content. |
| `items` | `NavItem[]` | `[]` | `{ label, href, active?, external? }` navigation items. |
| `actions` | `Snippet` | `undefined` | Optional right-side actions. |
| `sticky` | `boolean` | `false` | Keeps the header at the top while scrolling. |
| `mobileLabel` | `string` | `'Open menu'` | Accessible label for the mobile menu trigger. |

#### `PageShell.svelte`
Consistent centered page width and responsive gutters.

| Attribute | Type | Default | Description |
|---|---|---|---|
| `children` | `Snippet` | required | Page content. |
| `width` | `'narrow' \| 'wide' \| 'full'` | `'wide'` | Content max-width preset. |
| `class` | `string` | `''` | Additional class names. |

#### `SectionHeader.svelte`
Eyebrow, title, description, and optional action used to start sections.

| Attribute | Type | Default | Description |
|---|---|---|---|
| `eyebrow` | `string` | `undefined` | Small uppercase section label. |
| `title` | `string` | required | Main heading. |
| `description` | `string` | `undefined` | Supporting copy. |
| `align` | `'left' \| 'center'` | `'left'` | Text alignment. |
| `action` | `Snippet` | `undefined` | Optional action slot. |

#### `Divider.svelte`
Ornamental or plain section divider.

| Attribute | Type | Default | Description |
|---|---|---|---|
| `ornament` | `boolean` | `false` | Adds the small centered mark treatment. |
| `label` | `string` | `undefined` | Optional accessible label. |
| `spacing` | `'sm' \| 'md' \| 'lg'` | `'md'` | Vertical spacing preset. |

### 2. Actions and navigation

#### `Button.svelte`
Primary action primitive. Icon-only buttons use the same component with `variant="button"`; they must provide an accessible `label`.

| Attribute | Type | Default | Description |
|---|---|---|---|
| `variant` | `'primary' \| 'secondary' \| 'ghost' \| 'danger' \| 'button'` | `'secondary'` | Visual emphasis; `button` is the square icon-only treatment. |
| `size` | `'sm' \| 'md' \| 'lg'` | `'md'` | Control size. |
| `type` | `'button' \| 'submit' \| 'reset'` | `'button'` | Native button type. |
| `label` | `string` | `undefined` | Required for `variant="button"`; becomes the accessible name. |
| `disabled` | `boolean` | `false` | Disables interaction. |
| `loading` | `boolean` | `false` | Shows progress and prevents repeated submission. |
| `leading` / `trailing` | `Snippet` | `undefined` | Optional Lucide icon/content slots. |
| `children` | `Snippet` | `undefined` | Button label; omitted for icon-only buttons. |

#### `Link.svelte`
Text link with default, hover, external, and inline-arrow treatments.

| Attribute | Type | Default | Description |
|---|---|---|---|
| `href` | `string` | required | Link destination. |
| `variant` | `'default' \| 'muted' \| 'inline'` | `'default'` | Visual treatment. |
| `external` | `boolean` | `false` | Adds external indicator and safe link attributes. |
| `arrow` | `boolean` | `false` | Adds a trailing arrow indicator. |
| `underline` | `boolean` | `true` | Controls underline treatment. |
| `children` | `Snippet` | required | Link content. |

### 3. Content and surfaces

#### `Card.svelte`
Base bordered surface for feature, blog, gallery, and utility content.

| Attribute | Type | Default | Description |
|---|---|---|---|
| `variant` | `'default' \| 'feature' \| 'media' \| 'interactive'` | `'default'` | Layout and hover treatment. |
| `href` | `string` | `undefined` | Makes the card a link. |
| `eyebrow` | `string` | `undefined` | Optional metadata label. |
| `title` | `string` | `undefined` | Card heading. |
| `description` | `string` | `undefined` | Supporting copy. |
| `image` | `string` | `undefined` | Optional media URL. |
| `footer` | `Snippet` | `undefined` | Footer content/action slot. |

#### `Badge.svelte`
Compact status/category label.

| Attribute | Type | Default | Description |
|---|---|---|---|
| `tone` | `'neutral' \| 'accent' \| 'success' \| 'warning' \| 'danger'` | `'neutral'` | Semantic color. |
| `size` | `'sm' \| 'md'` | `'sm'` | Badge size. |
| `icon` | `Snippet` | `undefined` | Optional Lucide icon. |
| `children` | `Snippet` | required | Badge label. |

#### `EmptyState.svelte`
Friendly placeholder for unavailable or empty content.

| Attribute | Type | Default | Description |
|---|---|---|---|
| `icon` | `Snippet` | `undefined` | Optional icon. |
| `title` | `string` | required | Empty-state heading. |
| `description` | `string` | `undefined` | Explanation. |
| `action` | `Snippet` | `undefined` | Optional recovery action. |

### 4. Forms and controls

#### `TextInput.svelte`
Text, search, and password input wrapper.

| Attribute | Type | Default | Description |
|---|---|---|---|
| `label` | `string` | required | Visible or visually-hidden label. |
| `value` | `string` | `''` | Bindable value. |
| `placeholder` | `string` | `undefined` | Input hint. |
| `type` | `'text' \| 'search' \| 'password' \| 'email'` | `'text'` | Native input type. |
| `description` | `string` | `undefined` | Supporting help text. |
| `error` | `string` | `undefined` | Validation message. |
| `disabled` | `boolean` | `false` | Disables input. |
| `required` | `boolean` | `false` | Marks input required. |

#### `Select.svelte` — bits-ui
Single-value selection with keyboard navigation and portal support.

| Attribute | Type | Default | Description |
|---|---|---|---|
| `label` | `string` | required | Visible label. |
| `value` | `string` | `undefined` | Bindable selected value. |
| `items` | `SelectItem[]` | required | `{ label, value, disabled? }` options. |
| `placeholder` | `string` | `'Select an option'` | Empty state. |
| `disabled` | `boolean` | `false` | Disables selection. |
| `error` | `string` | `undefined` | Validation message. |

#### `Checkbox.svelte` — bits-ui
Single boolean setting.

| Attribute | Type | Default | Description |
|---|---|---|---|
| `label` | `string` | required | Checkbox label. |
| `checked` | `boolean` | `false` | Bindable state. |
| `description` | `string` | `undefined` | Supporting text. |
| `disabled` | `boolean` | `false` | Disables interaction. |
| `indeterminate` | `boolean` | `false` | Shows mixed state. |

#### `RadioGroup.svelte` — bits-ui
Mutually exclusive options.

| Attribute | Type | Default | Description |
|---|---|---|---|
| `label` | `string` | required | Group label. |
| `value` | `string` | `undefined` | Bindable selected value. |
| `items` | `RadioItem[]` | required | `{ label, value, description?, disabled? }` options. |
| `orientation` | `'horizontal' \| 'vertical'` | `'vertical'` | Option layout. |

#### `Switch.svelte` — bits-ui
On/off preference control.

| Attribute | Type | Default | Description |
|---|---|---|---|
| `label` | `string` | required | Switch label. |
| `checked` | `boolean` | `false` | Bindable state. |
| `disabled` | `boolean` | `false` | Disables interaction. |
| `description` | `string` | `undefined` | Supporting text. |

### 5. Disclosure and feedback

#### `Accordion.svelte` — bits-ui
Single or multiple expandable content sections.

| Attribute | Type | Default | Description |
|---|---|---|---|
| `items` | `AccordionItem[]` | required | `{ value, title, content, disabled? }` items. |
| `type` | `'single' \| 'multiple'` | `'single'` | Expansion mode. |
| `collapsible` | `boolean` | `true` | Allows all items to close in single mode. |
| `defaultValue` | `string \| string[]` | `undefined` | Initially expanded item(s). |

#### `Tabs.svelte` — bits-ui
Tabbed content with responsive overflow behavior.

| Attribute | Type | Default | Description |
|---|---|---|---|
| `items` | `TabItem[]` | required | `{ value, label, content }` tabs. |
| `value` | `string` | `undefined` | Bindable active tab. |
| `orientation` | `'horizontal' \| 'vertical'` | `'horizontal'` | Tab layout. |
| `activation` | `'automatic' \| 'manual'` | `'automatic'` | Keyboard activation behavior. |

#### `Alert.svelte`
Inline informational, success, warning, or error message.

| Attribute | Type | Default | Description |
|---|---|---|---|
| `tone` | `'info' \| 'success' \| 'warning' \| 'danger'` | `'info'` | Semantic alert tone. |
| `title` | `string` | `undefined` | Optional strong label. |
| `dismissible` | `boolean` | `false` | Shows a close action. |
| `onDismiss` | `() => void` | `undefined` | Dismiss callback. |
| `children` | `Snippet` | required | Alert message. |

#### `Tooltip.svelte` — bits-ui
Non-essential contextual hint for controls and icons.

| Attribute | Type | Default | Description |
|---|---|---|---|
| `content` | `string` | required | Tooltip text. |
| `side` | `'top' \| 'right' \| 'bottom' \| 'left'` | `'top'` | Preferred placement. |
| `delay` | `number` | `300` | Open delay in milliseconds. |

#### `Modal.svelte` — bits-ui
Dialog for confirmation, forms, and focused content.

| Attribute | Type | Default | Description |
|---|---|---|---|
| `open` | `boolean` | `false` | Bindable open state. |
| `title` | `string` | required | Dialog title. |
| `description` | `string` | `undefined` | Dialog description. |
| `closeOnOutsideClick` | `boolean` | `true` | Outside-click behavior. |
| `children` | `Snippet` | required | Dialog body. |
| `footer` | `Snippet` | `undefined` | Action area. |

### 6. Data and utility components

#### `CodeBlock.svelte`
Terminal/code presentation with copy action.

| Attribute | Type | Default | Description |
|---|---|---|---|
| `code` | `string` | required | Code contents. |
| `language` | `string` | `'text'` | Display language label. |
| `filename` | `string` | `undefined` | Optional file label. |
| `copyable` | `boolean` | `true` | Shows copy control. |

#### `Pagination.svelte`
Navigation for paged collections.

| Attribute | Type | Default | Description |
|---|---|---|---|
| `page` | `number` | `1` | Bindable current page. |
| `totalPages` | `number` | required | Total page count. |
| `href` | `(page: number) => string` | `undefined` | Optional URL generator. |
| `label` | `string` | `'Pagination'` | Accessible navigation label. |

## Showcase page structure

The new `/components` route should present the library as a living reference page in this order:

1. Hero: brand mark, short design-system description, and font preview.
2. Brand identity and color tokens.
3. Typography scale and spacing/radius/shadow tokens.
4. Buttons, icon buttons, links, and badges.
5. Cards and content surfaces.
6. Text inputs, select, checkbox, radio group, and switch.
7. Accordion, tabs, tooltip, modal, and alerts.
8. Code block and pagination.
9. Responsive behavior notes and accessibility states.

Each section should show the rendered example beside a compact API summary. The page itself should use the same components it documents wherever practical.

## Suggested implementation order

1. Theme tokens and typography in `src/routes/theme.css`.
2. `Button`, `Link`, `Badge`, `Card`, and `Divider`.
3. `TextInput`, `Select`, `Checkbox`, `RadioGroup`, and `Switch`.
4. `Accordion`, `Tabs`, `Alert`, `Tooltip`, and `Modal` using `bits-ui`.
5. `BrandMark`, `SiteHeader`, `PageShell`, and `SectionHeader`.
6. `/components` showcase route and responsive polish.
7. Component tests and keyboard/accessibility review.
