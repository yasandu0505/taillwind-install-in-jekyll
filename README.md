# 🎨 Installing Tailwind CSS in Jekyll

A comprehensive guide to integrate Tailwind CSS into your Jekyll project for a modern, utility-first styling experience.

## 📋 Prerequisites

- Node.js (v14 or higher)
- Jekyll project already set up
- Basic knowledge of CSS and Jekyll

## 🚀 Installation Steps

### 1️⃣ Install Tailwind CSS

Install the stable version 3.x with typography plugin:

```bash
npm install -D tailwindcss@^3.4.0 @tailwindcss/typography
```

### 2️⃣ Initialize Tailwind Configuration

Generate the Tailwind configuration file:

```bash
npx tailwindcss init
```

### 3️⃣ Create Input CSS File

⚠️ **Important**: If you already have a `style.css` file in `assets/css/`, rename it to `custom_styles.css` (or any other name) and update your imports accordingly.

```bash
mkdir -p assets/css
echo "@tailwind base; @tailwind components; @tailwind utilities;" > assets/css/input.css
```

### 4️⃣ Configure Tailwind

Update your `tailwind.config.js` file to scan your Jekyll files:

```javascript
/** @type {import('tailwindcss').Config} */
module.exports = {
  content: [
    "./_layouts/**/*.html",
    "./_includes/**/*.html", 
    "./_posts/**/*.md",
    "./_pages/**/*.md",
    "./index.html",
    "./**/*.html"
  ],
  theme: {
    extend: {
      colors: {
        primary: {
          50: '#eff6ff',
          500: '#3b82f6',
          600: '#2563eb',
          700: '#1d4ed8',
        }
      },
      fontFamily: {
        'sans': [
          'SF Pro Display', 
          '-apple-system', 
          'BlinkMacSystemFont', 
          'Segoe UI', 
          'Roboto', 
          'Helvetica Neue', 
          'Arial', 
          'sans-serif'
        ],
      }
    }
  },
  plugins: [
    require('@tailwindcss/typography'),
  ],
}
```

### 5️⃣ Build Tailwind CSS

Generate the compiled CSS file:

```bash
npx tailwindcss -i ./assets/css/input.css -o ./assets/css/style.css --minify
```

### 6️⃣ Update Your Layout

Replace the Tailwind CDN link in your `_layouts/default.html` (or main layout file):

**Remove this:**
```html
<script src="https://cdn.tailwindcss.com"></script>
```

**Add this:**
```html
<!-- Tailwind CSS (built version) -->
<link rel="stylesheet" href="{{ '/assets/css/style.css' | relative_url }}">
```

### 7️⃣ Test Your Setup

Start your Jekyll development server:

```bash
bundle exec jekyll serve
```

Visit `http://localhost:4000` and test some Tailwind classes to ensure everything works!

### 8️⃣ Commit Your Changes

Save your progress to Git:

```bash
git add .
git commit -m "Replace Tailwind CDN with built CSS for production"
git push origin [your-branch]
```

## 🔄 Development Workflow

### Watch Mode for Development

For automatic CSS rebuilding during development, you can run Tailwind in watch mode:

```bash
npx tailwindcss -i ./assets/css/input.css -o ./assets/css/style.css --watch
```

### Build Script

Add these scripts to your `package.json` for easier development:

```json
{
  "scripts": {
    "build-css": "tailwindcss -i ./assets/css/input.css -o ./assets/css/style.css --minify",
    "watch-css": "tailwindcss -i ./assets/css/input.css -o ./assets/css/style.css --watch",
    "dev": "bundle exec jekyll serve & npm run watch-css"
  }
}
```

## 🎯 Pro Tips

### Custom Styles
If you need custom CSS alongside Tailwind, create a `custom.css` file and import it in your `input.css`:

```css
@tailwind base;
@tailwind components;
@tailwind utilities;

@import 'custom.css';
```

### Typography Plugin
The `@tailwindcss/typography` plugin adds beautiful typographic defaults. Use it with the `prose` class:

```html
<article class="prose lg:prose-xl mx-auto">
  {{ content }}
</article>
```

### Dark Mode Support
Enable dark mode in your `tailwind.config.js`:

```javascript
module.exports = {
  darkMode: 'class', // or 'media'
  // ... rest of config
}
```

## 🐛 Troubleshooting

### CSS Not Updating?
- Make sure to rebuild CSS after changes: `npm run build-css`
- Check that your file paths in `content` array are correct
- Ensure Jekyll is serving the correct CSS file

### Classes Not Working?
- Verify the class exists in Tailwind CSS documentation
- Check if you need to rebuild your CSS
- Make sure your HTML files are in the `content` paths

### Performance Issues?
- Always use `--minify` flag for production builds
- Consider purging unused CSS with the `content` configuration
- Use the built CSS instead of CDN for better performance

## 📚 Next Steps

1. **Learn Tailwind**: Check out the [official documentation](https://tailwindcss.com/docs)
2. **Customize**: Extend your theme in `tailwind.config.js`
3. **Components**: Create reusable components with `@apply` directive
4. **Plugins**: Explore additional Tailwind plugins for forms, aspect-ratio, etc.

## 🤝 Contributing

Found an issue or want to improve this guide? Feel free to open an issue or submit a pull request!

---

**Happy styling with Tailwind CSS and Jekyll!** 🎉
<p align="center">
  Made with ❤️ by <strong>Yasii</strong>
</p>