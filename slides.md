%title: Github actions in Action - Blablaconf 2021
%author: Abderrahim - @soub4i
%date: 2021-10-28




# Github actions in Action

> a brief introduction to Github actions

---

# whoami


MMMMMMMMMMMMMMMMMMMMMMMMmy+///+o++++sydNMMMMMMMMMMMMMMMMMMMM
MMMMMMMMMMMMMMMMMMMMMMMmo+oshddmmdhysooshNMMMMMMMMMMMMMMMMMM
MMMMMMMMMMMMMMMMMMMMMMNsohdmNNNNMMMMNNhoosNMMMMMMMMMMMMMMMMM
MMMMMMMMMMMMMMMMMMMMMdoydmmmNNNNNMMMMNNmsodMMMMMMMMMMMMMMMMM
MMMMMMMMMMMMMMMMMMMms+osssydmNNNNMMMMNNNmosMMMMMMMMMMMMMMMMM
MMMMMMMMMMMMMMMMMMMdosoosssosyhdmmdmNmmNNysMMMMMMMMMMMMMMMMM
MMMMMMMMMMMMMMMMMMMyossossyso++o/syymhyyyyyMMMMMMMMMMMMMMMMM
MMMMMMMMMMMMMMMMMMMyyyysoossyyNNohysyddhyysmMMMMMMMMMMMMMMMM
MMMMMMMMMMMMMMMMMmhyyhhhhhyshmMMmhdsooyhhydMMMMMMMMMMMMMMMMM
MMMMMMMMMMMMMMMMMyssyhhhddyo+shymddmddddhhMMMMMMMMMMMMMMMMMM
MMMMMMMMMMMMMMMMMmossyyyhhso+osyhmNNmmmmmNMMMMMMMMMMMMMMMMMM
MMMMMMMMMMMMMMMMMNooss+:://ooooydNNNmNmmhmMMMMMMMMMMMMMMMMMM
MMMMMMMMMMMMMMMMMMs++o+o+osyhhyo/+ymdddddNMMMMMMMMMMMMMMMMMM
MMMMMMMMMMMMMMMMMMy///shyo++oyhdy+:shhydMMMMMMMMMMMMMMMMMMMM
MMMMMMMMMMMMMMMMMMNo:-/yhyo+oshdmh+soosNMMMMMMMMMMMMMMMMMMMM
MMMMMMMMMMMMMMMMMMMN/--/ydmmmmmds/::/+dMMMMMMMMMMMMMMMMMMMMM
MMMMMMMMMMMMMMMMMMMMy:..-:+o++o/-../sdMMMMMMMMMMMMMMMMMMMMMM
MMMMMMMMMMMMMMMMMMMMdo/.``````.``.:sdmMMMMMMMMMMMMMMMMMMMMMM
MMMMMMMMMMMMMMMMMMMMmo+/:-...`..:+yddmNMMMMMMMMMMMMMMMMMMMMM
MMMMMMMMMMMMMMMMMMMMMs++//:///++shmmmdmmmy+sydmNNMMMMMMMMMMM
MMMMMMMMMMMMMMMMMMMmys++///++osydmmmmmNmd/----:://+osydmNMMM
MMMMMMMMMMMMMMMmds:-+++////+osyhdmmmmmNd:........----::/+osh
MMMMMMMMMMMNds+-..`./+///++osyhhdmmmmNy-``...`.`.....----://
MMMMMMMMmyo/--...```:/+++yddhyhdmmNmd/``````````.```.....---
MMMMMNdo/---....````-syyyhNNmhdmNNmo.```````````````````.-.-
MMMMNo:--....````````oddmmmNmmmNNy:`````` ``` ```````````.`.
MMMN+---...```````````/hmmmNNNmh/`                  ````````
MMMy--...```````       .odmmds:`                       `````
MMMo--..``````           ./:`                           `` `
MMM/...``````                                               
MMM:..````````                                              



Abderrahim SOUBAI-ELIDRISI (@soub4i)

- Software engineer & cloud architect | https://soubai.me
- Host S7aba Podcast (Moroccan cloud podcast) | https://s7aba.ma

---

# Before we start - 1

## Github:

a provider of Internet hosting for software development and
version control using Git.

---

# Before we start - 2

## Git:

a free and open source distributed version control system

---

# Before we start - 3

## DevOps:

- a set of practices that combines software development (Dev) and
  IT operations (Ops).

- It aims to **shorten** the systems development life cycle and
  provide continuous delivery with high software quality.

---

# Before we start - 4

## CI/CD:

is the combined practices of continuous integration (CI)
and either continuous delivery or continuous deployment (CD).

            +----------------+       +----------------+       +----------------+         +----------------+
            |                |------>|                |------>|                |-------->|                |
            |      Code      |       |      Build     |       |      Test      |         |     Deploy     |
            +----------------+       +----------------+       +----------------+         +----------------+

- **Continuous delivery**: the process of delivering software
  continuously to customers (manual deployment).

- **Continuous deployment**: the process of delivering software
  continuously to customers (automatic deployment).

---

## Definition

> Github Actions: enables you to create custom/automate software development lifecycle


                  +----------------+       +----------------+       
                  |                |------>|                |
                  |  When this     |       |   Do this      |
                  +----------------+       +----------------+


---

## Usage

- Project management
- Linting and formatting
- Building
- Testing
- Deploying
- Putting releases out


---

# Main concepts

          +----------------+       +----------------+
          |     Event      |------>|                |
          | (push,tag,...) |       |   workflows    |
          +----------------+       +-------|--------+
                                           |
                                           |
                                           |
                                           |
                                           v
                                   +----------------+
                                   |                |
                    +------------- |      Jobs      |-----------+
                    |              +----------------+           |
                    |                      |                    |
                    |                      |                    |
                    |                      |                    |
           +----------------+   +----------------+  +----------------+
           |      Step      |   |      Step      |  |      Step      |
           |                |   |                |  |                |
           +----------------+   +----------------+  +----------------+

---

## Main concepts

- **Actions**: are the smallest portable building block of a workflow and can be combined as steps to create a job.

- **Events**: are specific activities that trigger a workflow run.

- **Runner**:

  - a machine with the Github Actions runner application installed
  - runner waits for available jobs it can then execute.
  - After picking up a job they run the job's actions and report the progress and results.
  - can be hosted on **Github** or self-hosted on your **own** machines/servers.

- **Job**:

  - made up of multiple steps and runs in an instance of the virtual environment.
  - Jobs can run independently of each other or sequential.

- **Step**:

  - a set of tasks that can be executed by a job.
  - can run commands or actions.

- **Workflow**: is an automated process that is made up of one or multiple jobs

  - can be triggered by an event.
  - defined using a YAML file in the `.github/workflows` directory.

---

## Pros and cons

.--------------------------------+-------------------.
|Advantages                      | Disadvantages     |
|--------------------------------+-------------------|
|Free (pay-as-you-go)            |No native caching  |
|--------------------------------+-------------------|
|cross-platform (Linux/macOS/Win)|Single platform    |
|--------------------------------+-------------------|
|Matrix builds/any language      | poor documentation|
'--------------------------------+-------------------'


---

## Example 1

~~~

name: Hello-World-Actions

on:
  push:
    branches: [main]
  # Allows you to run this workflow manually from the Actions tab
  workflow_dispatch:

jobs:
  say_hello:
    # The type of runner that the job will run on
    runs-on: ubuntu-latest
    steps:
      - name: Say Hello
        run: echo Hello World!

      - name: Say Goodbye
        run: |
          echo Job Finished.
          echo Goodbye!
~~~

---

## Example 2

~~~
on:
  pull_request:

jobs:
  commit-lint:
    steps:
      # ...
  unit-test:
    needs: commit-lint
    strategy:
      matrix:
        python-version: [3.7, 3.8]

    steps:
      # ...
      - name: Test with pytest
        run: |
          # ...
          pytest --force-flaky --min-passes 1 --max-runs 5 --cov=jina --cov-report=xml -n 1 --timeout=120 -v tests/unit

  integration-test:
    needs: commit-lint
    strategy:
      matrix:
        python-version: [3.7, 3.8]

    steps:
      # ...
      - name: Test with pytest
        run: |
          # ...
          pytest --force-flaky --min-passes 1 --max-runs 5 --cov=jina --cov-report=xml -n 1 --timeout=120 -v --ignore-glob='tests/integration/hub_usage/dummyhub*' tests/integration

~~~

---

# Misc

## GUI and Marketplace

## Limitations

- Each workflow can run for a maximum of 58 minutes including queuing and execution.
- Each workflow can run a maximum of 100 actions
- A repository can run a maximum of 2 workflows concurrently
- A task performed within an action cannot trigger other actions.

## Alternatives

- GitlabCI (Mohamed Daoudi talk 19:40PM)
- CircleCI
- Jenkins
- TravisCI
- Drone
- Codeship

---

# Demos & slides

~~~
 ▄▄▄▄▄▄▄  ▄     ▄▄▄▄▄▄  ▄  ▄▄▄▄▄▄▄
 █ ▄▄▄ █ ▀█▄█▀ ▄ ▄ ▀▄▀█▄ █ █ ▄▄▄ █
 █ ███ █ ▀▀▄▀▄▄▄▄ ██▄█ ▀█▀ █ ███ █
 █▄▄▄▄▄█ █ █ ▄▀█▀█▀▄ █▀█ ▄ █▄▄▄▄▄█
 ▄▄▄▄▄ ▄▄▄▄▄ █▀▄▄▄▄ ▀▄██ █▄ ▄ ▄ ▄
 ██▄▀ ▄▄▀▀█ ▄▄  ▄▀▄▀▀█▀▀▀▄ ▀▄▄▄▀█▀
 █▄█ █ ▄ ██▀█  ▀ ▀▄ ▄ ▀█▀▀█▀▄█▄▀  
 █▀██▀▀▄█▄██ ▀██▄█ █▀▀ ▄▀▄▄██▄  █▀
 ▄    ▄▄▄▄▄▄ █▀▄ ▀▄▄▀▄▀█▀▀█▀█▄ ▀▄
 ▀▀██▀█▄▄ ▄▄▄▄  ▄█▀▀▀▀██▀ ▄█  █ █▀
 ▄▄ ▀▄█▄▄▄▄▄█  ▀▀ ▄  ▀▀█ ▄▀  ▄ ▀▄
 █▀█ █▀▄ ▀▄  ▀██▄▀▀█▀█▀ ▀▄▄█▄ █ █▀
 █ █ ▄▄▄▄▀▄▀ █▀▄██▄ ▄ ▀▄ ▄████▀▀ ▄
 ▄▄▄▄▄▄▄ █▄ ▄▄  ▄██▀▀▀█ ▄█ ▄ ██▀▄▀
 █ ▄▄▄ █ ▄▄██  ▀▄ ▄█▄▀▀█▀█▄▄▄█▀▀ █
 █ ███ █ █ ▀ ▀██▄█▀▀▀█▄  ▄▀ ▀▀▄▄▀▀
 █▄▄▄▄▄█ █▄█ █▀▄█ ▄  ▀██▄▄▄ ▀ █▀▄
