# QA Release and Testplan documentation

## Browsers list we use to test the software

| OS      | Browser                               |
|---------|---------------------------------------|
| MacOS   | Firefox                               |
| MacOS   | Google Chrome                         |
| MacOS   | Safari                                |
| Windows | Edge                                  |

## Focused testing

### What? Why?

To prepare for a production release we need as much test coverage as we possibly can on each (new) feature.
Certain improvements (for example mentioned in the Release notes) need to be tested manually to be sure it works as
intended.
These (mostly new) features are usually not yet implemented in the E2E Robotframework test coverage.

### When?

Each release.

### How?

#### Preparations

- Get the Release notes and compare with the 'current' production
  release tag.
- Check if all PR's merged are mentioned in all these release notes.
- Write down what you would like to inform stakeholders about (in plain language) when informing them about the upcoming
  release
- These are actually your official Release notes and at the same time the test scenario's that you need to test manually
- Write them down in a way that you can add screenshots and write down steps you take (or actions you perform) to prove
  that you have tested it properly.

#### Perform the test

This is usually performed on the ACC environment, but this is not mandatory.

Write this in your testreport while testing:

- Testperiod: DD-MM-YYYY
- Date of this testreport: DD-MM-YYYY
- Github release tag you are testing with: (for example) woo-web 1.4.29
- URL where you have tested on: (for example) [https://open.minvws.nl/](https://open.minvws.nl/)
- Tests performed by: `name of the tester`
- Hardware used: (for example) Macbook Pro 14 inch (M3 pro processor)
- Software/browser used: (for example) Google Chrome Versie 120.0.6099.234

### What is the result?

We can send this Testreport in Markdown together with the ✅ new features as Release notes to the Product Owner.
He can now ask for a release to Ops and inform for example stakeholders.

The complete checklist for a release can be found in this repo.

For each production release, we now create a new issue in the coordination repository (copy into a new ticket) with
details about the upcoming release and QA adds the Testreport as a comment.

## Exploratory testing

### What? Why?

Surf to the website and start with an open mind. You need to be able to look 'fresh' at all the details and all the UX
and UI. This way you always see improvements.

### When?

From time to time....about once a month we do exploratory testing for 2-3 hours.

### How?

#### Examples how we do this

- open the website as if you do not know anything about this website
- make your browser very small or very wide and see how the website reacts
- open the website on your phone in landscape and portrait mode
- search for too long words in the search engine and see what happens with the design
- try to access hidden pages or admin-only pages
- try to think like a criticaster and see what is wrong about the website

### Why do we do this again?

- To find 'edge case' bugs (while try breaking things)
- to keep improving the website for all kinds of viewers/users
- to not have a tunneled vision about this website

### What is the result?

- usefull issues to fix bugs (make screenshots and write down steps you took)
- usefull questions to the UX designers about the interface
- new knowledge for the Frontend developers about the responsiveness of the website (and sometimes accessibility
  improvements too)
- keeps the team sharp

## E2E Testcoverage

### What? Why?

A Robotframework can 'act as a human' and surf around and 'do stuff' on a website or in the admin portal for example.
This way you can test all kinds if features, like fill a form, do a search, open the menu.

### When?

TEST & ACC environments have E2E Robotframework tests running every night.
And in the CI these are executed while checking each PR to the `main` branch.

### How?

Fully automated with workflow files / Github Actions configurations.

### What is the result?

A summary with outcome per E2E test. If a test fails, the development team has work to do to fid that. This is an
example of this summary:

- Total tests: 6
- :green_circle: 6 passed
- :red_circle: 0 failed

| Test                           | Result         |
|--------------------------------|----------------|
| P01 - Zoeken                   | :green_circle: |
| P02 - Zoekresultaten filteren  | :green_circle: |
| P03 - Document overzichtpagina | :green_circle: |
| B01 - Inlogmodule              | :green_circle: |
| B02 - Besluitdossier filteren  | :green_circle: |
| B03 - Besluitdossier zoeken    | :green_circle: |

The current E2E testcoverage can be found here: [https://github.com/minvws/nl-rdo-woo-web/blob/main/docs/test.md](https://github.com/minvws/nl-rdo-woo-web/blob/main/docs/test.md)

## Production release E2E Testcoverage meeting

After each successful production release the QA team has a meeting to discuss what extra E2E robot tests are needed to
cover the new features. These tests are then added to
the [/docs/test.md](https://github.com/minvws/nl-rdo-woo-web/blob/main/docs/test.md) file with a 'work in progress'
icon. This way the test engineer knows what he needs to write tests for and the team knows whats coming in the near
future.
