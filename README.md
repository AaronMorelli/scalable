# Scalable

Scalable is a tool for collecting manageability and performance metrics from various data platforms and databases. Data is collected from one or more instances of a supported platform (currently Databricks, Snowflake, and PostgreSQL) and stored in a database (currently PostgreSQL, support may be expanded). Analysis and visualization tools then enable insights for the user.

## Scala? In 2026?

This is unabashedly a portfolio project; the author is a data engineer and Scalable is a full-fledged application using the more prominent languages utilized in data engineering. Writing a non-trivial application while using Scala (and Python and JavaScript) sharpens skills in these important languages. Plus, Scala is a pleasant language within which to work (though tooling is subpar).

The author is also a database nerd; collecting and analyzing the instrumentation metrics of a data platform is one of the best ways to learn the architecture and internals of that platform, leading to more effective usage of the platform for various types of workloads. And given that the author regularly works in Databricks, Snowflake, and PostgreSQL, this application can have real-world use.


## Features

- Connect to one or multiple instances of Databricks, Snowflake, or PostgreSQL over JDBC, and collect various types of platform metrics for storage (usually locally, or in a DBA instance)
  - Configuration allows control over which metrics are collected and how frequently.
- Automatically-derived datasets (from the raw metric data), via predefined PostgreSQL functions and procedures, enable quick answers to the more common performance and management questions
- Interact with the data in PostgreSQL via a set of predefined Python notebooks
- Expose the data to a JavaScript-powered dashboard in a local web browser via a set of web APIs

The Scala-written collection application and web API application can both be run either as a normal Java application (requiring that the JVM be installed) or as a standalone executable.


## Architecture

A Scala collection application is configured and then started to run against one or more instances of a supported data platform. Data is collected according to configured frequencies, and the application can be long-running (sitting quietly in a loop) or can be started periodically to collect the set of metrics that are due next. The frequency of metric collection can vary significantly depending on the individual metrics, as some metrics only need to be collected occasionally (e.g. once a day, or once every few hours), while other metrics may need a higher frequency.

Collected metrics are written to a PostgreSQL database. A "Mgmt" schema holds central configuration and logging/diagnostics. A separate schema exists for each supported platform; data collected from multiple instances of the same platform are all stored in the same set of tables, identified by the name of the instance in one of the index keys.

A separate Scala application can be started to expose the data in the PostgreSQL database through web APIs, which can then be accessed from a JavaScript application in a web browser to display the most commonly-useful metrics through appropriate visualizations.

A set of predefined Python notebooks allows a more interactive experience with the data while still providing an on-ramp to obtaining answers quickly for the most common questions.


## Contributing

Scalable is not taking PRs at this time.


## Use of AI

One of the key goals of Scalable is for the author to increase his skills in Scala, Python, and JavaScript. The vast majority of code has thus been written by hand, and the main use of LLMs has been as a conversation partner for research into specific subtasks. Some snippets in the code have been "inspired" from conversations with an LLM, but the author has never abdicated his own need to understand the solution fully; this would simply be missing the point.




