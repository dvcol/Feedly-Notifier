# Repository Guidelines

## Project Structure & Module Organization

Feedly Notifier is a browser extension for Chrome, Firefox, Opera, and Edge. Source files live in `src/`: JavaScript modules are under `src/scripts/`, extension pages are `popup.html` and `options.html`, and static resources are grouped into `styles/`, `images/`, `sound/`, and `_locales/`. Store-listing translations are maintained separately in `translations/store/`. Grunt generates unpacked extension files and release archives in `build/`; treat that directory as disposable output. The `e2e/` directory is reserved for end-to-end coverage but currently has no committed tests.

## Build, Test, and Development Commands

- `npm ci` installs the exact dependency versions from `package-lock.json`.
- `npm run lint` checks JavaScript with the repository's ESLint configuration.
- `npm run lint:fix` applies safe, automatic lint fixes.
- `npx grunt sandbox --clientId=<id> --clientSecret=<secret> --browser=chrome` creates an unpacked development build in `build/`. Supported browser values are `chrome`, `opera`, and `firefox`.
- `npx grunt build --clientId=<id> --clientSecret=<secret> --browser=firefox` cleans, builds, and packages a browser-specific ZIP.

After a sandbox build, load `build/` as an unpacked/temporary extension in the target browser.

## Coding Style & Naming Conventions

Follow `.editorconfig`: UTF-8, four-space indentation, final newlines, and no trailing whitespace. ESLint targets ES2021 browser scripts and enforces double quotes, semicolons, braces for control flow, and indented `switch` cases. Use `camelCase` for variables and functions and descriptive lowercase filenames consistent with `feedly.api.js` and `background.js`. Keep browser-specific behavior explicit and localize user-facing text through `src/_locales/`.

## Testing Guidelines

There is no automated test runner or coverage threshold yet. Before submitting, run `npm run lint`, build the affected browser target, and manually exercise authentication, feed refresh, badge counts, popup actions, and options persistence. For UI changes, verify both popup and options pages. Add future browser-flow tests under `e2e/` with behavior-focused names such as `popup-refresh.spec.js`.

## Commit & Pull Request Guidelines

Recent history uses short, imperative subjects such as `Sanitize feed content in all browsers`; dependency updates use `Bump <package> from <old> to <new> (#123)`. Keep commits focused and avoid signatures, attribution footers, or generated-by notices. Pull requests should explain the user-visible change, link relevant issues, list browsers manually tested, and include screenshots for UI changes. Confirm lint and a clean browser-specific build before requesting review.

## Security & Configuration

Never commit Feedly credentials, access tokens, generated `keys.json`, or build artifacts. Pass sandbox credentials only through local build arguments and review generated packages before distribution.
