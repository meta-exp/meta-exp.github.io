# MetaExp: Interactive Explanation and Exploration of Large Knowledge Graphs

## TODO Picture

## Motivation

We present MetaExp, a system that assists the user during the
exploration of large knowledge graphs, given two sets of initial
nodes. At its core, MetaExp presents a small set of meta-paths to the
user, which are sequences of relationships among node types. Such
meta-paths do not overwhelm the user with complex structures, yet
they preserve semantically-rich relationships in a graph. MetaExp
engages the user in an interactive procedure, which involves simple
meta-paths evaluations to infer a user-specific similarity measure.

More information can be found in the [paper](resources/paper.pdf), [slides](resources/presentation.pdf) and the [poster](resources/poster.pdf).

## TODO  Deployment


## System Architecture

small description

![system overview](img/architecture.png)

### [ReactJS UI](https://github.com/MetaExp/frontend)
 toso small description
 - use Mozilla Firefox
 - komponenten
 - stores

### [Python Flask API and Algorithmic Backend](https://github.com/MetaExp/backend)
- routennamen, methode, input, output, purpose
- generelles ablaufdiagram
- python komponenten

### [Neo4j Graph Algorithms](https://github.com/MetaExp/neo4j-graph-algorithms)
- hinzugefügte procedures, input output, purpose

## Contributors
Freya Behrens, Sebastian Bischoff, Pius Ladenburger, Julius Rückin, Laurenz Seidel, Fabian Stolp, Michael Vaichenker and Adrian Ziegler.

## Acknowledgments
This work was conducted with our project partners [neo4j](https://neo4j.com), [helmholz zentrum münchen](https://www.helmholtz-muenchen.de/) and [knowing health](https://knowing-health.com/).

## License
All work is licensed under [MIT License](LICENSE.md).
