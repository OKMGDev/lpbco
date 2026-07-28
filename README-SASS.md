# SASS Setup for Shopify Theme

This theme now supports SASS/SCSS for better CSS organization and development.

## Setup

1. **Install dependencies:**
   ```bash
   npm install
   ```

2. **Start development with watch mode:**
   ```bash
   npm run sass:dev
   ```
   This will:
   - Watch for changes in `src/scss/`
   - Compile to `assets/`
   - Generate source maps for debugging
   - Use expanded CSS output

3. **Build for production:**
   ```bash
   npm run sass:build
   ```
   This will:
   - Compile all SCSS files
   - Minify CSS (compressed)
   - No source maps

4. **Watch mode (simple):**
   ```bash
   npm run sass
   ```
   Basic watch without source maps

## File Structure

```
src/scss/
├── main.scss              # Main entry point
├── _variables.scss        # SASS variables
├── _base.scss            # Base styles
├── _utilities.scss       # Utility classes
├── components/
│   ├── _header.scss
│   └── _footer.scss
└── sections/
    └── _collection-list.scss
```

## Usage

1. **Write your SCSS in `src/scss/`**
2. **Use files in `main.scss`** using `@use` (modern SASS syntax)
3. **Files compile to `assets/main.css`**
4. **Reference in Liquid files:**
   ```liquid
   {{ 'main.css' | asset_url | stylesheet_tag }}
   ```

### Modern SASS Syntax

This project uses the modern `@use` and `@forward` syntax instead of deprecated `@import`:

- **`@use 'file'`** - Loads a module once
- **`@use 'file' as *`** - Loads without namespace (for variables)
- **`@forward 'file'`** - Re-exports a module's variables/mixins/functions

## Converting Existing CSS

To convert existing CSS files to SCSS:

1. Copy CSS from `assets/base.css` to `src/scss/_base.scss`
2. Update `main.scss` to import it
3. Start using SASS features (variables, nesting, mixins)
4. Run `npm run sass:dev` to compile

## SASS Features You Can Use

- **Variables:** `$primary-color: #252831;` (use `@use 'variables' as *;` to access)
- **Nesting:** 
  ```scss
  .header {
    .logo { ... }
  }
  ```
- **Mixins:** Reusable style blocks
- **Partials:** Files starting with `_` are not compiled separately
- **Functions:** Built-in and custom functions
- **Operators:** Math operations

### Using Variables in Your Files

To use variables from `_variables.scss` in any file:

```scss
@use '../variables' as *;  // Use 'as *' to access variables without namespace

.my-class {
  color: $color-night-sky;
  padding: $spacing-md;
}
```

Or with namespace:

```scss
@use '../variables' as vars;

.my-class {
  color: vars.$color-night-sky;
  padding: vars.$spacing-md;
}
```

## Notes

- Shopify doesn't natively support SCSS, so you must compile to CSS
- Compiled CSS files go in `assets/` folder
- Keep your SCSS source files in `src/scss/`
- Don't edit compiled CSS files directly - edit SCSS and recompile

