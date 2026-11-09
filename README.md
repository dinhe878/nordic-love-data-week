# Nordic Love Data Week

The public website for Nordic Love Data Week, an annual event promoting research data management, sharing, and literacy across the Nordic region. It is built with [Jekyll](https://jekyllrb.com/) and hosted on [GitHub Pages](https://pages.github.com/).

**Live site:** https://www.nordiclovedataweek.org/

## About the Event

Love Data Week is an international celebration of data, taking place every year during the week of Valentine's Day. Nordic Love Data Week is organized by a consortium of Nordic universities.

For more information about international activities, visit the [ICPSR event website](https://www.icpsr.umich.edu/sites/icpsr/about/news-events/international-love-data-week).

## Getting Started

### Prerequisites

This website is built with Jekyll, which requires [Ruby](https://www.ruby-lang.org). 

1. **Check if Ruby is installed:**
   ```bash
   ruby -v
   ```

2. **Install Ruby (if needed):**
   - **macOS (Apple Silicon M1/M2/M3):** Use Homebrew
     ```bash
     brew install ruby
     export PATH="/opt/homebrew/opt/ruby/bin:$PATH"  # Add to ~/.zshrc
     ```
   - **macOS (Intel):** 
     ```bash
     brew install ruby
     export PATH="/usr/local/opt/ruby/bin:$PATH"  # Add to ~/.zshrc
     ```
   - **Linux:** Follow the [Ruby installation docs](https://www.ruby-lang.org/en/documentation/installation/)
   - **Windows:** Install [RubyInstaller](https://rubyinstaller.org/) or use [Windows Subsystem for Linux](https://docs.microsoft.com/en-us/windows/wsl/)

### Local Development Setup

1. **Clone the repository:**
   ```bash
   git clone https://github.com/dinhe878/nordic-love-data-week.git
   cd nordic-love-data-week
   ```

2. **Create a Python virtual environment (optional, for data-related scripts):**
   ```bash
   python3 -m venv .venv
   source .venv/bin/activate  # On Windows: .venv\Scripts\activate
   ```

3. **Install Bundler:**
   ```bash
   gem install bundler
   ```

4. **Install Jekyll and dependencies:**
   ```bash
   bundle install
   ```
   
5. **Run the local development server:**
   ```bash
   bundle exec jekyll serve
   ```
   
   Then visit: [http://127.0.0.1:4000](http://127.0.0.1:4000)

6. **Check the build:**
   ```bash
   bundle exec jekyll build
   ```

   If you modify `_config.yml`, restart the development server (Ctrl+C, then re-run `bundle exec jekyll serve`).

## Editing the Website

This is a Jekyll website using [Kramdown](https://kramdown.gettalong.org/quickref.html) Markdown and [Liquid](https://shopify.github.io/liquid/) templates.

### Key Configuration File: `_config.yml`

Main settings to update:

- **`title`** - Site title used in title bar and various places
- **`nav_title`** - Site name and strapline in the top navigation
- **`event_date`** - Event dates (displayed throughout the site)
- **`event_year`** - Current event year, used to identify archive pages
- **`author`** - Primary contact/organizing institution
- **`mailbox_address`** - Contact email address (recommended: shared mailbox)
- **`description`** - Short event description (used by search engines and social media)
- **`url`** - Published site URL (without trailing slash)
- **`github_repo`** - GitHub repository name
- **`event_status`** - Controls page visibility based on event timeline (`soon`, `now`, `over`, `demo`)
- **`registration_status`** - Controls the form link on the disabled registration template (`soon`, `open`, `closed`, `demo`)
- **`team`** - Team members with names, emails, images, affiliations, and social links

### Content Pages

Key pages to customize:

- **`index.md`** - Homepage/landing page
- **`agenda.md`** - Current event schedule
- **`registration.md`** - Disabled registration page template; excluded from the build
- **`activities.md`** - Global activities; currently contains 2026 content
- **`about.md`** - Information about the event and organizing team
- **`videos-slides.md`** - Event recordings and presentation slides; currently contains 2026 content
- **`where-is-the-data-day.md`** - Where's the Data Day; currently contains 2026 content
- **`2026/`** - Archived 2026 event pages
- **`code-of-conduct.md`** - Event code of conduct
- **`faq.md`** - Frequently asked questions

### Enabling a registration page

The site does not currently use a central registration page. `registration.md` is retained as a template but excluded from the Jekyll build and navigation; individual events can still link to their own registration pages.

If central registration is needed in a future year:

1. Update `registration.md` with the current event details and replace its placeholder form URL with a real, tested link. Review what the form collects and its privacy and data-retention arrangements.
2. Remove `registration.md` from `exclude` in `_config.yml`, and add it to `header_pages` if it should appear in navigation.
3. Set `registration_status` to `soon`, `open`, or `closed` as appropriate. The page's `event_status` front matter also controls when it appears in the navigation; update it if needed.
4. Build and preview the site, checking the page and form link before publishing.

### Assets

- **`assets/logo.png`** - Logo displayed in the top navigation bar
- **`assets/`** - Images, PDFs, stylesheets, and other shared or event-specific files
- **Team member images** - Store profile photos in `assets/` (referenced in `_config.yml`)

### Adding Team Members

Edit the `team` list in `_config.yml`:

```yaml
team:
  - name: Team Member Name
    email: email@example.com
    image: /assets/member-photo.jpg
    affiliation: University Name
    title: Position/Role
    links:
      - title: Website
        url: https://example.com
        icon: bi-globe2
      - title: GitHub
        url: https://github.com/username
        icon: bi-github
```

Team members are automatically displayed on the `about.md` page.

### Adding Navigation Pages

1. Create a new Markdown file in an appropriate location
2. Add front matter with `menu_title` and `menu_icon` (Bootstrap Icons):
   ```markdown
   ---
   title: Page Title
   menu_title: Nav Label
   menu_icon: icon-name
   ---
   ```
3. Add the source path to `header_pages` in `_config.yml`

### Useful Liquid Tags

- **Reference config variables:** `{{ site.event_date }}`
- **Link to pages:** `[Link text]({{ site.baseurl }}{% link page-name.md %})`
- **Loop through team members:** 
  ```liquid
  {% for member in site.team %}
    {{ member.name }} - {{ member.affiliation }}
  {% endfor %}
  ```

See [Jekyll Liquid documentation](https://jekyllrb.com/docs/liquid/) for more.

## Contributing and Publishing

The `main` branch is the GitHub Pages publishing source. Use a short-lived branch and a pull request for each change. For example, working on the 2027 agenda:

1. Update `main` and create a branch:
   ```bash
   git switch main
   git pull --ff-only origin main
   git switch -c content/2027-agenda
   ```
2. Make changes, then test with `bundle exec jekyll build` and `bundle exec jekyll serve`.
3. Commit and push your branch:
   ```bash
   git add .
   git commit -m "Update 2027 agenda"
   git push -u origin content/2027-agenda
   ```
4. Open a pull request against `main` and optionally request a review.

> [!IMPORTANT]
> By defualt it will pull request against `JGIBristol/hackathon-template` beacuse this repo is folked from it, so make sure that you pull request agains the `main` of this repo.

5. After merging, check the live site and delete the branch.

The site normally rebuilds and deploys within a few minutes after a merge. Force-refresh your browser if necessary.

## Project Structure

```
.
├── 2026/                    # Archived 2026 event pages
├── index.md                 # Current event homepage
├── agenda.md                # Current event agenda
├── videos-slides.md         # Unversioned recordings (currently 2026)
├── about.md                 # General event and team information
├── _config.yml              # Main configuration file
├── _includes/               # Reusable page components
│   ├── header.html
│   ├── footer.html
│   ├── breadcrumbs.html
│   └── youtube.html
├── _layouts/                # Page templates
│   ├── default.html
│   ├── project.html
│   └── notebook.html
├── _projects/               # Individual project pages
│   ├── 01-project-title.md
│   └── 02-project-title.md
├── assets/                  # Images and stylesheets
│   ├── main.scss
│   └── logo.png
├── activities/              # Event activities and templates
│   ├── environment/         # Python environment files
│   └── templates/           # Email and form templates
├── Gemfile                  # Ruby dependencies
└── *.md                     # Main content pages (index, agenda, etc.)
```

## Yearly Archives

The [2026 archive](https://www.nordiclovedataweek.org/2026/) lives in `2026/`. It has its own copies of the agenda, videos and slides, global activities, and Where's the Data Day pages. The original unversioned pages remain in place for existing links, so changes that should appear in both copies must be applied to both.

Keep archive links pointed at year-specific pages, and preserve the referenced assets. When moving a page listed in `header_pages`, update its source path in `_config.yml`. Before repurposing an unversioned page for a new year, ensure the previous year's content and links are preserved in its archive.

## Acknowledgements

This website template is based on the [Hackathon Website Template](https://github.com/JGIBristol/hackathon-template) developed by the [Jean Golding Institute](https://www.bristol.ac.uk/golding/) at the University of Bristol, specifically by [James Thomas](https://github.com/jatonline).

The template was originally created for the [CMIP6 Data Hackathon](https://cmip6moap.github.io/) (2–4 June 2021) and has been adapted for use by the Nordic Love Data Week 2026 organizing consortium.

## License

See the [LICENSE](LICENSE) file for details.

## Contact

For questions about Nordic Love Data Week, contact the team via the [About page](https://www.nordiclovedataweek.org/about/).
