# Netflix Portfolio Template

A Netflix-inspired, open-source portfolio template built with **HTML, CSS, and vanilla JavaScript**. Turn your professional story into a streaming-style experience: click your name to start the intro, choose a profile, browse career collections, and open a cinematic video preview.

**No backend. No build step. No production dependencies. MIT licensed.**

[Create your own copy](https://github.com/shivam-aggarwal-git/netflix-portfolio-template/generate) · [Configuration](config.js) · [Media provenance](MEDIA.md) · [License](LICENSE)

![Profile selection preview](docs/profiles.png)

## Contents

- [Features](#features)
- [Requirements](#requirements)
- [Quick start with GitHub CLI](#quick-start-with-github-cli)
- [Use the GitHub website instead](#use-the-github-website-instead)
- [Run locally](#run-locally)
- [Customize your portfolio](#customize-your-portfolio)
- [Add your resume and logos](#add-your-resume-and-logos)
- [Customize intro, sound, and video](#customize-intro-sound-and-video)
- [Deploy to GitHub Pages](#deploy-to-github-pages)
- [Publish future updates](#publish-future-updates)
- [Project structure](#project-structure)
- [Testing](#testing)
- [Troubleshooting](#troubleshooting)
- [License and media](#license-and-media)
- [Contributing](#contributing)

## Features

- Four configurable profiles: Recruiter, Hiring Manager, Tech Enthusiast, and Stalker.
- Click-to-start name zoom, original intro animation, and synchronized sound.
- Burgundy profile screen with bright profile tiles and a responsive mobile layout.
- Configurable hero slideshow, pause controls, and muted background video.
- A video-preview dialog with native playback, volume, and full-screen controls.
- Horizontal experience, expertise, achievement, credential, and education collections.
- Detail dialogs with Escape/outside dismissal and focus return.
- Credential filters generated from the categories in your configuration.
- Optional PDF resume, contact/social links, availability badges, and a coming-soon feature.
- Keyboard support, reduced-motion support, and data-saver considerations.
- Relative asset paths that work on GitHub Pages repository URLs.
- Generic examples only: no real resume, employment records, personal contact details, or organization logos.

## Requirements

For local preview, you need:

- **Git** to clone and update your repository.
- **Python 3** to run a small local static server.
- A modern browser and any text editor.
- A **GitHub account** to publish your copy.

**GitHub CLI (`gh`) is optional** and is used in the command-line quick start. Node.js and Playwright are needed only for the optional tests. You do not need npm, React, a database, API keys, or a paid service to run the website.

Check the tools you plan to use:

```sh
git --version
python3 --version
gh --version
```

## Quick start with GitHub CLI

Run these commands in the directory where you keep your projects. Replace `my-portfolio` if you want a different repository name.

```sh
# Sign in to your GitHub account, if you have not already.
gh auth login

# Create YOUR repository from this template and clone it locally.
gh repo create my-portfolio \
  --template shivam-aggarwal-git/netflix-portfolio-template \
  --public \
  --clone

cd my-portfolio

# Preview the unchanged template.
python3 -m http.server 4173 --bind 127.0.0.1
```

Open [http://127.0.0.1:4173/](http://127.0.0.1:4173/). Click **YOUR NAME** to start the intro, then choose a profile. Press **Ctrl+C** in the terminal to stop the server.

Your new repository belongs to your account and has its own history. Edit `config.js` before publishing your personal portfolio. Commands later in this README assume you are inside this new repository.

## Use the GitHub website instead

1. Open [this template repository](https://github.com/shivam-aggarwal-git/netflix-portfolio-template).
2. Select **Use this template → Create a new repository**.
3. Choose your account, enter a name such as `my-portfolio`, and create the repository. A public repository supports GitHub Pages on GitHub Free.
4. Clone **your new repository**, replacing `YOUR-USERNAME` below:

```sh
git clone https://github.com/YOUR-USERNAME/my-portfolio.git
cd my-portfolio
python3 -m http.server 4173 --bind 127.0.0.1
```

You can also edit files directly on GitHub if you do not want a local checkout.

## Run locally

From the repository root:

```sh
python3 -m http.server 4173 --bind 127.0.0.1
```

Visit [http://127.0.0.1:4173/](http://127.0.0.1:4173/). Save edits and refresh the browser to see them. This server does not provide live reload. Use HTTP preview rather than relying on double-clicking `index.html`, especially when testing video and file paths.

If port 4173 is busy:

```sh
python3 -m http.server 4174 --bind 127.0.0.1
```

Then open `http://127.0.0.1:4174/`.

## Customize your portfolio

Most changes belong in **[config.js](config.js)**. It is a JavaScript object, so keep quotes, commas, brackets, and braces intact. Replace the supplied examples with accurate information; examples are not real employment or credentials.

### 1. Set your identity and contact details

Edit the existing fields rather than adding a second `window.PORTFOLIO` object:

```js
name: "Alex Morgan",
role: "Product Engineer",
specialties: ["WEB APPLICATIONS", "PRODUCT DEVELOPMENT"],
about: "Write a concise introduction describing your actual work and interests.",
location: "Your city, country",
experienceLabel: "Your experience summary",
openToWork: true,
notice: "Serving notice period",
email: "hello@example.com",
linkedin: "https://www.linkedin.com/in/YOUR-PROFILE/",
github: "https://github.com/YOUR-USERNAME",
resume: "assets/resume.pdf",
demoMode: false,
```

These are example values. Use your own links and details. Empty `email`, `linkedin`, `github`, or `resume` fields hide their links. Set `openToWork: false` to remove the Open to work badge. Leave `notice: ""` to hide the notice-period badge.

The name, role, and about fields also update the page title, description, and Open Graph text. The first hero slide uses these identity fields; subsequent slides use the `slides` entries. Set `demoMode: false` after replacing the example content to remove the template-demo banner.

### 2. Add your career collections

| Configuration key | What it controls | Main record fields |
| --- | --- | --- |
| `experience` | Career journey | `title`, `role`, `date`, `location`, `tag`, `items`, optional `logo` |
| `expertise` | Skills and technical knowledge | `title`, `sub`, `description`, `color` |
| `achievements` | Verified outcomes | `title`, `sub`, `description`, `color` |
| `credentials` | Courses, certificates, and badges | `title`, `issuer`, `year`, `category`, `description`, optional `logo` |
| `education` | Degrees and qualifications | `title`, `sub`, `description`, optional `logo` |
| `interests` | Personal-interest chips | An array of strings |
| `labStories` | Longer personal-interest descriptions | `title`, `description` |

Example experience record:

```js
{
  title: "Your organization",
  role: "Your job title",
  date: "Your start date – Your end date",
  location: "Your work location",
  tag: "YOUR SPECIALTY",
  color: "blue",
  logo: "assets/logos/your-company.png",
  items: [
    "Describe a responsibility you held.",
    "Describe a result you can substantiate."
  ]
}
```

Example credential record:

```js
{
  title: "Your course or certification",
  issuer: "Your learning provider",
  year: "2026",
  category: "Professional learning",
  color: "cyan",
  logo: "assets/logos/your-provider.png",
  description: "Describe the credential you earned."
}
```

Records with the same credential `category` appear under the same filter. Available card color names are `blue`, `purple`, `cyan`, `gold`, `red`, and `slate`. Keep at least one profile and one slide in the configuration. Separate personal experiments from professional achievements, and include metrics only when you can support them.

### 3. Customize profiles and slideshow

A profile's `first` value selects which collection appears first:

```js
{
  name: "Recruiter",
  subtitle: "Experience & impact",
  first: "career",
  color: "#008fff"
}
```

Supported collection IDs are `career`, `expertise`, `achievements`, `knowledge`, and `education`. All collections remain accessible after profile selection.

For subsequent hero slides, edit the `title`, `subtitle`, `description`, and `image` fields in `slides`. Use `\n` in a title for a line break. Use relative image paths such as `assets/my-background.webp`.

For deeper visual changes, edit **styles.css**. Interaction behavior is in **app.js**.

## Add your resume and logos

No personal PDF or organization logos are included.

1. Copy your PDF to `assets/resume.pdf`.
2. Set `resume: "assets/resume.pdf"` in `config.js`.
3. Open the local preview and check View resume and Download resume.

On macOS/Linux, you can copy a PDF with:

```sh
cp "/path/to/your/resume.pdf" assets/resume.pdf
```

For logos:

```sh
mkdir -p assets/logos
cp "/path/to/your/company-logo.png" assets/logos/company.png
```

Then use `logo: "assets/logos/company.png"` on the relevant record. Add only media you are allowed to publish. GitHub Pages filenames are case-sensitive: `Company.png` and `company.png` are different paths.

Anything you commit to a public repository, including a resume PDF and contact details, becomes public. Review your own documents before adding them.

## Customize intro, sound, and video

| File | Purpose |
| --- | --- |
| `assets/intro.mp3` | Original standalone intro sound cue |
| `assets/intro.mp4` | Four-second opening background video; its audio is muted in the opening player |
| `assets/preview.mp4` | Twelve-second preview and muted hero background video; the preview has its own embedded audio |
| `assets/ai-core.webp` | Main background and collection artwork |
| `assets/ai-lab.webp` | Secondary hero artwork |

The visitor clicks their name to start the name zoom, opening video, and MP3 together. This deliberate gesture allows sound under normal browser autoplay restrictions. There is no separate Play Intro button. Skip, mute, Escape, and automatic completion are supported.

You can replace a file while preserving its name. Use MP4/H.264 for broad video compatibility and an MP3 for the separate sound cue. Keep the intro close to four seconds; if you change its length, update the completion timeout in `beginIntro()` in `app.js` and the `name-intro` animation duration in `styles.css`.

Replacing `intro.mp3` changes the name-click intro sound. It does **not** change the sound already embedded in `preview.mp4`; replace that video if you want a different preview soundtrack.

To keep loading fast, compress imagery to WebP and avoid large video files. The bundled videos are lightweight animations made from two AI images. See [MEDIA.md](MEDIA.md) for their origin and reuse terms.

## Deploy to GitHub Pages

### 1. Commit and push your personalized version

Check that the remote points to **your** repository:

```sh
git remote -v
git status
```

Then publish your edits:

```sh
git add index.html styles.css config.js app.js assets .nojekyll
git commit -m "Personalize my portfolio"
git push origin main
```

If you also edited the documentation, include those files in `git add`.

### 2. Enable Pages in GitHub settings

1. Open your new repository's **Settings → Pages**.
2. Under Source, select **Deploy from a branch**.
3. Choose **main** and **/ (root)**, then **Save**.
4. Open the **Actions** tab and wait for **pages build and deployment** to complete.
5. Return to Pages settings for the published URL.

For a repository named `my-portfolio`, the URL is:

```text
https://YOUR-USERNAME.github.io/my-portfolio/
```

A repository named `YOUR-USERNAME.github.io` uses the account's root Pages URL instead. Keep `.nojekyll`, `index.html`, `styles.css`, `config.js`, `app.js`, and `assets/` in the repository root.

### Optional: enable Pages using GitHub CLI

If Pages is not already enabled, you can use the API instead of the settings UI:

```sh
portfolio_repo="$(gh repo view --json nameWithOwner --jq '.nameWithOwner')"

gh api --method POST "repos/$portfolio_repo/pages" \
  -f 'source[branch]=main' \
  -f 'source[path]=/'

# Get the configured public URL.
gh api "repos/$portfolio_repo/pages" --jq '.html_url'

# Inspect recent deployment runs.
gh run list --limit 5
```

The POST command is for initial setup. If Pages is already enabled, use its existing settings rather than creating it again.

## Publish future updates

After editing the configuration or assets:

```sh
git status
git add config.js assets
git commit -m "Update portfolio content"
git push origin main
```

Include `index.html`, `styles.css`, or `app.js` in `git add` if you changed those too. Pushing to the configured Pages branch triggers a new deployment. Use the Actions tab to confirm success.

## Project structure

```text
.
├── index.html          # Semantic page structure
├── styles.css          # Layout, theme, and animations
├── config.js           # Your identity, collections, links, and slides
├── app.js              # Client-side rendering and interactions
├── .nojekyll            # Static GitHub Pages publishing
├── assets/
│   ├── ai-core.webp
│   ├── ai-lab.webp
│   ├── intro.mp3
│   ├── intro.mp4
│   └── preview.mp4
├── docs/profiles.png   # Generic README screenshot
├── tests/verify.cjs    # Optional browser smoke tests
├── MEDIA.md            # Media provenance and reuse terms
├── CONTRIBUTING.md
└── LICENSE
```

## Testing

Manually check the intro, profile selection, slides, carousel arrows, detail dialogs, resume links, contact links, and mobile navigation before sharing your site. Test at phone and desktop widths, including keyboard navigation and reduced motion.

Optional automated smoke tests require Node.js and Playwright. From the repository root:

```sh
npm install --no-save playwright
npx playwright install chromium
```

Start the server in one terminal:

```sh
python3 -m http.server 4173 --bind 127.0.0.1
```

Run tests from a second terminal in the same directory:

```sh
node tests/verify.cjs
```

For another local port on macOS/Linux:

```sh
BASE_URL=http://127.0.0.1:4174/ node tests/verify.cjs
```

The smoke suite assumes the default sample names and collection labels. Run it before personalizing, or update those assertions to match your configuration. Optional environment variable `CHROMIUM_PATH` selects an installed Chromium executable. Test dependencies are for development only; the published website does not use them.

## Troubleshooting

| Problem | What to check |
| --- | --- |
| No sound before clicking | Expected browser behavior. Click your name to begin the synchronized intro. |
| Changes do not appear | Save the file, refresh the browser, and confirm the latest Pages deployment succeeded. Try a hard refresh: Cmd+Shift+R on macOS or Ctrl+Shift+R on Windows/Linux. |
| Blank page or broken interactions | Look for a missing comma, quote, or bracket in `config.js`; inspect the browser console. |
| No resume/contact button | Set the relevant field in `config.js`; empty optional links are intentionally hidden. |
| Broken image, PDF, or video | Confirm the file exists, check exact filename capitalization, and use relative paths without a leading `/`. |
| GitHub Pages shows 404 | Check that `index.html` is at the selected branch's root and the deployment completed. |
| Still seeing YOUR NAME or the demo banner | Replace the example configuration and set `demoMode: false`. |
| Intro does not zoom or slideshow stays paused | Check the operating system's reduced-motion preference and the slideshow pause button. |
| Background video stays still | Reduced motion, data saver, a paused slideshow, an open dialog, or an offscreen hero can pause playback. The Preview player remains explicitly playable. |
| Git push fails | Verify `git remote -v`, authentication, and permissions for your own repository. |

## License and media

The project uses the **MIT License**. Retain the copyright and license notice when redistributing it. See [LICENSE](LICENSE).

The included original synthesized sound, AI artwork, and animation assembled from that artwork are offered for reuse under the same MIT terms to the extent rights can be granted. AI-generated imagery may not attract copyright protection in every jurisdiction; no exclusive rights or third-party clearance are promised. See [MEDIA.md](MEDIA.md).

**Netflix Portfolio Template is an independent project, not affiliated with or endorsed by Netflix.** No Netflix logo animation, Netflix sound recording, personal resume, or third-party organization logos are bundled. If you substitute media, check its redistribution permissions.

## Contributing

Bug fixes, accessibility improvements, and documentation updates are welcome. Read [CONTRIBUTING.md](CONTRIBUTING.md), open an issue to discuss larger changes, and submit a focused pull request describing the change and its validation.

Keep examples generic. Do not include personal resumes, real credential records, contact details, secrets, or media without redistribution rights in contributions.
