.. _framework-conception:

Conception 
##########

Several conceptions were tested to develop the framework and worflow management that fit with requirements

- Basic one with Python scripts calling tools: not formal, first draft, first try to understand conception complexity
- Several workflow tool managers (Airflow from Airbnb, Luigi from Spotify, Cloudslang, ...): not convenient for flexibility in worflow conception (dependencies between the tasks)
- Home-made workflow manager in Python based on configuration file and scripts: more formal and closer to needed conception but difficulties in task dependencies and worflow management
- Galaxy (current one): worflow manager relying on output/input dependencies (better model of the data flow for meta-omic data processing)

Galaxy is choosen as tool and workflow management, because:

- Workflow conception based on output/input dependencies and not on dependencies between the tasks
- Web-based interface and API
- Docker container
- Development of numerous tools to help the development, installation, deployment of a Galaxy server
- Documentation
- Galaxy management (architecture, github, docker, ):
- Community with active developers, mailing-lists, ...
- ToolShed with numerous available wrappers for useful tools

However, there si several cons of Galaxy use

- Difficulty to understand how it works really, how to implement tools, how to deploy, ...
- Too light documentation
- Management of large databases and datasets
- Docker use
- Computation time?

ASaiM Galaxy instance is light version of Galaxy dedicated to process gut microbiota data. For this purpose, tools, workflows and databases are specifically choosen.