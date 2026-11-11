# JobOps for Job Seekers

A local-first job-search workspace for collecting leads, tracking applications, following up, organizing connections, and preparing cover letters. This copy has generic starting settings and no imported applications or personal cover-letter examples.

## Share it for a beta

Keep the source in a GitHub repository so you can review suggestions and update the app. Put **only the contents of this `shareable/` folder** in that repository; never publish the parent workspace, which has your private profile and application history.

For the simplest beta, turn on GitHub Pages from the repository's `main` branch and root folder. Then share the Pages URL with the recruiter; they can pass it to job seekers. GitHub Pages has a soft 100 GB/month bandwidth limit and GitHub says it is not for free hosting of a commercial SaaS, so treat it as a testing option if the project may grow or become a service.

For a growth path, connect the GitHub repository to Cloudflare Pages using its Git integration. For this plain HTML app, set the build command to `exit 0` and the output directory to the repository root (`.`). Cloudflare deploys after pushes and provides preview URLs for pull requests. Its current docs say static asset requests are free and unlimited; if the app adds server-side functions or accounts, those have separate usage limits and costs.

Before the first commit, put the repository's `/issues/new/choose` URL in `window.JOBOPS_FEEDBACK_URL` in `index.html`. The app footer will then show **Suggest an improvement**. Review suggestions in GitHub Issues, edit the files, and push changes; the hosting service republishes the updated version.

The app files are easy to edit directly:

- `index.html` contains the page layout and labels.
- `app.js` contains app behavior, default search sources, and the URL builder in `buildSearches()`.
- `styles.css` contains visual styles.
- `.github/ISSUE_TEMPLATE/feature_request.yml` gives people a consistent way to suggest changes.

To add or change a search site, update `SEARCH_SOURCES` and the matching entry in the `builders` object inside `buildSearches()`. If the site has no stable searchable URL, use a Google site-scoped query or a link to the site's search page and explain the behavior in the card hint.

## Search behavior

Search links open current results in the chosen destination; the app does not scrape job boards. Google Maps is used to find employers by type and area. After choosing an employer, enter its name in **Company to check** to open a Google Jobs search for that company. Job Search Database is a curated directory of specialized job boards, so its link opens the directory rather than pretending it contains job listings.

Some specialist sources are searched through Google with a `site:` constraint so role and location terms can be included even when the source does not expose a stable public search URL. Review the destination results and apply on the employer's own site.

## Data and privacy

The app stores its records in the current browser's local storage and IndexedDB. It has no server, accounts, or cross-device sync. Each job seeker should use their own browser profile or device. Clearing browser data can erase their records. Do not put resumes, application histories, or contact lists in the repository.

This shareable edition starts with a separate `jobops.general.v1` storage namespace and an empty tracker. Your personal workspace remains in the parent folder and uses a different namespace. Do not publish `personal_profile.js` or `job_search_import.js` from the parent folder.
