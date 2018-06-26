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

### Requirements
Our deployment is based on several docker containers, please install docker: [Mac](https://docs.docker.com/docker-for-mac/install/), 
[Windows](https://docs.docker.com/docker-for-windows/install/) and 
[Ubuntu](https://docs.docker.com/engine/installation/linux/docker-ce/ubuntu/).

### Graph Database
A - Neo4j is already running
B - New Neo4j Instance
 mvn clean install
 kopiert in plugins ordner
### Python
- start sockercontainer
- redis server deployen
- test_import route callen
### UI
To build your own local code use `deployment/build-ui.sh /path/to/code` (e.g. `deployment/build-ui.sh .`), 
set the environment variable `REACT_APP_API_HOST` according to you API (e.g. export `REACT_APP_API_HOST=[API Endpoint]`) and 
to run a single container `deployment/run-ui.sh [PORT]` (e.g. ./deployment/run-dev-ui.sh).



## System Architecture

small description

![system overview](img/architecture.png)

### [ReactJS UI](https://github.com/MetaExp/frontend)

Cross-Browser Usablity: Use Mozilla Firefox. Input range slider-thumb styling only works with Firefox
Architectural Approach: [Flux-Pattern](https://facebook.github.io/flux/docs/in-depth-overview.html#content)

Following, according to the Flux-Pattern, we describe the API-Communication, the most important stores and components and to which stores, i.e. data changes, they listen to and which actions they trigger.

#### API-Communication

- `/src/utils/MetaPathAPI.js` holds all relevant actions regarding API-Communication
- Actions provided according to each component's functionality
- `process.env.REACT_APP_API_HOST` React env-variable holds API-Endpoint

#### Stores

- AccountStore: Stores data regarding login information, e.g. username, chosen dataset, login state
- AppStore: Navigation data, like current page and previous and next page (footer navigation)
- SetupStore: Data of setup page, i.e. chosen node sets, cypher queries for neo4j graph visualization through forked third party [neo4j-graph-renderer](https://github.com/jbitton/neo4j-graph-renderer/pull/7)
- ExploreStore: Meta-Paths and rating information, chosen rating interface, batch size
- ResultStore: Holds explanatory data as a similarity score, top-k contributing meta-paths and additional meta-path information

#### Components

Main Parts: Setup page, Explore page, Result page

**Setup Page:**

-

**Explore Page:**

-

**Result Page:**

-

### [Python Flask API and Algorithmic Backend](https://github.com/MetaExp/backend)

#### Overview
The python backend is structured into several components, each is responsible for either serving the api or part of the algorithmic backbone. The algorithmic parts are in their basic functionality. Work on the individual components is conducted outside of the MetaExp-Project, but might be referenced here in the future.

- Serving Modules
  - `server` : Serve API endpoints with a flask/gunicorn server
  - `redis_own` : Provide access to a redis database where node embeddings are stored
  - `neo4j_own` : Connector to the neo4j database
- Algorithmic Modules
  - `active_learning` : Provide active learning functionality for interactively learning a preference model of meta-paths
  - `domain_scoring` : Calculate the similarity of two node sets given a preference over meta-paths
  - `embeddings` : Compute vector-embeddings of MetaPaths
  - `explaination` : Explain the similarity score

#### API

The API is not stateless, the image below describes the process of interating with the API.
Users need to login to the system for a specific dataset.
This is followed by the input-set selection and then the iterative rating of paths.
Finally the user can view the similarity.
These phases are sequential. 
Since this is a prototype, it is likely that the system will crash if they are called arbitrarily.

<img src="img/python_api_overview.png" alt="API_calls" width="600px"/>

![API_procedures](img/python_api_overview.png =250x)

- **`get-available-datasets`**
  - Returns a list of all available neo4j-datasets in the backend.
  - *IN* `None`
  - *OUT* `{[dataset1, dataset2, ...]}`

- **`login`**
  - Login into the system.
  - *IN* `{'username': username, 'dataset': datasetname, 'purpose': purpose_of_similarity}`
  - *OUT* `{'status': 200}`
 
- **`node-types`**
  - Select the input node types for both sets for the algorithm.
  - *IN* `{'start_label': label_of_start_node, 'end_label': label_of_end_node, 'start_node_ids': list_of_node_ids, 'end_node_ids': list_of_node_ids}`
  - *OUT* `{'status': 200}`
  
- **`next-meta-paths/<int:batch_size>`**
  - Retrieve the next batch_size MetaPaths that should be labelled by the user.
  - *IN* `None`
  - *OUT* `{'metapaths': [path1, path2, ... ], 'next_batch_available': bool}`

'meta_paths': [{'id': 3,
                   'metapath': ['Phenotype', 'HAS', 'Association', 'HAS', 'SNP', 'HAS', 'Phenotype'],
                   'rating': 0.75},...]
    'min_path':{}
    'max_path':{}

- **`rate-met-paths`**
  - Send metapaths that have been rated.
  - *IN* `{'meta_paths': [{'id': 3,
                   'metapath': ['Phenotype', 'HAS', 'Association', 'HAS', 'SNP', 'HAS', 'Phenotype'],
                   'rating': 0.75},...],
    'min_path':{'id': ,...},
    'max_path':{'id': ,..}}`
  - *OUT* `{'status': 200}`
 

- **`select_dataset`**
  - HI
  - *IN* `None`
  - *OUT* `{'status': 200}`
 
 
- routennamen, methode, input, output, purpose

### [Neo4j Graph Algorithms](https://github.com/MetaExp/neo4j-graph-algorithms)
- hinzugefügte procedures, input output, purpose

## Contributors
Freya Behrens, Sebastian Bischoff, Pius Ladenburger, Julius Rückin, Laurenz Seidel, Fabian Stolp, Michael Vaichenker and Adrian Ziegler.

## Acknowledgments
This work was conducted with our project partners [neo4j](https://neo4j.com), [helmholz zentrum münchen](https://www.helmholtz-muenchen.de/) and [knowing health](https://knowing-health.com/).

## License
All work is licensed under [MIT License](LICENSE.md).
