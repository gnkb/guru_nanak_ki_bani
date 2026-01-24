## How is this site put together

This site is put together using Hugo. Hugo is installed on windows via Chocolatey. The theme is hugo-book, which can be viewed in the hugo.toml.

The site contents are in content/essays

I use a github build pipeline to compile the markdown files in content/essays into the static html files

## Installing Hugo on Windows

### Option 1: Using Chocolatey (Recommended)
1. Install Chocolatey if you haven't already:
   - Open PowerShell as Administrator
   - Run: `Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.WebClient]::new().DownloadString('https://chocolatey.org/install.ps1') | iex`

2. Install Hugo:
   ```powershell
   choco install hugo -confirm
   ```

3. Verify installation:
   ```powershell
   hugo version
   ```

### Option 2: Using Scoop
1. Install Scoop if you haven't already:
   ```powershell
   Set-ExecutionPolicy RemoteSigned -Scope CurrentUser
   irm get.scoop.sh | iex
   ```

2. Install Hugo:
   ```powershell
   scoop install hugo
   ```

### Option 3: Manual Download
1. Download the latest Hugo release from: https://github.com/gohugoio/hugo/releases
2. Choose the Windows version (hugo_X.XX.X_Windows-64bit.zip)
3. Extract the zip file and add the `hugo.exe` to your PATH

## Setting up a Local Hugo Server for Testing

To test changes locally before deploying, you can run Hugo's built-in development server:

1. Navigate to your project directory:
   ```powershell
   cd c:\src\gnkb
   ```

2. Start the development server:
   ```powershell
   hugo server
   ```

3. Open your browser and go to `http://localhost:1313`

The server will automatically rebuild and refresh when you make changes to your content or configuration files.

### Useful Hugo Server Options:
- `hugo server -D` - Include draft pages in the build
- `hugo server --bind 0.0.0.0` - Bind to all network interfaces (accessible from other devices)
- `hugo server --port 8080` - Use a different port

## How Hugo Works

Hugo is a static site generator written in Go. Here's how it processes your content:

### Core Concepts:
- **Content**: Markdown files in the `content/` directory are processed into HTML
- **Templates**: Layout files in `layouts/` and `themes/` define how content is rendered
- **Configuration**: `hugo.toml` (or `config.toml`) contains site-wide settings
- **Themes**: Reusable templates and assets (this site uses the hugo-book theme)

### Build Process:
1. Hugo reads your configuration file (`hugo.toml`)
2. It scans the `content/` directory for Markdown files
3. Each Markdown file is converted to HTML using templates
4. Static assets (CSS, JS, images) are copied to the output directory
5. The final static site is generated in the `public/` directory

### Key Directories:
- `content/` - Your Markdown content files
- `layouts/` - Custom templates (overrides theme templates)
- `static/` - Static assets (images, CSS, JS)
- `themes/` - Theme files (hugo-book theme)
- `public/` - Generated static site (created during build)

### Front Matter:
Each content file starts with YAML/TOML front matter containing metadata:
```yaml
---
title: "Page Title"
date: 2024-01-01
draft: false
---
```

### Shortcodes:
Hugo supports shortcodes for reusable content snippets. This site uses www.statcounter.com for analytics, provided by StatCounter, and a contact form supplied by Elfsite.

For more information, visit the official Hugo documentation: https://gohugo.io/

## Project Structure

```
gnkb/
├── archetypes/          # Content templates for new pages
├── assets/             # SCSS/Sass files and other assets
├── content/            # Markdown content files
│   ├── _index.md       # Homepage content
│   └── essays/         # Essay content organized by topic
├── data/               # Data files (JSON, YAML) for site data
├── i18n/               # Internationalization files
├── layouts/            # Custom layout templates
├── public/             # Generated static site (auto-created)
├── resources/          # Processed assets (auto-created)
├── static/             # Static assets (images, CSS, JS), CNAME file for custom domain configuration
│   └── images/         # Site images
└── themes/             # Hugo themes
    └── hugo-book/      # The hugo-book theme
```

## Adding New Content

### Creating a New Essay

1. Create a new Markdown file in `content/essays/`:
   ```powershell
   hugo new essays/your-essay-title.md
   ```

2. Edit the generated file with your content. The front matter should include:
   ```yaml
   ---
   title: "Your Essay Title"
   description: "Brief description of the essay"
   date: 2026-01-19
   lastmod: 2026-01-19
   slug: "your-essay-slug"
   weight: 1000  # Controls display order (lower = higher priority)
   tags: ["tag1", "tag2"]
   categories: ["Sikh Philosophy"]
   keywords: ["keyword1", "keyword2"]
   draft: false
   ---
   ```

3. Write your essay content in Markdown format below the front matter.

### Content Organization

- **Essays**: Main content goes in `content/essays/`
- **Categories**: Use `categories: ["Sikh Philosophy"]` for grouping
- **Tags**: Use tags for cross-referencing related content
- **Weight**: Lower weight numbers appear first in lists
- **Draft**: Set `draft: true` to exclude from production builds

## Deployment

This site uses GitHub Actions for automated deployment:

1. **Push to main branch**: Triggers automatic build and deployment
2. **Build process**: Hugo compiles Markdown to static HTML in `public/`
3. **Deployment**: Static files are deployed to the hosting platform

### Manual Build

To build the site manually:
```powershell
hugo  # Generates static files in public/
```

To build with drafts included:
```powershell
hugo -D
```

## Theme Customization (Hugo Book)

This site uses the [Hugo Book theme](https://themes.gohugo.io/themes/hugo-book/). Key configuration options in `hugo.toml`:

- **Book Menu**: Configure the left sidebar menu
- **Search**: Built-in search functionality
- **Code Highlighting**: Syntax highlighting for code blocks
- **Comments**: Integration with comment systems

### Customizing the Theme

1. **Override templates**: Add custom layouts in `layouts/` directory
2. **Custom CSS**: Add styles in `assets/css/` or `static/css/`
3. **Theme parameters**: Modify theme behavior in `hugo.toml`

## Contributing

### Content Guidelines

1. **Front Matter**: Always include complete front matter for each essay
2. **Markdown**: Use standard Markdown syntax
3. **Images**: Place images in `static/images/` and reference as `/images/filename.jpg`
4. **Links**: Use relative links for internal content
5. **Proofreading**: Ensure content is well-written and accurate

### Development Workflow

1. Create a new branch for changes
2. Test locally with `hugo server`
3. Commit changes with descriptive messages
4. Push to GitHub (triggers automated deployment)

## Troubleshooting

### Common Issues

**Site doesn't build:**
- Check for YAML/TOML syntax errors in front matter
- Ensure all required fields are present
- Verify file paths and links

**Content not appearing:**
- Check if `draft: true` is set
- Verify weight and date settings
- Ensure file is in correct directory (`content/essays/`)

**Styling issues:**
- Clear browser cache
- Check for CSS conflicts
- Verify theme configuration

**Local server issues:**
- Ensure port 1313 is not in use
- Try different port: `hugo server --port 8080`
- Check firewall settings

### Getting Help

- Check Hugo documentation: https://gohugo.io/
- Hugo Book theme docs: https://themes.gohugo.io/themes/hugo-book/
- GitHub Issues: Report bugs or request features

## Requirements

- **Hugo**: Version 0.80.0 or later
- **Git**: For version control
- **Text Editor**: VS Code recommended for Markdown editing
- **Browser**: Modern browser for testing

## License

[Add your license information here]