In dbt, "built-in variables" generally refer to the Jinja context variables and Environment variables that dbt automatically populates during a run.

These are grouped into several categories based on how you access them and what information they provide.

1. The target Variable
The target object contains information about your current connection profile (defined in profiles.yml).

target.name: The name of the target (e.g., dev, prod).

target.schema: The default schema for the current target.

target.type: The database type (e.g., snowflake, bigquery, postgres).

target.database: The database name (adapter-specific).

target.threads: Number of threads configured for the run.

target.profile_name: The name of the active profile.

2. Node & Model Context
These variables provide information about the specific model or resource currently being processed.

this: Represents the current model's relation (database, schema, identifier). Used in incremental models or custom SQL.

model: A dictionary containing metadata about the current model (name, unique_id, config, etc.).

schema: The schema where the current model is being built.

database: The database where the current model is being built.

3. Execution & Run Context
These provide details about the dbt invocation itself.

execute: A boolean that is True during the "execution" phase (when dbt is actually running SQL against your DB) and False during parsing.

flags: An object containing the CLI flags passed to the command (e.g., flags.FULL_REFRESH, flags.WHICH).

invocation_id: A unique UUID generated for every dbt command run.

run_started_at: The timestamp (Python datetime object) when the run began.

selected_resources: A list of all nodes (models, tests, etc.) selected for the current command.

thread_id: An identifier for the current Python thread executing the model.

4. Project-Level Information
project_name: The name of the project as defined in dbt_project.yml.

dbt_version: The version of dbt currently running.

graph: A massive dictionary representing the entire dbt project DAG (nodes, sources, exposures).

5. Built-in Functions as Variables
While these are technically functions, they are part of the built-in context you'll use constantly:

var: Used to access project variables defined in dbt_project.yml or via the CLI.

env_var: Used to pull environment variables from the system (e.g., {{ env_var('DBT_SECRET_KEY') }}).

builtins: A dictionary providing access to dbt's internal methods (like ref or source) even if you have overridden them with custom macros.

6. dbt Cloud Environment Variables
If you use dbt Cloud, several additional environment variables are automatically available:

DBT_CLOUD_PROJECT_ID: The ID of the project.

DBT_CLOUD_RUN_ID: The ID of the current run.

DBT_CLOUD_ENVIRONMENT_TYPE: Returns dev, staging, or prod.

DBT_CLOUD_GIT_SHA: The git commit SHA for the current run.

Would you like me to show you an example of how to use one of these in a macro or a conditional model (e.g., using target.name to limit data in dev)?
