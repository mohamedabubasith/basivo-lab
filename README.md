# basivo-lab

A/B testing for product teams. A team creates an experiment ("old checkout vs new checkout"), their app asks basivo-lab which version each user should see, sends back what users did (clicked, bought), and basivo-lab tells them which version wins and whether the result is real or luck.

## How this repo is built

This product is built by AI agents ([basivo-factory](https://github.com/mohamedabubasith/basivo-factory)) from Jira tickets in project `BL`:

1. A person moves a ticket to **Selected for Development**: the agents plan it and post the plan on the ticket.
2. A person replies **/approve**: the agents write the code, run the tests, fix failures (at most 3 tries per step) and open a pull request.
3. A person reviews and merges.

Decisions every change follows are in [`.factory/knowledge/`](.factory/knowledge/). Agent settings are in [`.factory/agents/`](.factory/agents/).

## Status

Empty until ticket BL-7 (project setup) is built.
