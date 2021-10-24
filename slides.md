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

- Software engineer and cloud | https://soubai.me
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

> Github Actions: enables you to create custom software development lifecycle

---

# Main concepts

          +----------------+       +----------------+
          |                |------>|                |
          |     Event      |       |   workflows    |
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
name: Run test matrix

on: [push]

jobs:
  build:
    runs-on: ubuntu-latest
    strategy:
      matrix:
        node-version: [8.x, 10.x, 12.x, 14.x]
        mongodb-version: [4.0, 4.2, 4.4]
        redis-version: [4, 5]

    steps:
      - name: Git checkout
        uses: actions/checkout@v2

      - name: Use Node.js ${{ matrix.node-version }}
        uses: actions/setup-node@v1
        with:
          node-version: ${{ matrix.node-version }}

      - name: Start MongoDB v${{ matrix.mongodb-version }}
        uses: supercharge/mongodb-github-action@1.3.0
        with:
          mongodb-version: ${{ matrix.mongodb-version }}

      - name: Start Redis v${{ matrix.redis-version }}
        uses: supercharge/redis-github-action@1.1.0
        with:
          redis-version: ${{ matrix.redis-version }}

      - run: echo "done"
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
 
