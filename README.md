# GitHub Contribution Snake 🐍

An animated snake that eats your GitHub contributions - **built from scratch!**

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/Tailwind-Stocker/contribution-snake/output/github-contribution-grid-snake.gif">
  <source media="(prefers-color-scheme: light)" srcset="https://raw.githubusercontent.com/Tailwinf-Stocker/contribution-snake/output/github-contribution-grid-snake-light.gif">
  <img alt="GitHub Contribution Snake" src="https://raw.githubusercontent.com/Tailwinf-Stocker/contribution-snake/output/github-contribution-grid-snake-light.gif">
</picture>

## What does this do?

This project automatically generates an animated snake that moves through your GitHub contribution graph, "eating" your contributions as it goes. The snake animation is updated automatically every 12 hours and can be embedded in your GitHub profile README.

**🔥 Custom Implementation**: This uses a custom Python script (not external actions) to fetch your GitHub contributions via the GraphQL API and generate the snake animation from scratch!

## Features

- 🐍 **Custom-built snake animation** (no external dependencies!)
- 📊 **Real GitHub data** via GraphQL API
- 🌙 **Automatic theme switching** (light/dark mode support)
- 🎨 **Multiple formats** (SVG and GIF for both themes)
- ⚡ **Auto-updates** every 6 hours
- 📱 **Responsive design**
- 🔧 **Fully customizable** colors and behavior

## How It Works

1. **Fetches Data**: Uses GitHub GraphQL API to get your contribution calendar
2. **Processes Grid**: Converts raw data into a structured contribution grid
3. **Generates Path**: Creates a zigzag path for the snake to follow
4. **Creates Animation**: Renders SVG and GIF animations with the snake eating contributions
5. **Auto-deploys**: Pushes generated files to GitHub Pages

## Setup Instructions

### 1. Fork or Create Repository

1. Fork this repository or create a new repository with the same structure
2. Make sure the repository is public (required for GitHub Pages)

### 2. Enable GitHub Actions

1. Go to your repository settings
2. Navigate to "Actions" → "General"
3. Under "Actions permissions", select "Allow all actions and reusable workflows"

### 3. Enable GitHub Pages

1. Go to your repository settings
2. Navigate to "Pages"
3. Under "Source", select "Deploy from a branch"
4. Select branch: `output` and folder: `/ (root)`
5. Click "Save"

### 4. Run the Action

1. Go to the "Actions" tab in your repository
2. Click on "Generate Snake Animation"
3. Click "Run workflow" → "Run workflow"
4. Wait for the workflow to complete (usually takes 1-2 minutes)

### 5. Add to Your Profile

Add this to your GitHub profile README.md for **automatic theme switching**:

```markdown
<picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/YOUR_USERNAME/YOUR_REPOSITORY_NAME/output/github-contribution-grid-snake-dark.svg">
  <source media="(prefers-color-scheme: light)" srcset="https://raw.githubusercontent.com/YOUR_USERNAME/YOUR_REPOSITORY_NAME/output/github-contribution-grid-snake.svg">
  <img alt="GitHub Contribution Snake" src="https://raw.githubusercontent.com/YOUR_USERNAME/YOUR_REPOSITORY_NAME/output/github-contribution-grid-snake.svg">
</picture>
```

**For GIF animations with theme switching:**

```markdown
<picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/YOUR_USERNAME/YOUR_REPOSITORY_NAME/output/github-contribution-grid-snake.gif">
  <source media="(prefers-color-scheme: light)" srcset="https://raw.githubusercontent.com/YOUR_USERNAME/YOUR_REPOSITORY_NAME/output/github-contribution-grid-snake-light.gif">
  <img alt="GitHub Contribution Snake" src="https://raw.githubusercontent.com/YOUR_USERNAME/YOUR_REPOSITORY_NAME/output/github-contribution-grid-snake-light.gif">
</picture>
```

**For static theme (light mode only):**

