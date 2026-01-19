# Personal Website - Hugo

This is a minimalist personal website built with [Hugo](https://gohugo.io/), inspired by the clean designs of [Jan Leike](https://jan.leike.name/), [John Schulman](http://joschu.net/), and [Jiaxin Wen](https://jiaxin-wen.github.io/).

## Quick Start

### Local Development

1. Install Hugo (if not already installed):
   ```bash
   brew install hugo
   ```

2. Start the development server:
   ```bash
   hugo server --port 3000
   ```

3. Open your browser at `http://localhost:3000`

### Build for Production

```bash
hugo
```

The static site will be generated in the `public/` directory.

## Project Structure

```
personal-website-hugo/
├── content/          # Content files (markdown)
│   ├── about.md
│   ├── publications.md
│   └── posts/        # Blog posts
├── themes/
│   └── minimal/      # Custom minimalist theme
│       ├── layouts/  # HTML templates
│       ├── static/   # CSS, images, etc.
│       └── css/
│           └── style.css
└── hugo.toml         # Hugo configuration
```

## Features

- **Minimalist Design**: Clean, simple, and focused on content
- **Fast**: Built with Hugo (Go), extremely fast build times
- **Responsive**: Works great on mobile and desktop
- **Easy to Maintain**: Simple file structure, no complex dependencies

## Migration from Jekyll

This site was migrated from Jekyll to Hugo for better performance and simpler maintenance. All content has been preserved.

## Deployment

### GitHub Pages

1. Build the site: `hugo`
2. Push the `public/` directory to the `gh-pages` branch, or use GitHub Actions

### Other Platforms

Hugo generates static HTML files that can be deployed to any static hosting service:
- Netlify
- Vercel
- Cloudflare Pages
- AWS S3 + CloudFront

## License

All original textual content is licensed under the [Creative Commons Attribution-NonCommercial-NoDerivatives 4.0 International License](http://creativecommons.org/licenses/by-nc-nd/4.0/).
