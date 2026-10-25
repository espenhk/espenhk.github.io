# espenhk.github.io

Landing page at <https://espenhk.github.io/>. `index.html` lists every public
repo under `espenhk` that has GitHub Pages turned on, by calling the GitHub API
from the browser, so a new Pages site shows up without editing this repo.

- Link target: the repo's **Website** field if set, otherwise
  `https://espenhk.github.io/<repo>/`.
- Description: the repo's GitHub description.
- Hide a repo: add the topic `unlisted` to it.
- The list is cached in the browser for an hour (unauthenticated GitHub API
  calls are limited to 60 per hour per visitor).
