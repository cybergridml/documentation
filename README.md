## Cyber-Grid Architecture Modeling Language for Power Systems

Welcome to **CyberGridML**, an open initiative focused on modeling cyber-physical power grid systems with **SysML v2**, **CyberGridML concepts**, and web-based engineering tools.

CyberGridML provides modeling capabilities for representing the interaction between electrical grid assets, control functions, software resources, communication media, and computing infrastructure. The goal is to support clearer system architecture descriptions for modern power grids where cyber and physical components are increasingly interdependent.

## 🙋‍♀️ What is CyberGridML about?

CyberGridML is centered around a domain-specific modeling environment for cyber-physical grid engineering.

The project currently focuses on:

* **CFA — Control Function Architecture**
  Modeling grid elements, substations, buses, controllers, loads, generators, batteries, lines, and related control structures.

* **CRA — Computing Resource Architecture**
  Modeling computing resources, software resources, communication media, redundancy clusters, allocations, and cyber infrastructure links.

* **CFRA — Control Function / Resource Architecture**
  Bridging control functions with the computing and software resources that support them.

* **Hazards**
  Capturing hazardous situations and risk-related concerns at the heart of the model, so that cyber-physical architectures can be analyzed not only in terms of structure, but also in terms of potential failures, threats, vulnerabilities, and operational risks.

The main application is built with **Java**, **Spring Boot**, **SysON**, and **Eclipse Sirius Web**, providing a web-based modeling experience around SysML v2 concepts.

## 👩‍💻 Main project

Our main repository is:

* **cybergridmodel** — the CyberGridML modeling application and profile implementation.

It includes:

* the CyberGridML SysML library;
* custom SysON/Sirius Web diagram descriptions;
* project templates for CyberGridML models;
* domain-specific nodes, edges, properties, and services;
* GitHub Actions workflows for building and publishing release JARs.

## 🌈 Contributing

Contributions are welcome.

Good places to contribute include:

* improving the CyberGridML SysML library;
* adding or refining Functional, Resources or Hazards capabilities;
* improving model initialization and project templates;
* strengthening tests and CI workflows;
* improving documentation and examples;
* reporting bugs or inconsistencies in the modeling behavior.

Before contributing, please open an issue or discussion to describe the change you want to make. This helps align contributions with the project roadmap and modeling semantics.

Typical contribution workflow:

```bash
git checkout main
git pull origin main
git checkout -b feature/my-change
```

Then commit your changes and open a pull request.

## 👩‍🔬 Development stack

CyberGridML currently relies on:

* **Java 17**
* **Spring Boot**
* **SysON**
* **Eclipse Sirius Web**
* **SysML v2**
* **Maven**
* **PostgreSQL**
* **Docker Compose**
* **GitHub Actions**

For local development, PostgreSQL is expected to be available, typically through Docker Compose.

## 📦 Releases

Release artifacts are produced through GitHub Actions.

Versioned releases are based on Git tags using the following format:

```text
vX.Y.Z
```

Example:

```bash
git tag v0.1.0
git push origin v0.1.0
```

The release workflow builds the application JAR and publishes it as a GitHub Release asset.

## 👩‍💻 Useful resources

Useful resources will progressively be added to the organization and project repositories, including:

* setup instructions;
* modeling guidelines;
* CyberGridML profile documentation;
* example models;
* architecture notes;
* release and deployment instructions.

For now, the best starting point is the main application repository and its source code.

## 🍿 Fun facts

CyberGridML sits at the intersection of power systems, software architecture, distributed control, and model-based systems engineering.

In other words: we like grids, graphs, diagrams, and coffee-powered modeling sessions.

## 🧙 Building better grid models

Modern electrical grids are no longer only physical infrastructures. They are cyber-physical systems composed of electrical assets, control logic, communication networks, software services, and computing platforms.

CyberGridML aims to make those relationships explicit, navigable, and easier to analyze through model-based engineering.

