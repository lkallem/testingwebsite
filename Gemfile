# Ruby gem dependencies for the Jekyll build.
# Install/update with `bundle install`; run locally with `bundle exec jekyll serve`.
#
# NOTE: This site is NOT built with the classic `github-pages` gem because that
# gem only allows a fixed whitelist of themes (jekyll-theme-yat is not on it).
# Deployment instead uses a custom GitHub Actions workflow (.github/workflows/
# deploy.yml) that runs this exact Gemfile.
source "https://rubygems.org"

gem "jekyll", "~> 4.3"
gem "jekyll-theme-yat"          # site theme (see AGENTS.md: do not swap)

group :jekyll_plugins do
  gem "jekyll-feed"             # RSS/Atom feed
  gem "jekyll-seo-tag"          # SEO meta tags
  gem "jekyll-paginate"         # pagination
end