```markdown
![Snake Animation](https://raw.githubusercontent.com/YOUR_USERNAME/YOUR_REPOSITORY_NAME/output/github-contribution-grid-snake.svg)
```

**For static theme (dark mode only):**

```markdown
![Snake Animation](https://raw.githubusercontent.com/YOUR_USERNAME/YOUR_REPOSITORY_NAME/output/github-contribution-grid-snake-dark.svg)
```

**Replace:**
- `YOUR_USERNAME` with your GitHub username
- `YOUR_REPOSITORY_NAME` with the name of this repository

## Local Testing

You can test the snake generation locally before deploying:

1. **Install Python dependencies**:
   ```bash
   pip install -r requirements.txt
   ```

2. **Set environment variables**:
   ```bash
   export GITHUB_USERNAME=your_username
   export GITHUB_TOKEN=your_personal_access_token
   ```

3. **Run the test script**:
   ```bash
   python test_local.py
   ```

4. **Check output**: Look in the `dist/` folder for generated files

### Getting a GitHub Token

1. Go to [GitHub Settings > Developer settings > Personal access tokens](https://github.com/settings/tokens)
2. Click "Generate new token (classic)"
3. Give it a name and select the `read:user` scope
4. Copy the token and use it as `GITHUB_TOKEN`

## Customization

### Colors

You can customize colors by modifying the `scripts/generate_snake.py` file:

```python
self.colors = {
    'background': '#0d1117',      # Background color
    'grid': '#21262d',            # Grid line color
    'levels': [                   # Contribution level colors (light to dark)
        '#161b22',                # No contributions
        '#0e4429',                # Low contributions
        '#006d32',                # Medium contributions  
        '#26a641',                # High contributions
        '#39d353'                 # Very high contributions
    ],
    'snake': '#f85149',           # Snake body color
    'snake_head': '#ff6b6b'       # Snake head color
}
```

### Snake Behavior

Modify the `create_snake_path()` method to change how the snake moves:
- **Zigzag pattern** (default): Alternates direction each column
- **Spiral pattern**: Could spiral inward/outward
- **Random walk**: Random movement through high-contribution areas

### Schedule

The snake updates every 6 hours by default. To change this, modify the cron schedule in the workflow:

```yaml
schedule:
  - cron: "0 */6 * * *"  # Every 6 hours (default)
  - cron: "0 */12 * * *" # Every 12 hours
  - cron: "0 0 * * *"    # Daily at midnight
```

## Output Files

The action generates four files:

1. **github-contribution-grid-snake.svg** - Light theme SVG animation
2. **github-contribution-grid-snake-dark.svg** - Dark theme SVG animation  
3. **github-contribution-grid-snake-light.gif** - Light theme GIF animation
4. **github-contribution-grid-snake.gif** - Dark theme GIF animation

## Troubleshooting

### Action Fails
- Ensure your repository is public
- Check that GitHub Actions are enabled
- Verify the workflow file syntax

### Snake Doesn't Show
- Wait for the action to complete (check Actions tab)
- Ensure GitHub Pages is enabled with `output` branch
- Check that the image URL in your README is correct

### No Contributions Visible
- The snake uses your public GitHub contributions
- Private repository contributions won't be visible
- Make sure you have some contributions in the current year

## Advanced Usage

### Manual Trigger

You can manually trigger the snake generation:

1. Go to Actions tab
2. Select "Generate Snake Animation"
3. Click "Run workflow"

### Use Different User

To generate a snake for a different user, modify the workflow:

```yaml
github_user_name: different-username
```

## Credits

This is a **custom implementation** built from scratch using:
- **Python** for the core logic
- **GitHub GraphQL API** for contribution data
- **Pillow (PIL)** for GIF generation
- **svgwrite** for SVG animation
- **GitHub Actions** for automation

Inspired by the original [Platane/snk](https://github.com/Platane/snk) project, but built completely from scratch for full customization!

## License

MIT License - feel free to use this for your own profile!

---

⭐ **Star this repository if it helped you create an awesome GitHub profile!**
